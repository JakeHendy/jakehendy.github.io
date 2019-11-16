---
layout: post
title: 12/11's Cloud Landing  ☁
tags: aws, aws-updates
---

Welcome to Clouds At LHR, where all the updates for Ireland and London and those full of fun come in to land.
We'll keep your the news young, drifted, and stacked in your inbox, and anyone else's so feel free to forward this on.
Sign up at [https://tinyletter.com/CloudsAtLHR](https://tinyletter.com/CloudsAtLHR), follow me and send feedback to [@JakeHendy on Twitter](https://twitter.com/JakeHendy)!

We've got ~2~, ~no 3~, ergh ~5~ days of updates for you; as AWS' update cycle seems to increase with the workload at my day job!
A few of us in the cross-gov community are hoping we can automate some of the aggregation (using AWS _of course_) so if you have any suggestions send them on through.



## Features and News Updates

Let's disect the news.

### QuickSight Launches Actions, UI based ingestion history, and oh so much more

Add one-click filtering of your dashboards through Actions.
Click on datapoints to view relevant information in other visuals, or even to external dashboards and services.
QuickSight Actions allows a great level of interactivity and I'm very excited to link this in; combine it with the ability to publish dashboards and you're able to harness the technical power of AWS for your marketing and analytics teams in a safe and auditable fashion.

Your SPICE datasets now have ingestion history available, including error codes for when dataset failures/initialisations failed.

If your dashboards and visualisations need right now, SPICE and Direct Query datasets support the `now()` function too!

Available in London and Ireland, for both Standard and Enterprise.

### Systems Manager Distributor enables in-place update of packages

Following on from the recent update which allowed the Systems Manager agent to self-update, your software packages can be updated instead of uninstall-old-then-reinstall-new.
Available in London and Ireland!

### Amazon Linux 2 AMI with .NET Core supports .NET Core 3.0

The preconfigured AL2 AMI now comes with .NET Core 3.0, Mono 5.18, PowerShell Core 6.2, and the AWS CLI.
As .NET Core 3.0 supports ARM64, you could in theory run your apps on the new `a` instance series!

### RDS for Oracle Z1d available in additional regions

You can launch RDS for Oracle on Z1d instances in London! Z1d instances have incredible compute performance and memory making it ideal for those extortionate per-core licensing costs. (AWS' words, not mine!)

### NoSQL Workbench for Amazon DynamoDB supports DynamoDB Local

I haven't had much time to play with the Workbench but if you're in an environment where connecting to AWS Is difficult you can at least use the Workbench with DynamoDB local now; which runs as a Java JAR on your local machine.

### IoT Device Management introduces new fleet-level metrics

As the title says, you can use the standard metrics (min, max, sum, average, standard deviation, variance, and sum of squares) across several metrics in your fleet; from battery life to temperature, as well as maintaining the individuality of the sensors and devices.

Available where IoT Device Management is offered!

### Cost Explorer supports hourly and resource level granularity

You can now track your costs at the hourly granularity for up to 14 days, as well as individual EC2 instances.

The charging model is interesting, it's $0.01 per 1,000 UsageRecords. A UsageRecord is one line of usage, so one EC2 running for a day would generate 24 hourly Usagerecords.

### Cloudwatch Metric Math support more functions

Sort 'em, slice 'em, remove empty, and conditially (`if`/`and`/`or`) mathematise your data.

For instance, you could take sort by EC2 CPU Utilisation, take the top 5, see if the AutoScalingGroup is at its maximum, and then trigger an alarm using an SNS Topic or CloudWatch Events.
Another example Amazon give is triggering autoscaling when either CPU or Memory are at a certain value.

### CloudFormation supports Resource Import

One of the biggest bugbearers of mine is when you need to refactor the CloudFormation that creates an S3 Bucket or DynamoDB table, or when something wasn't available through CloudFormation so it was created through the CLI.
Not a problem any more! You can import existing resources in to new stacks and existing stacks. You have to use the console or CLI to import them, and I'm excited to see how this plays out with the CDK.

Available in London and Ireland!

### CloudSearch supports mandating HTTPS and minimum TLS Version

CloudSearch is one of those services that you don't hear about very often, but you'll be pleased to know that it allows you mandate all traffic is submitted over HTTPS and the minimum TLS version is required.

Available in Ireland!

### Transcribe supports speech-to-text in 8 additional languages

Irish English, Scottish English, Welsh English, Dutch, Frasi, Indonesian, Portuguese, and Tamil langauges are now supported for text-to-speech with Amazon Transcribe.

Available in London and Ireland!

### Data Lifecycle Manager supports adding tags to lifecycle policy

Tag up your Data Lifecycle policies to help categorise and organise those policies of yours.

### RDS Performance Insights supports counter metrics for SQL Server

RDS Performance Insights supports counter metrics; enabling you to customise the dashboard to include up to 10 additional graphs showing a selection of both operating system and database performance metrics.

### ElastiCache supports T3 Standard cache nodes

Upgrade cache nodes from T2 to T3 to gain some performance improvements and price reductions.
You could even use multiple caches/cache nodes instead of one large r5 group to better isolate your data and save money.
Perfect for baseline loads as well as those that might have small spikes in usage.

### AWS Data Exchange




## Blog Posts


