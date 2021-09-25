---
layout: single
title: Parameters, please
tags: aws, iac, jakes-builders-library
---

A great friend recently asked if I could help an individual in the CDK slack channel. This individual had a DynamoDB table in one CDK stack and wanted to depend on it in another for a producer/consumer of data in that table.
The individual then changed the logical ID of that resource and boomalaboomala it went boom.

The logical ID I hear you ask? Okay quick detour, this part highlighted:

```python
from aws_cdk import (core, aws_s3 as s3)

class ExampleStack(core.Stack):
    def __init__(self, scope: core.Construct, id: str):
        super().__init__(scope, id, **kwargs)

        self.hyacinthe = s3.Bucket(
            self, 
            "ItIsPronouncedBookay", # <-- this is the Logical ID
            bucket_name = "hyacinth"
        )
```

Changing the logical ID in CloudFormation generally means that it is a different resource. CloudFormation will both try to delete it and recreate it, with some fun things happening.

I did it with a Lambda, and didn't update the function name, and CloudFormation complained that the function already existed. _Like yes of course it exists_... ohhh it's a new thing to you. Of course, I changed the lambda function name and then it was fixed. Function deployed, accolades collected, yadayadayada.

**Back on topic.**

This individual had `overrideLogicalIds` turned on for some reason, I didn't explore why but one assumes that since this is non-default behaviour they reasonably knew what they were doing. Even if they didn't, the solution reasonably remains.

The individual had a CfnExport (which CDK generates for you under the hood when you pass classes/Stacks/Constructs around) which was failing every time because the Logical ID kept changing. How do you get around this? With our trust friend AWSSMPM!

## AWS Systems Manager Parameter Store

Systems Manager is something that I don't work with a lot of (mostly dealing with serverless) but there are two features of it I absolutely adore; Parameter Store, and Session Manager. Today we're covering Parameter Store.

__Parameter store can store parameters of anything!__

You know AWS Secrets Manager? Before we had that (which was only a few years ago) we used Parameter Store and IAM policies, because if you managed to break the several security boundaries we already had you probably had a reasonable level of access anyway and would discover the secret.

_[Editor's note: I am fortunate to work in an organisation with a mature AWS Organisation that has sensible defaults and good layers of security, so we could relax the normal security rigmarole in a few select cases!]_

You can store parameters for applications in there too, or the AMI IDs for your regularly-baked golden AMIs. You are baking them, right?

Parameter Store also enjoys first class support in _native_ CloudFormation with [Dynamic References][dynamic-references]. The problem with Dynamic References for SSM at least is that you must specify a version; and "$LATEST" is not a version unlike in the lambda world. This makes sense, because it is supposed to be a stable build. Parameters are owned by the account, and if you're the only one in that account that's great—but that's not the case. Remember, the foundations AWS create (like dynamic references and their uses) must work for everybody.

There are two solutions.

### Update your applications

If you control the code for your applications this is brilliant, as you can probably change references that use environment variables to get parameters from parameter store, or have code that runs alongside them to set those environment variables.

Create a new parameter in your CDK class that exports and that's it, the value is updated each time the stack is deployed.
Your applications can fetch this on startup, regularly in code execution, or when a resource is provisioned.

As an example if you update the parameter, you scan scale out your EC2s to pick up the new parameter and see if it works, if it doesn't you can quickly revert and reprovision and done. Your CFn deploy time will probably slightly improve

### ParamExim

Export it and re-import it.

> But Jake you just said that you can't use Latest, and I want to use the latest

This is absolutely right, you cannot do this in pure CloudFormation with Dynamic References.

The power of the CDK however, allows you to do so much more than simply dynamic references. In fact, in the CDK's [very own guide][cdk-ssm] for using Parameter Store they offer support for getting the latest _at deploy time_. Not synth time when you execute `cdk deploy` and get your template, but when that template is actually `cloudformation:CreateChangeSet`'d and deployed.

> But Jake, I'm not using CDK yet

First I strongly suggest you start moving as much as you can. You can use CDK as a wrapper as it has first class support for CloudFormation, which is paradoxical as it is CFn.

![Yo I heard you like CDK][cdk-xzibit-meme]

Then, you can use AWS Custom Resources. If CDK didn't have such wonderful first class support for getting the latest, you could use an AWS CDK Custom Resource to [wrap an AWS API Call][cdk-wrap-api].
Your Custom Resources can depend on a single Lambda Function that is deployed once in your account, because a Custom Resource is either backed by SNS or Lambda, the ARN for either is the Service Token. If you deploy a single Lambda Function in an account and you give it a name, you can re-create that ARN easily:

`!Sub 'arn:${AWS::Partition}:lambda:${AWS::Region}:${AWS::AccountId}:ParameterStoreLookup'`

That's all there is to it.

## Wrapup

If your resources are tightly coupled, you don't need to worry about logical IDs changing, and your configuration can be fixed in Infrastructure-as-Code and you don't need to support changing it on the fly then carry on passing stacks/constructs/CFN Exports around.

If your resources need to be loosely coupled, consider using Parameter Store to act as the bring and break the hard dependency.

Any questions, feel free to hit me on Twitter!

[dynamic-references]: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/dynamic-references.html#dynamic-references-ssm
[cdk-ssm]: https://docs.aws.amazon.com/cdk/latest/guide/get_ssm_value.html
[cdk-xzibit-meme]: https://i.imgflip.com/51ze1g.jpg
[cdk-wrap-api]: https://docs.aws.amazon.com/cdk/api/latest/docs/@aws-cdk_custom-resources.AwsCustomResource.html