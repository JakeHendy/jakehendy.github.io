---
layout: post
title: 08/10's AWS Updates ☁
tags: aws, aws-updates
---

_A lookback of the past 24 hours of updates from AWS, applicable to my x-gov colleagues and I with the occasional interesting piece thrown in._

So I never got around to completing the post for yesterday for Reasons™, so we have a slightly larger update today!
There's another mixed bag of updates today, so let's drop in:

# New Quick Start to deploy Amazon Managed Blockchain
Interesting that there's a quick start to deploy a managed service, but having not read much in to Blockchain/Amazon's Managed Blockchain it seems like a great idea. The Quick Start will install the network, the first member, and its peer nodes within 15 minutes. Of course, Managed Blockchain is currently only available in US East (N. Virginia)/`us-east-1`, so it'll be a while before it's coming to Ireland or even London!

# Direct Connect announces support for Granular Cost Allocation and removal of Payer ID Restriction for a DC Gateway Association
There's not a lot to say here that isn't in the title!
Costs are now allocated to the AWS account that made the data transfer through a private/transit virtual interface, rather than the account that owns the virtual interface. The actual cost/GB doesn't change, and this change is being applied from October 1st—yes, retroactively.
Additionally, DC Gateway Associations had to be under the same payer ID as the VPCs/Transit Gateways, but now you can use any account under any payer ID.

# Queue Purchases of EC2 Reserved Instances
You can now queue your Reserved Instance (RIs) purchases ahead of time, allowing you to ensure uninterrupted coverage of your RIs and the cost savings involved. For example, schedule your yearly RIs to renew every year. If you then replatform/change instance family, you'll know you can cancel the request for the future/change the RI to your new instance family.

# Introducing `ml.p3dn.24xlarge`
SageMaker now has a mighty-large instance for your machine learning workloads. The `ml.p3dn.24xlarge` has 8 NVIDIA Tesla GPUs with NVLink, 256GB of _GPU_ Memory, 96 Skylake vCPUs (_remember the other p3s use Broadwell chips_), 768GB of RAM, up to 100Gbps of Network bandwidth, 14Gbps of EBS Bandwidth, _and_ two 900GB NVMe SSDs attached locally to the instance.
Available in N Virginia (`us-east-1`) and Oregon (`us-west-1`) regions, I can imagine there will be a few of these flying to Ireland soon. 

# AWS Backup Enhances SNS Notifications to filter on job status
AWS Backup will now filter your SNS notifications based on the status of your backup job, rather than you having to filter yourself.
Reminder! AWS Backup allows you to backup and restore EBS Volumes, RDS Databases, DynamoDB Tables, EFS File Systems, and Storage Gateway volumes.

# Pinpoint adds support for Message Templates
Create templates for email, push notifications, and SMS messages for all Pinpoint projects. Reduce risk and increase reuse by creating either static templates, or use the Handlebars templating language to create in-depth templates with variables and all. Push notifications can be further templated with channel-specific settings, including sounds and icons. 

# VPC Traffic Mirroring now supports AWS CloudFormation
As the title says, you can now configure traffic mirroring using AWS CFn. The CFn resources look quite comprehensive, allowing you to specify source/target instances and the ability to update them as well. Deploy these same session configurations against multiple AWS environments too!

# Managed Services Console now supports earch and usage-based filtering
Use keyword searching and filter results based on must recently or most frequently used. AWS Managed Services features a catalogue of over 30 AWS Services with over a hundred different Change Types to deploy or update resources in to your AMS environment. 

# App Stream now supports FIPS 140-2 compliant endpoints
In all US regions where App Stream is now available you can use FIPS 140-2 compliant endpoints, but you must configure the CLI/SSO relay URLs to do so. 

# Amazon EventBridge now supports AWS CloudFormation
EventBridge now supports AWS CloudFormation for creating and configuring EventBridge resoures!
EventBridge helps you analyse and process real-time data internally and externally from sources such as Zendesk, Datadog, and Pagerduty. These events can be routed to targets such as AWS Lambda. 
CFn support is available everywhere EventBridge is.

# New Solution Accelerators for IoT Greengrass
There are 2 new Solution Accelerators for IoT Greengrass, to help you with Extract, Transform, and Load (ETL) functions and running SageMaker models locally on edge devices, including inference on local data, while publishing those results to other Greengrass devices or AWS. 

# DirectConnect announces resiliency toolkit.
The Connection Wizard is now supported within the Resiliency Toolkit, helping you define which resiliency model you fall in to and how to proceed after that. There are 3 models available, "Maximum Resiliency" with 99.99% SLA if you meet the requirements; "High Resiliency" with 99.9% SLA if you meet the requirements; and "Development and Test" with no SLA but presumably cheaper. It's definitely worth reading [Resiliency Toolkit announcement](https://aws.amazon.com/about-aws/whats-new/2019/10/aws-direct-connect-announces-resiliency-toolkit-to-help-customers-order-resilient-connectivity-to-aws/) to get more detail.
This is available in all Commercial Regions, with China and GovCloud support coming soon. 

# Cognito has better CloudFormation support
You can now specify/configure the hosted UI domain, customise that hosted UI, configure your Identity Provider, and more within CloudFormation! Have a look at the [AWS Cognito CloudFormation reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_Cognito.html) for more!
