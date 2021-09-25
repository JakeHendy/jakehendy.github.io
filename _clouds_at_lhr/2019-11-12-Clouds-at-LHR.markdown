---
layout: single
title: 12/11's Cloud Landing  ☁
tags: aws, aws-updates
---

Good afternoon! Welcome to the ninth post in the series that has a name; _Clouds At LHR_. You can also sign up for the newsletter on Tiny Letter; [https://tinyletter.com/CloudsAtLHR](https://tinyletter.com/CloudsAtLHR), or look at the embed form at the bottom of this post. As always you can send feedback to [@JakeHendy on Twitter](https://twitter.com/JakeHendy) or through any other means you have!

Unsurprisingly there's no overall theme for today's update, we've got DynamoDB features, Single Sign-on features, Encryption, and Configuration Management. There's something for everyone in here though I'm sure!

## Feature and Service updates

The latest feature and service updates that are either juicy, in Ireland or London, or all 3/4!

### DynamoDB Accelerator (DAX) is available in London

If you wanted to use DAX in London now you can! DAX allows you to accelerate reads up to 10x, even when you're performing millions of requests per second (_how big is that bill_).
DAX is also relatively easy to drop in if you own the code that talks to DynamoDB, as you can add the DAX SDK and change some calls (cos it's always that easy...) and you'll use the accelerator.
Interestingly though, DAX is still only supported on the R4 and T2 instance families, and I'm not sure why!

### Use AWS CLI v2 with AWS SSO

Finally! If you use AWS CLI v2 you can now integrate your users with SSO directly.
With this direct integration comes support for named profiles (and Administrators can also enforce which profiles) as well as automatic credential short-lived credential rotation.
Another benefit of using SSO with short-lived credentials is that you never have to do any additional work for long-running operations; as you're renewed via SSO under the hood!

There's a companion blog post which we'll review below!

Available in Ireland and London now; and if you use SSO I'd love to hear from you and know how it works.

### CloudFormation updates for API Gateway, CodePipeline, and more

Some of these updates add support to CloudFormation for features/updates released within the past week, as well as increasing tagging support for some services.

You can now add tags to:

* custom actions and pipelines in CodePipeline
* API Keys, Rest APIs, Usage Plans, Domain Names, and Client Certificates in API Gateway
* a new topic in SNS.

On top of that you can:

*  specify whether AWS Amplify creates a [preview environment](https://jakehendy.com/2019/10/25/Clouds-at-LHR#amplify-console-supports-pull-request-previews) for your pull request branches and which backend environment to use for those previews
* Configure slow publishing for Amazon ElasticSearch Service with the `LogPublishingOptions` property
* Configure gRPC Routes in App Mesh; including route actions, route matches, route metadata, the route metadata match method (!), and the retry policy
* allow usernames to be emails and passwords, add or update schema attributes, and set an alias for the User Pool in Cognito
* create message templates for email, push notification, or SMS in Amazon Pinpoint.

Tasty!

### Encryption SDK (ESDK) for JavaScript is now Generally Available

This is the "first time client-side encryption is supported natively in the browser" according to the release.
[The ESDK](https://github.com/aws/aws-encryption-sdk-javascript/) is designed to allow you to use industry best practice and proven libraries to secure content in browser at the edge of the cloud, and has sibling libraries in the C, Java, Python, and the command line.
As the algorithms are compatible between all the libraries, providing you maintain access to the keys, you can securely encrypt content from device to server all the way through!

### Config supports AWS Key Management Service and Amazon ElasticSearch Service

Record all the changes made to configuration for KMS and Amazon ES now with Config!
For KMS, Config can record changes to the metadata and configuration attributes.
For ES, Config can track instance type changes, encryption settings, network configuration, and the access policies.

These are supported in both a perma-log fashion as well as triggering checks on change to ensure compliance with internal/customer-focussed policies.

## News and blogs

We're highlighting one of the developer blogs today.

### [AWS CLI v2 supports SSO](https://aws.amazon.com/blogs/developer/aws-cli-v2-now-supports-aws-single-sign-on/)

The blog post walks through a simple setup of a local user session with SSO and issuing a sample command with CLI v2.
The tailend of the blog post mentions that you will be logged out again though at some point, and you have to `aws2 sso login` agian, which I find rather strange and counter-intuitive against the news releases announcements (for some version of long-running operation).
I guess it depends on your SSO mechanism, if you were using AD/AzureAD I would expect it to use the machine tokens to re-auth behind the scenes. This is a developer preview however, so one could reasonably send feedback and contribute back otherwise...

## TinyLetter signup

<form style="border:1px solid #ccc;padding:3px;text-align:center;" action="https://tinyletter.com/CloudsAtLHR" method="post" target="popupwindow" onsubmit="window.open('https://tinyletter.com/CloudsAtLHR', 'popupwindow', 'scrollbars=yes,width=800,height=600');return true"><p><label for="tlemail">Enter your email address</label></p><p><input type="text" style="width:140px" name="email" id="tlemail" /></p><input type="hidden" value="1" name="embed"/><input type="submit" value="Subscribe" /><p><a href="https://tinyletter.com" target="_blank">powered by TinyLetter</a></p></form>
