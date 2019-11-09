---
layout: post
title: 09/11's Cloud Landing  ☁
tags: aws, aws-updates
---

Good morning! Welcome to the eigth post in the series that has a name; _Clouds At LHR_. You can also sign up for the newsletter on Tiny Letter; [https://tinyletter.com/CloudsAtLHR](https://tinyletter.com/CloudsAtLHR), or look at the embed form at the bottom of this post. As always you can send feedback to [@JakeHendy on Twitter](https://twitter.com/JakeHendy) or through any other means you have!

It's been a busy week for Amazon (and me, sorry!) so we've got (!) 22 updates available for you from the past 5 days, some big, some small. We've got a whole range of updates, from new instance types to improvements for _your_ customers to wider networking support to support for SQL Server 2019 and oh SO much more.

I'd also like to say a thankyou to Michael Brunton-Spall for his shoutout in [CyberWeekly](https://tinyletter.com/CyberWekly),it's a privilege to be able to work in the Civil Service amongst fantastic colleagues such as Michael and recently-crowned-Hero Matt Lewis, and so so so many others!

If you didn't have something to hand whilst you read this, this is your last chance, because it's a long one and you'll need it!

## Feature and Service updates

The latest feature and service updates that are either juicy, in Ireland or London, or all 3/4!

### Manage your Amazon API Gateway Service Quotas

No longer will you be forcecd to read the documentation for API Gateway, you can now view them all in the Service Quotas dashboard _and_ raise the requests from there. _Very helpful_, and available in London and Ireland!

### New C5d Instance Types

The C5 instance family features custom Intel Xeon Scalable processors, with a single-core max-frequency of 3.9GHz and an all-core boost up to 3.6GHz, these processors are great for when those numbers _need_ crunching and the machine learning needs its homework done; no small thanks to the additional AVX-512 VNNI instructions.
If that wasn't enough, the C5d instance family adds NVMe storage attached straight to the host meaning it's attached straight to your instances.
And if _that_ wasn't enough and you wanted more bang from your instances, the new `12xlarge`, `24xlarge`, and `metal` types will be of interest to you.
The `12xlarge` gives you 48 vCPUs, 96GiB of RAM, two 900GiB NVMe SSDs, and an up to 12 Gigabit network connection.
The `24xlarge` almost exactly doubles that with 96 vCPUs, 192GiB of RAM, four 900GiB NVMe SSDs, and an up to 25 Gigabit network connection.
If you need direct access to the host and memory too, the `metal` option gives you that flexibity with the same specs as the `24xlarge`.
Available in London and Ireland today!

### Single-click update setup for AWS Systems Manager Agents

One click in the console and every agent you have installed on your EC2s, on your on-premise servers, and your Virtual Machines will automatically update to the latest AWS Systems Manager agent as and when it's released.
The [Automate Updates](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent-automatic-updates.html) documentation page will give you more information, but it's one way to make sure you, your ops team, and your development teams can always take advantage of the latest offerings from AWS Systems Manager.

### PostgreSQL 12.0 available in the RDS Preview Environment

Just over a month after PostgreSQL 12.0 went GA, it's now available for any AWS customer to use in the [RDS Preview Environment](https://aws.amazon.com/rds/databasepreview/)! It'll be deleted after 60 days, supports T2/3, M4/5, and R4/5 instances.
Only available in Ohio (`us-east-2`) but if you can deploy in London or Ireland, you can deploy in Ohio too right? 😉

### Elastic File System now supports a 7-day lifecycle management policy

Move your EFS files to Infrequent Access within 7 days now, in addition to the 14, 30, 60, or 90 days you could previously.
Available in both London and Ireland!

### CodeBuild supports Secret Manager

Pass credentials to AWS CodeBuild jobs via Secrets Manager now; via your buildspec or an environment variables.
_Editor's note, you could previously use Paramater Store, Secrets Manager is a fantastic and long overdue addition!_

### EMR announces one-click access to persistent Spark History Server

Log directly in to the off-cluster Spark History Server (an extension of the Spark Web UI) to better [debug and monitor](https://docs.aws.amazon.com/emr/latest/ManagementGuide/app-history-spark-UI.html) your applications via the AWS Console.
The Spark History Server, as well as event and container logs, are persisted outside of the cluster and its lifecycle so you can investigate both running and terminated clusters.
Spark History Server is available with EMR version 5.25 in both London and Ireland!

### Comprehend supports an additional six languages

Comprehend now supports Chinese (Traditional and Simplified), Korean, Hindi, Japanese, and Arabic. Comprehend helps by using machine learning to find insights and relationships in written text.
Available in London and Ireland!

### Savings Plans

There's a blog post below which we'll go over.
Savings Plans are similar to Reserved Instances, they allow you to "save up to 72%" on EC2 and Fargate costs in exchange for comitting to spending a certain amount for 1 or 3 years. The difference is that your commitment is based upon pricing (e.g. $10 an hour) rather than a specific instance type/family.

They're available in all regions outside of China, and we'll dive deeper in to them in that blog post.

### Pinpoint adds _Journeys_

Journeys are "fully automated, multi-step engagement programs" for your customers.
Journeys can involve emailing users on that journey, identifying actions such as clicking on links in emails or notifications and waiting. You can create Journeys through the console or the API, so you can enable your marketing teams to create highly effective journeys for your customers.
Journeys are available in Ireland, and I expect if Pinpoint comes to London so will Journeys.

### Step Functions Data Science SDK for SageMaker

Freshly released, the Data Science SDK comes in the form of a Python library and is supported in Jupyter Notebooks.
The SDK allows developers and data scientists to easily create workflows spanning pre-processing, modelling, machine learning, and post-processing of data. You can integrate with Glue, Lambda, as well as SageMaker, to orchestrate huge amounts of infrastructure.
When you want to promote a workflow (pipeline) to production the SDK can export CloudFormation to launch it in to your production environment.

The SDK is free-to-use, [get started with the Hello World notebook](https://github.com/awslabs/amazon-sagemaker-examples/blob/master/step-functions-data-science-sdk/hello_world_workflow/hello_world_workflow.ipynb) available on GitHub.

### Redshift supports changing table sort keys online

Avoid recreating your tables because you need to change the sort key, thanks to Redshift 1.0.10654.
Redshift now supports adding and changing the sort keys on the fly, enabling your query patterns to evolve and respond to changing business requirements without having to recreate the tables in question.

### RDS for Oracle supports Oracle Database 19c

Oracle Database 19c is a long-term-support release for Oracle Database 12.2, supported until 2023 for Premier Support and 2026 for Extended Support customers.
You'll want to target `Oracle 19.0.0.0.ru-2019-07.rur-2019-07.r1` as the engine version, because you know naming things is hard.

### Code Suite supports SNS notifications

CodeCommit, CodeBuild, CodeDeploy, and CodePipeline now support SNS notifications for status updates and events, including links to those individual resources. You're not charged for the notifications themselves but are charged for the SNS topic and other associated resources.

### Automated Draining for Kubernetes Nodes on Spot Instances

Saving up to 90% is great when using spot instances but handling the two-minute-warning that your spot instance is about to be no more is troublesome. Step in the AWS [Node Termination Handler](https://github.com/aws/aws-node-termination-handler), which connects the AWS Termination Notifications to the Kubernetes control plane, which in turn will handle cordoning and draining of the affected instances.
Alongside running in production, the Node Termination Handler project allows you to simulate termination requests on your infrastructure.

Supported for home-grown k8s clusters and EKS!

### QuickSight enhances the mobile experience

The iOS app has received a significant upgrade, and a new Android app has been launched.
You can securely get insights on your data from anywhere you have a connection to AWS:(quoting the news release)
> browse, favorite, and interact with your dashboards; explore your data with drilldowns and filters; stay ahead of the curve via forecasting; get email alerts when unexpected changes happen in your data; and share those insights with colleagues.

There's an accompanying blog post for the app release, which we will cover below.
Available in London and Ireland.

### QuickSight supports Cross-Source joins

This was in the same announcement as the mobile app, but it deserves to be its own announcement.
You can wire up multiple data sources and join those sources together in one dataset; so you can pull in customer data from CRM tools like Salesforce, access logs from ELB, and order data from DynamoDB to create one powerful dashboard.

### App Mesh supports HTTP/2 and gRPC

As the title says, App Mesh supports traffic over HTTP/2 and gRPC between services in the mesh.
This includes App Mesh itself; collectings logs and metrics, health checks, traffic routing and retries.

Available in London and Ireland!

### RDS for PostgreSQL snapshots support upgrading snapshots

Snapshots used to be tied to a specific version of PostgreSQL and are immutable, so if you wanted to restore an unsupported version you were out of luck.
You can use this feature to additionally perform multiple major version upgrades and then restore them to a supported version, greatly reducing the time required to upgrade to later versions.

### Batch now supports GPU scheduling on G instance series

Batch supports scheduling GPU workloads on the GPUs in the G3, G3s, and G4 instance families in addition to the P2 and P3 instance families.
Batch supports scheduling tasks based upon GPU requirements; the type of and number of accelerators your batch jobs require. Batch will maintain the scaling group to maintian the required number of accelerators, and isolates the accelerators to ensure they're only available by the required containers.

### CloudWatch announces cross-account, cross-region dashboards

Can I just say _FINALLY 🎉_.
Enable the cross-account data publication in each account, and CloudWatch will aggregate them in the receiving ("central") account when you enable the cross-account, cross-region view.
You can then create dashboards that allow you to view resources across all your regions and then drill down in to specific views and other dashboards as appropriate.
Some of the main benefits here are reducing fatigue from your teams; maintaining multiple dashboards/sessions, concentrating everything on to one monitor and web session, and allowing teams to better concentrate their data from one account.

Next up, publishing dashboards URLs so I don't have to sign in with a Console account to put it on the TV...

### EC2 Supports SQL Server 2019

In all AWS regions you can now run Windows Server 2016/2019 AMIs with SQL Server 2019 Web, Express, Standard, and Enterprise editions pre-licenced.
In this announcement AWS finish by highlighting AWS Systems Manager as a recommended tool for migrating from 2008/2008 R2 workloads.
There's a dig at Windows too where they recommend the [SQL Server Re-platforming assistant](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/replatform-sql-server.html) for "customers looking to modernize their SQL Server workloads from a Windows to Linux operating system and save on Windows licensing costs"; no need to be catty AWS...

## News and blogs

We have a new region in the works, as well as some expansion on the features released above.

### [AWS in Spain](https://aws.amazon.com/blogs/aws/cross-account-cross-region-dashboards-with-amazon-cloudwatch/)

Coming late 2022 or early 2023, Madrid will be the seventh region after Milan opens in 2020.
Not much else has been mentioned, such as the number of AZs but one can imagine it'll be the standard 3 as services like Redshift were mentioned a lot at AWS developer engagements in Spain.

### [I need an [AWS] Hero](https://aws.amazon.com/blogs/aws/meet-the-newest-aws-heroes-including-the-first-data-heroes/)

Disappointingly for Shrek fans this blog is actually titled "Meet the newest AWS Heroes".
Regardless, there's a group of fantastic people here who you should follow and take note of, as they're some of the most knowledgable around!

### [AWS Savings Plans](https://aws.amazon.com/blogs/aws/new-savings-plans-for-aws-compute-services/)

Savings Plans are interesting, in that they're applied for Fargate and EC2 and are based upon committing to spending so much on compute.
You're able to look in Cost Explorer to see where you could take advantage of Savings Plan with recommendations and then purchase a Savings Plan; which wasn't explained in the release...
Twitterverse of course discovered some [interesting financial quirks](https://twitter.com/cperciva/status/1192606121690710016) when you take out a Savings Plan; whilst you can recover the tax (probably) I'm wondering if this is an oversight in the (one can imagine incredibly complex) finance systems.

### [QuickSight for Mobile](https://aws.amazon.com/blogs/big-data/announcing-the-new-mobile-app-for-amazon-quicksight/)

I don't know about you but I always want to crunch, filter and visualise 30TB of numbers on my personal device waiting for the bus. I facetiously jest, this is incredibly useful and highlights the capability of commodity services like QuickSight, where you can view all that data on the go.
I won't steal from the blog, it's worth looking into. It certainly reminded me that I could make use of QuickSight (not even QuickSight mobile) for some data visualisation...
It'll be interesting to see what the outcomes are!

## TinyLetter signup

<form style="border:1px solid #ccc;padding:3px;text-align:center;" action="https://tinyletter.com/CloudsAtLHR" method="post" target="popupwindow" onsubmit="window.open('https://tinyletter.com/CloudsAtLHR', 'popupwindow', 'scrollbars=yes,width=800,height=600');return true"><p><label for="tlemail">Enter your email address</label></p><p><input type="text" style="width:140px" name="email" id="tlemail" /></p><input type="hidden" value="1" name="embed"/><input type="submit" value="Subscribe" /><p><a href="https://tinyletter.com" target="_blank">powered by TinyLetter</a></p></form>
