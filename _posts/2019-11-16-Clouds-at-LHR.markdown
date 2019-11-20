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

Following on from enabling API subscriptions in API Marketplace, there's a new service for Data. Qualified (and that's important) providers can offer free and paid products on Marketplace, as well as off-contract products which can be managed separately.
Providers are able to require approval for subscriptions to maintain compliance and review use cases. Providers can receive daily, weekly, and monthly reports on the products and subscribers' activity.

Consumers can use the API or Console to load data directly in to S3. When a new "revision" of data is made available from a provider, a CloudWatch Event fires enabling the consumer to perform a variety of actions.
Billing is managed as a line-item on your existing invoice or you can bring external contracts in with the provider.

If you're in the AWS ecosystem this is perfect and allows you to a great amount of flexibility for data ingestion, although I'll be curious to see how the community integrates this with other cloud providers/ecosystems.

Available in London and Ireland!

### Configure table settings from DynamoDB Restore

When restoring a DynamoDB table you can opt to exclude some/all of the local/global secondary indices from being created with the restored table. Opting to exclude these indices can significantly decrease the time it takes for you to import those tables.

You can also change the capacity settings and billing configuraton for the table on import, enabling you to cost-optimise upon restore.

### Easily deploy SQL Server Always On solutions with a new wizard

AWS Launch Wizard for SQL Server enables you to configure a full SQL Server Always On Availability Group, instead of manually configuring the individual resources. You "simply" input your SQL Server requirements from performance to connectivity and the wizard will identify the right resources. Finally the wizard gives you an estimade cost for the AG, and allows you to tweak a few settings before you finally push through.
One of the best features is that it creates the CloudFormation templates for you to re-use and adjust; so you can avoid all the manual template writing. 

If you're trying to run a SQL Server Availability Group on AWS you _probably_ have some experience so you'll be more than happy to hack around with these templates. If you don't have experience, this is a pretty solid way to start. Win-win right?

Available in London and Ireland!

### AWS CodePipeline Enables Passing Variables between Actions

_Finally_ you can pass variables from one action to another in a pipeline.
These variables are evaluated at execution time, so you can export a URL from a build job and run tests against it in a later action, or use a Lambda to output variables.

Fantastic. Finally. Avaialble in London and Ireland!

### Automate your operational playbooks with Systems Manager

Add Python or PowerShell scripts to your existing playbooks, add wiki-documentation, and bring Systems Manager centre-stage of your operational play.

If you're not used to writing the JSON/YAML required for Automation then the custom playbook, there's a playbook builder which you can use to learn how it all fits together.
_Editor's note: I think I'm going to use this to help out our central support team during quick out-of-hours triage_.

Available in London and Ireland!

### GitHub Actions for Elastic Container Services!

There are [four actions](https://github.com/aws-actions) available so far:

* Configure AWS Credentials
* Log in to ECR
* Render a task definition (aka put a container image in to a task definition)
* Deploy a task definition to an ECS Service

What's more, is there is an GitHub Organisation open for these AWS Actons already so I'm hopeful there are more  actions in the pipeline (sorry), and the fantastic [Clare Liguori](https://github.com/clareliguori) is currently behind the four so they're definitely worth taking a look.

What little I've used of GitHub actions I love it, and am looking forward to using these within our GitHub Actions pipeline.
There's inbuilt support for secrets with GitHub actions so it's ready to go!
We've got a blog post below which we'll cover, which you should definitely check out.

### Redshift launches cross-instance restore

A recurring theme with AWS is you can't restore to something that isn't exactly like what you backed up from. For Redshift, that's no longer the case; you can restore to different sizes or different node types in either direction. The examples given are beefing up a restore of production data for heavy analysis, or downsizing for a development cluster based upon production data.

Available in all Redshift regions running `1.0.10013` or higher!

### SNS supports Dead-Letter Queues

If SNS was unable to deliver a notification to a subscription enpdoint, SNS will now post a message to an SQS queue for you.
Alongside the SNS -> SQS integration, you can receive a CloudWatch Alarm for when something has moved in to the Dead Letter Queue, _and_ there are logs to help you troubleshoot the message failure.

You could also set up a DLQ for when your SNS DLQ needs a DLQ. There'll be a blog post below with less snark for you to peruse!

Available in London, Ireland, and every other commercial region!

### WorkSpaces Directory APIs


### Export GuardDuty Findings to an S3 Bucket



## Blog Posts

### [Aaaand ACTION](https://aws.amazon.com/blogs/opensource/github-actions-aws-fargate/)

### [Dead Letter Queues](https://aws.amazon.com/blogs/compute/designing-durable-serverless-apps-with-dlqs-for-amazon-sns-amazon-sqs-aws-lambda/)
