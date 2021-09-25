---
layout: single
title: 06/02's Cloud Landing  ☁
tags: aws, aws-updates
---

Good morning good morning. Following on from yesterday's post it seems there are indeed a number of updates rolling out the door. Clouds@LHR will filter out the crud (ew MySQL!) so keep your eyes on the blog. You can also sign up for the newsletter on Tiny Letter; [https://tinyletter.com/CloudsAtLHR](https://tinyletter.com/CloudsAtLHR), or look at the embed form at the bottom of this post. As always you can send feedback to [@JakeHendy on Twitter](https://twitter.com/JakeHendy) or through any other means you have! Perhaps through the [online form](https://forms.office.com/Pages/ResponsePage.aspx?id=DQSIkWdsW0yxEjajBLZtrQAAAAAAAAAAAAMAALQXYjNUMDYyQ0o0MEkyUVIxUFdWNzhSVlZFVVBPUC4u)...

## Feature and Service updates

We've got 6 updates to discuss today, from features for end-users and sysadmins to helping your auditing and monitoring requirements.

### Introducing the Desktop Client for AWS Client VPN

Following on from the AWS EC2 VPN, AWS have released a desktop client that can be rolled out to end-user devices for more seamless integration with that VPN for Windows and Mac clients.
One of the selling points of this package is that you can use AWS services end-to-end, whether you "trust" them more against Cisco AnyConnect is an exercie for the implementor. Cost will be another factor if you want to run connections back to your offie via VPC VPNs/DirectConnect, but if you just want a VPN to your VPCs and no further you're probably going to reap the rewards very quickly.
The other question of course is, do you need the desktop client if you're running a recent version of Windows and macOS? Will lifting the client up the stack out of the OS give you benefits? Definitely one to watch!

### Amazon Cognito User Pools APIs integrated with CloudTrail

All of the [User Pool Action APIs](https://docs.aws.amazon.com/cognito-user-identity-pools/latest/APIReference/API_Operations.html) are now logged in CloudTrail, by any admin. CloudTrail is wonderful in that you can't change it _and_ it is an event source for EventBridge etc. So perhaps when a user's MFA is added/updated/removed you can fire a lambda to add/remove access to services etcetera.
This is of course secondary to the fact that every action in Cognito User Pools is now audited and logged!

### AWS Ground Station Cross Region Data Delivery

Previously you had to run your own solution if you wanted to move data from a Ground Station region (a US one) to any other region; which in turn has cost implications of moving that data through the AWS backbone. You could have negotiated a nice savings package with AWS (because if you're using satellites you probably have Enterprise Support, _right?_) but now Ground Station will do the heavy lifting of moving data to _your_ region for _free_. You still only pay for the time your antenna link is active!
Available for Ground Stations in `us-east-2` (Ohio) and `us-west-2` (Oregon).

### Amazon VPC Flow Logs Now Support 1-minute Aggregation Intervals

If you want to analyse your VPCs just that little bit quicker, now you can! VPC Flow Logs support delivery in max-1-minute intervals at no additional cost. The knock-on effects of this are that you can flatten your compute requirements (i.e. you don't have large processing spikes) as well as identifying issues earlier.

Available everywhere!

### Rerun Commands with AWS Systems Manager Run Command

There's two small-but-big-impact quality-of-life improvements here for Run Command, exact re-run and copy-and-modify.
Given you've already executed one command manually you might want to do it again, but to save yourself the copy-paste and configuration setup, you can now push a "rerun" button and AWS will do all of that for you. Useful for those one-off investigations etcetera.
Copy-and-modify allows you to copy a command exactly and then tweak it like a new command, which you could then run repeatedly as you need to.
Useful for when you're developing your automation, as well as incident (beit security or otherwise) investigtion!

Available everywhere you have AWS Systems Manager Run Command.

### AWS Security Hub adds more resource integrations, increases limits, and adds a new field

The actual news release for this is a bit confusing. Security providers can now send security findings for 15 new resources (reproduced below), as well as attaching 32 (up from 10) resources to a single finding.

The understated new feature is the `Compliance.RelatedRequirements` field, where providers can tell you which regulatory controls a compliance finding relates to.

The new resources are:
> AwsCodeBuildProject, AwsEc2NetworkInterface, AwsEc2SecurityGroup, AwsElasticsearchDomain, AwsLambdaLayerVersion, AwsRdsDbInstance, and AwsWafWebAcl. These new resource types do not yet have details objects: AutoscalingAutoscalingGroup, AwsDynamoDbTable, AwsEc2Eip, AwsEc2Snapshot, AwsEc2Volume, AwsRdsDbSnapshot, AwsRedshiftCluster, and AwsS3Object

## News and blogs

No blogs today, I'll keep an eye out!

## TinyLetter signup

<form style="border:1px solid #ccc;padding:3px;text-align:center;" action="https://tinyletter.com/CloudsAtLHR" method="post" target="popupwindow" onsubmit="window.open('https://tinyletter.com/CloudsAtLHR', 'popupwindow', 'scrollbars=yes,width=800,height=600');return true"><p><label for="tlemail">Enter your email address</label></p><p><input type="text" style="width:140px" name="email" id="tlemail" /></p><input type="hidden" value="1" name="embed"/><input type="submit" value="Subscribe" /><p><a href="https://tinyletter.com" target="_blank">powered by TinyLetter</a></p></form>
