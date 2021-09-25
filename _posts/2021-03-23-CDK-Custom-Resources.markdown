---
layout: single
title: CD-Okay that's how you do custom resources
tags: cdk, aws
---

Recently I've needed to use [CDK Custom Resources][cdk-custom-resources] and they're _slightly_ different from traditional CloudFormation Custom Resources.
The documentation tells you to wrap your response in a `Data` key, but it doesn't explain why.

When you use a CDK custom resource, CDK actually deploys a [JavaScript lambda][cdk-framework-lambda] which acts as a wrapper around your lambda:
This wrapper does several things which we'll go in to detail on:

## Handling Responses to CloudFormation

This provider lambda will handle the responses to CloudFormation for you, including serialising your data and including the success codes.
Your actual lambda doesn't need to do anything but execute successfully and return a JSON-serialisable object from its handler.
The provider lambda takes the result of your lambda and includes it in the CFn response so you can use your `getAtt`/`get_att` methods as you would in the CFn world.

## Allows you to execute long running tasks

Sometimes the work you need to do takes some time, and managing retries of your resources can be a complex engineering challenge.
The provider will invoke your lambda at regular intervals, for your lambda to check if your event operation had completed.

> But that will only give you 15 minutes?

Yeap if the provider was just a lambda. The provider starts out as a lambda, but if you specify a `isComplete` handler CDK will create you a [Step Function (!)][step-function] to periodically call your function at regular intervals (that you specify) to a maximum timeout (that you specify), and then handle returns to CloudFormation.

It very much takes away all the pain of managing long-running tasks yourself. Now you may ask is it really that difficult to do long runnning tasks given it's a state machine or possibly an EC2 and the answer is no, but CDK is all about making things easier and simpler. Why should you manage the long running tasks and state machines when you can focus on determining if the resource is ready yet? Let's face it, you're paying for the lambdas and state machines either way, chances are the CDK team will make them as cheap as they can.

## If it's so simple why did you get stuck?

Well, I thought they were like regular CloudFormation Custom Resource lambdas, but they're simpler. First let's look at what a CloudFormation Custom Resource lambda has to do, and don't [forget to bundle `cfnresponse`][cfn-response-module] or make sure you upload it as a ZipFile:

```python
import boto3
import cfnresponse # lol, or inline it

lambda_ = boto3.client('lambda')

def handler(event, context):
    the_lambda  = lambda_.get_versions_by_function(FunctionName='KeepUpAppearances')
    versions = [int(version["Version"]) for version in the_lambda['Versions'] if version["Version"] != '$LATEST']
     print(f'The following versions are available {versions=}')
     latest_version = max(versions)
     response_data = {
         'LatestVersion': latest_version
     }
     cfnresponse.send(event, context, cfnresponse.SUCCESS, response_data, event['PhysicalResourceID'])
```

In one CDK application with two custom resources I've managed to get CloudFormation to bundle `cfnresponse` in for only one...

What about in CDK land then?

```python
import boto3


lambda_ = boto3.client('lambda')

def handler(event, context):
    the_lambda  = lambda_.get_versions_by_function(FunctionName='KeepUpAppearances')
    versions = [int(version["Version"]) for version in the_lambda['Versions'] if version["Version"] != '$LATEST']
     print(f'The following versions are available {versions=}')
     latest_version = max(versions)
     response_data = {
         'LatestVersion': latest_version
     }
     return {
         'Data': response_data
     }
     
```

In this very simple example, it doesn't change much, but you still don't have to worry about that pesky cfnresponse.

You have to make sure that you wrap the data you want to be made available in that `Data` key though.

The [`onEvent` handler][on-event] method invokes the lambda, then coalesces the response data back in to a super object in the [`createResponseEvent`][create-response]: with this little JavaScript magic (the [spread operator][spread-operator]):

```typescript
return {
    ...cfnRequest,
    ...onEventResult,
    PhysicalResourceId: physicalResourceId,
  };
```

where `onEventResult` is the response of our lambda. This super object is then used in the [`cfnResponse.submitResponse`][provider-response] method:

```typescript
export async function submitResponse(status: 'SUCCESS' | 'FAILED', event: CloudFormationEventContext, options: CloudFormationResponseOptions = { }) {
  const json: AWSLambda.CloudFormationCustomResourceResponse = {
    Status: status,
    Reason: options.reason || status,
    StackId: event.StackId,
    RequestId: event.RequestId,
    PhysicalResourceId: event.PhysicalResourceId || MISSING_PHYSICAL_ID_MARKER,
    LogicalResourceId: event.LogicalResourceId,
    NoEcho: options.noEcho,
    Data: event.Data,
  };

  log('submit response to cloudformation', json);

  const responseBody = JSON.stringify(json);

  const parsedUrl = url.parse(event.ResponseURL);
  await httpRequest({
    hostname: parsedUrl.hostname,
    path: parsedUrl.path,
    method: 'PUT',
    headers: {
      'content-type': '',
      'content-length': responseBody.length,
    },
  }, responseBody);
}
```

## Summary

When I first looked in to this I was really confused why there was a need to wrap your response in `Data`, but it makes sense considering you could return anything. The Custom Resources implementation under the hood is really impressive, and now I understand it more I can certainly see more ways to use it; from large scale  ingestion with SQS + Lambda (where my `onEvent` can generate millions of messages and `isComplete` can check if the queue is empty) to EC2 fleet setup.

[cdk-framework-lambda]: https://github.com/aws/aws-cdk/blob/master/packages/%40aws-cdk/custom-resources/lib/provider-framework/runtime/framework.ts
[step-function]: https://github.com/aws/aws-cdk/blob/41a2b2ef39a3d2b46ae6e2c6f3480e786e8022b9/packages/%40aws-cdk/custom-resources/lib/provider-framework/provider.ts#L162
[cfn-response-module]: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-lambda-function-code-cfnresponsemodule.html#w2ab1c27c24c14b9c15
[provider-response]: https://github.com/aws/aws-cdk/blob/25e8d04d7266a2642f11154750bef49a31b1892e/packages/%40aws-cdk/custom-resources/lib/provider-framework/runtime/cfn-response.ts#L33
[on-event]: https://github.com/aws/aws-cdk/blob/41a2b2ef39a3d2b46ae6e2c6f3480e786e8022b9/packages/%40aws-cdk/custom-resources/lib/provider-framework/runtime/framework.ts#L26
[create-response]: https://github.com/aws/aws-cdk/blob/25e8d04d7266a2642f11154750bef49a31b1892e/packages/%40aws-cdk/custom-resources/lib/provider-framework/runtime/framework.ts#L153
[spread-operator]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax