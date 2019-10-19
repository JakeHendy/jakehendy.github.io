---
layout: post
title: 19/10's Cloud Landing  ☁
tags: aws, aws-updates
---

Good morning! Welcome to the fourth post in the series that has a name; _Clouds At LHR_. You can also sign up for the newsletter on Tiny Letter; https://tinyletter.com/CloudsAtLHR, or look at the embed form at the bottom of this post. As always you can send feedback to [@JakeHendy on Twitter](https://twitter.com/JakeHendy) or through any other means you have!

What's this, an update on a _Saturday_?!
I'll be honest I didn't get around to doing it yesterday, so now we can all enjoy both Thursday and Friday night's releases.
Additionally if you're reading this on Saturday you should also check out [CyberWeekly](https://tinylettter.com/CyberWeekly) for an interesting weekly round up of Cyber Security news, straight to your inbox!

# Feature and Service updates


## IoT Greengrass now provides deployment notifications to EventBridge

Whenever a Greengrass group deployment changes state, Greengrass will send a notification to EventBridge.

For instance, you can trigger a lambda which takes Corrective Action if a deployment goes bad whether it's restarting the deployment or involving a human. This is available out of the box with no changes required, take a look at the [EventBridge documentation](https://docs.aws.amazon.com/eventbridge/index.html) to find out more!

As a summary: EventBridge builds upon CloudWatch Events and enables you to act and respond to a variety events from both AWS Services and SaaS products. EventBridge is available in both Ireland and London.

## EC2 Hibernation is now available on Windows AMIs

Newly launched instances running an AMI of Windows Server 2012, 2012 R2, 2016, or 2019 nopw supprt EC2 Hibernation.
The instance must be a member of the M{3, 4, 5}, C{3, 4, 5}, or R{3, 4, 5} family and have no more than 16GB of RAM.
Instances that are running Amazon Linux (1 or 2) or Ubuntu 18.04 support hibernation on instances with up to 150GB of RAM.
I'm not sure where these limitations originate from, but if hibernation would help out your workloads this is available in Ireland and London!

## CloudWatch Anomaly Detection is now available in all commercial AWS Regions

Anomaly Detection uses Machine Learning to continually analyse your metrics, determining a baseline and then raising alarms when something appears out of the ordinary.
Anomaly Detection can be applied to both custom and AWS-vendored metrics, enabling you to easily highlight potential issues and alert on them with your standard practices.
The pricing for Anomaly Detection is decent, at first glance at least. $0.30 per alarm per month, against standard resolution metrics. You'll see this as three standard-resolution alarms on your bill: one for the lower bound, one for the evaluated metric, and one for the upper bound.
Available today through the console, API, CLI, and CloudFormation!

There's an accompany [blog post](https://aws.amazon.com/blogs/aws/new-amazon-cloudwatch-anomaly-detection/) out, check below!

## Attach EFS filesystems straight in the EC2 Launch Wizard

You can attach EFS filesystems straight away in the EC2 Launch Wizard. You can also create a new EFS file system from the wizard as well, enabling you to quickly prototype using EFS for your scenarios.
EFS and thus this feature is available in both London and Ireland!

## Amazon Lex achieves PCI DSS Compliance

If you work in the payment handling space you know this is mighty! Amazon Lex can now capture, transmit, and receive sensitive payment card data.  
You can now use the same conversational engine that Alexa uses (for both voice and text) to engage with your users and receive payment information.

Lex is only available in Ireland, but fingers crossed it'll come to London soon!

## CloudWatch alarms integrate with EventBridge

CloudWatch alarms now send state change notifications to EventBridge. A second event is raised in EventBridge to match that of your CloudWatch Alarm, allowing you to build new functionality to complement/succeed your existing alarm actions.
As Alarms only supported emails/SNS topics this will now allow you to trigger Lambda functions, Step Functions, System Manager automation documents and more without convuluted setup.

## SNS supports additional headers for mobile push

The number of headers available to structure your push notifications has expanded.
Take a look at the [list of reserved headers](https://docs.aws.amazon.com/sns/latest/dg/sns-message-attributes.html#sns-attrib-mobile-reserved) you can use to see if you can enrich your headers.
These reserved attributes are avialable in Ireland but not London.

## IoT Things Graph now integrates with CloudWatch metrics

You can now monitor your IoT Things Graph workflows using CloudWatch metrics. Metrics sent include _Success Count_, _Failure Count_, and _Total Count_, enabling you to set alarms (and associated EventBridge notifications!) to trigger actions based on those metrics.
Things Graph is a drag-and-drop interface to build IoT apps enabling you to connect and coordinate your devices. When you're ready to deploy, Things Graph will handle the mesasage building/translation enabling your services to all work together. 

# News Releases

This new feature comes straight from the blog or Twitter.

## CloudWatch Anomaly Detection

[CloudWatch Anomaly Detection](https://aws.amazon.com/blogs/aws/new-amazon-cloudwatch-anomaly-detection/) has gone live and it expands the number of services on AWS assisted by Machine Learning.
In this blog post the one-and-only Jeff Barr will walk you through setting up an example Anomaly Detection alarm, including the showing the one-click toggle to show when it would kick in.

Anomaly Detection builds upon over 12,000 internal models apparently.
I'll be curious to see how this works with our services at the Met Office, where traffic patterns are notoriously spikey. An extremely basic example would be to alert our Ops (either central Ops or DevOps) team to higher-than-usual traffic.
We could build on this to then adjust Application Auto Scaling based on the scale of the anomaly; perhaps leaving it alone for a 2x increase, or dialing it up to eleven if it's a 6x increase.

# TinyLetter signup

<form style="border:1px solid #ccc;padding:3px;text-align:center;" action="https://tinyletter.com/CloudsAtLHR" method="post" target="popupwindow" onsubmit="window.open('https://tinyletter.com/CloudsAtLHR', 'popupwindow', 'scrollbars=yes,width=800,height=600');return true"><p><label for="tlemail">Enter your email address</label></p><p><input type="text" style="width:140px" name="email" id="tlemail" /></p><input type="hidden" value="1" name="embed"/><input type="submit" value="Subscribe" /><p><a href="https://tinyletter.com" target="_blank">powered by TinyLetter</a></p></form>
