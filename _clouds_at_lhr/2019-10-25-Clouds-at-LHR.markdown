---
layout: single
title: 25/10's Cloud Landing  ☁
tags: aws, aws-updates
---

Good morning! Welcome to the fifth post in the series that has a name; _Clouds At LHR_. You can also sign up for the newsletter on Tiny Letter; [https://tinyletter.com/CloudsAtLHR](https://tinyletter.com/CloudsAtLHR), or look at the embed form at the bottom of this post. As always you can send feedback to [@JakeHendy on Twitter](https://twitter.com/JakeHendy) or through any other means you have!

It's been a busy couple of days in the office, with some minor updates coming out from AWS when it's been quiet and then some tasty ones the days we're busy. _It's almost like they know?!_

Today we have got 3 days worth of updates, from CI/CD improvements in Amplify to infrastructure-as-code improvements with OpsWorks to better managing how your AWS Batch workloads execute!

Grab your coffee/tea/cold-drink/snacks and let's dive straight in!

## Feature and Service updates

The latest feature and service updates that are either juicy, in Ireland or London, or all 3/4!

### OpsWorks for Chef now supports custom domain names

Specify a FQDN, an SSL certificate and matching private key, and complete an internal CNAME DNS record provisioning and away you go! Your OpsWorks for Chef will then expose a public Chef server on the URL you specify.
You can use this to ensure continuity of service when you (or OpsWorks) reprovision your Chef servers.
You cannot update an existing OpsWorks for Chef server however, so you'll need to use the Backup API and then the CreateServerAPI to recreate the service. Providing you have your certificate and key encoded in PEM format, you're good to go in 15 minutes!

### EFS now supports PrivateLink

EFS (the NFS filesystem) already uses TLS and of course you connect to it from within a VPC. This update means that the EFS _API_ is available over PrivateLink, so for managing your EFS file systems you can now do so without using the internet/public IP Addresses at all.

### Amplify Console supports Pull Request Previews

Amplify can now deploy a GitHub pull request to a unique URL, allowing your Dev/QA teams to easily preview future work before it is merged in. If you have a backend associated with your front-end app, Amplify will spin up a temporary backend which is deleted with the front-end when the PR is closed.

### AWS Glue can now rewind job bookmarks for Spark ETL jobs

If you use Glue you may find this one to be a life-saver. Glue tracks previously-processed data in ETL jobs by storing state information, otherwise known as a bookmark.
Resetting to a bookmark meant reprocessing all of the data processed by previous job runs, whereas now you can reprocess data only from that bookmark.

### New Classroom Course on Practical Data Science with SageMaker

_Practical Data Science with SageMaker_ is a new one day instructor-led course pitched at an intermediate level walking learners through a typical Machine Learning pipeline; from visualising data to building, training, and deploying the SageMaker model.
Available in public locations or private hire!

### Managed Blockchain supports CloudWatch for peer nodes

*BLOCKCHAIN*. Not only can you see CPU and memory utilisation of your peer nodes but transaction rate per node as well.
You can of course set Alarms and automate actions based upon those metrics and alarms...

### API Gateway supports wildcard custom domain names

Previously if you wanted to have one API Gateway but give out vanity or customer-specific URLs you would be disappointed and created a custom domain name for each usecase.
Now, now you can use one wildcard certificate, wildcard custom domain name, and provision `foo.api.bar.net`, `bing.api.bar.net`, `fizz.api.bar.net` and achieve simplified custom routing at lower cost. 
Providing you have AWS Certificate Manager (where doesn't?!) you can take advantage of this *magic* ✨.

### IoT Device Tester v2.1.0 now available for Greengrass
 
v2.1.0 supports Greengrass v1.9.4 and qualification of devices with ARM v6l arch. Qualify your devices for the Device Catalog or make sure they'll work with your investments on AWS!

### AWS Managed Services supports 29 more services, adds developer mode, managed Landing Zones

AWS Managed Serices (AMS) will run your account for you, looking after infrastructure day-to-day and providing cost-optimisations. Previously, to guarantee the security and compliance of these accounts, you couldn't use native API Access.  
Now, AMS accounts have enhanced IAM roles to enable you to quickly iterate and configure your services before handing them over to AMS. You're unable to remove the configurations required by AMS and there are guardrails to help protect you whilst doing so.

In addition to this 29 new services are supported by AMS, including AWS Lambda. For services which have lower day-to-day management requirements (such as Lambda), there's a reduced-price tier available for you too. Some of these more-managed services like Lambda can also be provisioned through the console!

If that wasn't enough for you, you can now have an AMS-manged AWS Landing Zone. The Landing Zone is a multi-account architecture designed for enterprises with suitable configuration off the bat. If you'd like to see what the AWS Landing Zone offers over the standard AMS Landing Zone, [check out the announcement](https://aws.amazon.com/about-aws/whats-new/2019/10/aws-managed-services-now-offers-managed-landing-zones/). _(And whip open your wallet!)_

To quote the update, these services have been added (in alphabetical order):

> AWS Certificate Manager, AWS CodeCommit, AWS CodeBuild, AWS CodeDeploy, AWS CodePipeline, AWS License Manager, AWS Snowball, AWS Well-Architected Tool, Amazon API Gateway, Amazon Athena, AWS CloudHSM, Amazon Comprehend, Amazon DocumentDB (with MongoDB compatibility), Amazon FSx, AWS Glue, Amazon Inspector, Amazon Kinesis Data Streams, Amazon Kinesis Video Streams, AWS Lambda, Amazon MQ, AWS Secrets Manager, AWS Security Hub, Amazon SimpleDB, AWS Step Functions, AWS Systems Manager Parameter Store, AWS Transit Gateway, AWS Web Application Firewall (WAF), Amazon WorkDocs, AWS X-Ray.

### Aurora supports storage cost allocation through tags

For both MySQL and PostgreSQL-compatible versions of Aurora, you can now assign tags to better categorise usage and achieve more granular cost reporting of various dimensions; from storage to I/O to backups and snapshots. 

### DocumentDB (compat with MongoDB) adds support for Change Streams

DocumentDB can now provide change streams; returning both the changed content as well as the full document. The stream is a time-ordered sequence of changes to collections and databases.
There are some limitations to the Change Stream feature in DocumentDB, from only being able to obtain change streams from the primary to losing changes after 2 hours to the stream being stalled from long-running write operations. 
Take a look at the [limitations](https://docs.aws.amazon.com/documentdb/latest/developerguide/change-streams.html#change-streams-limitations) to find out more!
Enabling change streams will incur extra I/O and Storage costs, in line with existing pricing models.

### Machine-to-Cloud Connectivity Framework supports SLMP

The Mitsubishi Seamless Messaging Protocol allows your machinery to communicate between applications without knowledge of the network hierarchy.
The Connectivity Framework solution deploys IoT Core and Greengrass, Lambda, DynamoDB, and S3 to enable you to prototype and deploy a secure communications platform on AWS for your machinery.

### AWS Batch supports now allocation strategies

Batch now supports optimising for throughput as well reducing spot interruption. Previously Batch attempted to achieve optimum cost when allocating jobs on the batch queue.
There's a [blog post](https://aws.amazon.com/blogs/compute/optimizing-for-cost-availability-and-throughput-by-selecting-your-aws-batch-allocation-strategy/) available which covers this in more detail, which we'll cover in more detail down below!

### GameLift supports Amazon Linux 2

You can not only take advantage of Amazon Linux 2 and the improvements it brings over AL 1, from more modern software versions and better performance on EC2, but you can now use the latest C5, M5, and R5 series of instances to not only improve performance but also lower cost!
_Winner winner chicken dinner_

## News Releases

This new feature comes straight from the blog or Twitter.

### [AWS Batch Allocation Strategy](https://aws.amazon.com/blogs/compute/optimizing-for-cost-availability-and-throughput-by-selecting-your-aws-batch-allocation-strategy/)

Following on from the news above, there's more information here on three strategies you can use now with AWS Batch.
To summarise, there's the original "Best Fit" which will pick from the instance families you specify, "Best Fit Progressive" that will look at other instance families and try to maintain the vCPU-to-memory ratio as well as delving in to spot capacity, and "Spot Capacity Optimised" which is perfect when you're running interruptible workloads.
_Best Fit_ seeems to be on the way out and has a radically reduced use-case, such as when you want to tightly control what instance family your workload runs on for cost purposes.

You can also use multiple compute environments with one job queue, where AWS Batch will pick the best compute environment for the job on the queue allowing you to burst over your minimum throughput. 

### [CloudFront now has its 200th Point of Presence](https://aws.amazon.com/blogs/aws/200-amazon-cloudfront-points-of-presence-price-reduction/)

CloudFront's 100th point of presence was launched in 2017, and they've just announced their 200th in South America.
If you don't have many customers in South America there isn't much for you in this blog post that is important day-to-day.
It does however have some other interesting facts, from high profile clients (the Royal Wedding, Commonwealth Games, 2019 FIFA Women's World Cup) to sustaining a 1.4Tbps memcached reflection attack. It's short, and worth a scan over for some talking points.

### [Amplify Pull Request Reviews and Cyprus Testing](https://aws.amazon.com/blogs/aws/improve-your-app-testing-with-amplify-consoles-pull-requests-previews-and-cypress-testing/)

I moved out of front-end development as my primary field a few years ago and the barrier to entry has seeminly risen in that time. The art of the possible has also immensely grown in that time, but the supporting work required for that has put me off dabbling in the field.
Until Amplify, it may not be the perfect use case but I'm impressed and intrigued by what Amplify offers. In this post Amplify offers first-party support for previewing GitHub pull requests (like how the GOV.UK Design System [deploys a netlify preview](https://github.com/alphagov/govuk-design-system/pull/1065#issuecomment-543161898)) on a dedicated Amplify preview environment.

In addition to previews to see your content there's also integration with the Cypress test framework as well, where Amplify will automatically detect your tests and adds a testing phase to your deployment pipeline.

One day, one day I'll pick up the JavaScript hat again... :) 

## TinyLetter signup

<form style="border:1px solid #ccc;padding:3px;text-align:center;" action="https://tinyletter.com/CloudsAtLHR" method="post" target="popupwindow" onsubmit="window.open('https://tinyletter.com/CloudsAtLHR', 'popupwindow', 'scrollbars=yes,width=800,height=600');return true"><p><label for="tlemail">Enter your email address</label></p><p><input type="text" style="width:140px" name="email" id="tlemail" /></p><input type="hidden" value="1" name="embed"/><input type="submit" value="Subscribe" /><p><a href="https://tinyletter.com" target="_blank">powered by TinyLetter</a></p></form>
