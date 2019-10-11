---
layout: post
title: 11/10's Cloud Landing  ☁
tags: aws, aws-updates
---

Good morning! Welcome to the first post in the series that has a name; _Clouds At LHR_. You can also sign up for the newsletter on Tiny Letter; https://tinyletter.com/CloudsAtLHR, or look at the embed form at the bottom of this post.

I was worried my first post here would be one or two releases from Amazon, but no! 

# RDS enables detailed backup storage billing
You'll now see individual line items for each backup from October 8th. After tagging your RDS DB instances you can separate the backup charges in Cost Explorer. Backups prior to 8th October remain under one line item.
Enabled for MySQL, MariaDB, PostgreSQL, Oracle, and SQL Server. 
There's even a [blog post](https://aws.amazon.com/blogs/database/amazon-rds-now-supports-detailed-backup-storage-billing/) available to help you get started; of which you can also take the same ideas to tag up other resources and view more indepth information in Cost Explorer. 

# ECS adds support for G4 instance types
I have a feeling I missed this one yesterday but! With the previous [launch of the G4 instance family](https://jakehendy.com/2019/09/23/AWS-Updates/#new-g4-instance-family-launched) you can now add them to your ECS for EC2 clusters where G4 instances are available. 
Run Amazon ECS GPU-optimised AMI Version 20190913 or higher to get started!

# Amazon Lex supports Checkpoints in Session APIs
This is really cool if you're working on chatbots. During a chat session you can mark a specific point in the conversation as a checkpoint, and Lex will remember that point allowing you to return to a point after a digression, maintaining dialog state, slot values, and all.
This feature is available in the SDKs with the `PutSession` API, and it's available in Ireland as well!

# Amazon Inspector adds benchmark support for Windows 2016
Amazon Inspector has expanded its Center for Internet Security's CIS Benchmarks for Windows 2016, allowing Inspector to verify your EC2 instances against the security best practices. 
Available in Ireland and London!

# Amazon Textract is now a HIPAA Eligible service
Whilst this is primarily US focussed it does demonstrate that Textract is aware of private information. To take advantage of the HIPAA protection (one assumes) you'll need a HIPAA Business Associate Addendum, which doesn't make it completely private. 

# SageMaker Ground Truth adds built-in workflows for verification and adjustment of data labels
What a title. 
Chain your Ground Truth labelling job in to a verification or adjustment job to start using the built in workflows to audit the accuracy of those labels. These features are supported for bounding boxes and semantic segmentation labels.
There's a [blog post](https://aws.amazon.com/blogs/machine-learning/verifying-and-adjusting-your-data-labels-to-create-higher-quality-training-datasets-with-amazon-sagemaker-ground-truth/) that has more information...
Available everywhere Ground Truth is!


# ECS now supports Image SHA Tracking 
Correlate container images pulled from ECR with scheduled tasks and where it's running, either on EC2 or Fargate. There's an immutable attribute to identify where your image has been deployed to track application adoption, incident repsonse, and lifecycle management. 
ECS implements this by using task state change events emitted to CloudWatch Events, and is fully integrated between ECR, ECS, Fargate, and CloudWatch Events. You can use this for exmaple to track patch auditing on your containerised applications.  
Update your ECS agent if you're running on EC2; Fargate and new ECS instances based on the Amazon Linux AMI already support this capability.
Available everywhere you can run ECS (everywhere?).

# AWS Console Mobile iOS app supports federated login
If you use federated login for your AWS accounts you can now use the iOS app to manage the select set of resources, enabling incident response whilst on the go. You can lever biometrics authentication to make access to AWS "resources a simple and quick", I'm assuming it's a simple and quick procedure :)

# Chatbot now supports notifications from AWS Config
Use your Slack/Chime integrations to receive notifications about Config rule compliance and config change reports. Simply configure an event rule for Config to publish to an SNS topic, and configure Chatbot to map that topic to a Slack channel or Chime chat room. 
Available everywhere that Chatbot is available!

# AWS Firewall Manager supports management of VPC Security Groups
I've never seen this before but Amazon now say a "security group acts as a virtual firewall". You can now use Firewall Manager to centrally manage a set of Security Groups across your whole organisation, ensuring consistency and security compliance. You can also use this to detect overly permissive or misconfigured rules.
Available everywhere that Firewall Manager is available!
_It's one tool in your arsenal, remember good security is about knowledge sharing as well as good tooling!_

# Glue can use custom certificates for JDBC connections. 
You can configure Glue to use custom certificates when using JDBC connections to your data sources, in both ETL jobs and Crawlers.
Available everywhere that Glue is available!


# TinyLetter signup

<form style="border:1px solid #ccc;padding:3px;text-align:center;" action="https://tinyletter.com/CloudsAtLHR" method="post" target="popupwindow" onsubmit="window.open('https://tinyletter.com/CloudsAtLHR', 'popupwindow', 'scrollbars=yes,width=800,height=600');return true"><p><label for="tlemail">Enter your email address</label></p><p><input type="text" style="width:140px" name="email" id="tlemail" /></p><input type="hidden" value="1" name="embed"/><input type="submit" value="Subscribe" /><p><a href="https://tinyletter.com" target="_blank">powered by TinyLetter</a></p></form>
         

