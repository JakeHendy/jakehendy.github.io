---
layout: post
title: 17/10's Cloud Landing  ☁
tags: aws, aws-updates
---

Good morning! Welcome to the third post in the series that has a name; _Clouds At LHR_. You can also sign up for the newsletter on Tiny Letter; [https://tinyletter.com/CloudsAtLHR](https://tinyletter.com/CloudsAtLHR), or look at the embed form at the bottom of this post. As always you can send feedback to [@JakeHendy on Twitter](https://twitter.com/JakeHendy) or through any other means you have!

What a busy 24 hours it's been; I've been having _fun_ with SharePoint updating my Team's site; there's been an internal expo; and AWS have released a number of updates. I'm also going to try a new format, including some interesting news as well as releases. 

# Feature updates

## New _Migrating To The Cloud_ Coursera course
Available digitally, this course focuses on using the AWS migration tools (Snowmobile is one method Joel, maybe this is your chance!) to move your compute, storage, and database workloads to AWS. You can "audit" the course for free or pay $49 and get a completion certificate and graded materials too.  

## New QuickStart to deploy TIBCO JasperReports on AWS
There's a 35-minute quickstart to deploy JasperReports on AWS, either extending your existing deployment or starting a new deployment. 
This QuickStart also features quick connects to enable JasperReports to connect to your RDS, RedShift, and EMR clusters and immediately begin reporting on them!

## AppStream 2.0 adds support for 4K UltraHD on 2 monitors, and 2K on 4
On _any_ instance type you can stream 2560x1600 content on 4 monitors. With the Graphics instance family you can stream 4K content on 2 monitors. You must use the Windows desktop client to take advantage this, and your image must be running an agent released after September 23rd 2019. 
_MMmmmmm 4K_

## AWS RoboMaker supports Robot OS 2 in beta. 
> ROS2 is built on top of Data Distribution Standard (DDS), an industry data connectivity standard that provides discovery, serialization, and transportation.
You can even play with this beta in Ireland, and AWS of course don't recommend it for production workloads. The beta is due to close in the secondhalf of 2020.

## MSK now supports 2-AZ clusters
_This release doesn't have the best information, so I do apologise_
You can now run your Managed Kafka clusters over 2 AZs.
I'm not sure if you could run your cluster in 3 AZs before, or if you had to spin up 3 individual clusters and configure their replication.
The documentation/developer guide is particularly lax as it indicates 3 availability zones. 
Maybe it means you can now run it in just 2 clusters instead of 3, who knows. 

## EMR 5.27.0 released; adds support for reconfiguring multi-master nodes
EMR 5.23.0 enabled support for multi-master nodes, increasing the resiliency of your long-lived jobs. 
Now with EMR 5.27.0, you can reconfigure those clusters without having to recreate the clusters, and whats more you can do it on the fly. 
Additionally, EMR 5.27.0 adds support for Apache Flink 1.8.1, Apache Spark 2.4.4 with Scala 2.11, JupyterHub 1.0.0, and Tensorflow 1.14.0. Flink now supports deployment within a multi-master node custer.
Everywhere that EMR is available, you can now upgrade to 5.27.0!

## Amazon DeepLearning containers support PyTorch
The Amazon DeepLearning docker containers now include PyTorch. These images are stored in ECR and can be deployed anywhere you can pull from ECR; from EC2, ECS, EKS, k8s on EC2, to SageMaker! 

## DocumentDB adds Aggregation Pipeline Capabilites using `$lookup`
DocumentDB now has support for the `$lookup` and `$addFields` aggregation pipeline stages, as well as the `$concatArrays` pipeline operator. 

## API Gateway supports access logging to Kinesis Firehose
In addition to CloudWatch logging you can now stream API Access logs to Firehose, enabling real-time analysis of your access patterns within AWS or using external services. Simply update your Gateway configuration to point to the Kinesis Stream as opposed to a CloudWatch log group and off you go!

## GuardDuty adds 3 new Threat Detections
GuardDuty will now raise an alarm if the S3 Block Public Access feature was disabled or if Server Access Logging was disabled where it was previously enabled. These findings have a _Low_ severity.

GuardDuty will raise an alarm with a _High_ severity if it detects an EC2 instance making a DNS query, which resolves to to the EC2 Metadata IP address (`169.254.169.254`) which can be an attempt at DNS rebinding, leading to exposure/exfiltration of IAM credentials etcetera.

## Neptune now supports streams to capture graph data changes
Neptune has an endpoint (for SPARQL or Gremlin formats) which will allow you to easily capture the change-log data of your Graphs. You can get a JSON view and trigger lambdas, or ingest data in to other services. This feature is in _lab mode_, and is toggleable within the cluster parameters under the name `neptune_lab_mode`. 
You will incur I/O and straoge costs associated with the change-log data, and this feature is available everywhere Neptune is today.

## Neptune supports SPARQL 1.1 Federated Queries
Neptune can now execute parts of your SPARQL queries across mutiple SPARQL endpoints within a VPC. 
You can now separate your data cross multiple Neptune clusters, as well as use Neptune to merge in content from external SPARQL endpoints. Neptune takes advantage of the `service` keyword within SPARQL to identify the location of the SPARQL endpoints to use, and can also be used to federate against another Neptune cluster secured with AWS IAM.
There are no additional data charges whilst data transfer is within the VPC. 

## CodePipeline adds execution visualistaion to execution history
You can now see visualisations of past pipeline executions, rather than information about actions that ran in a failed pipeline execution. In addition, you see the actions that didn't run helping you debug and understand pipeline failures better. 
This even applies to pipelines that make use of concurrent executions!

## RDS on VMware is Generally Available (in the US regions)
This is *interesting*, it's very similar to Control Tower.
RDS on VMware will allow you to run RDS on your own VMware estate in your own datacentre, and RDS will manage provisioning, OS and DB provisioning, backups, restores, healthchecks and all. You can run MSSQL, MySQL, and PostgreSQL clusters locally on your clusters today.
This is available in the US East regions (N. Virginia, Ohio), and I imagine more very soon
There's an accompanying [blog post](https://aws.amazon.com/blogs/aws/now-available-amazon-relational-database-service-rds-on-vmware/) which I highly recommmend reading. 
There are requirements for the local management plane (180GiB storage, 24vCPUs, 24GiB memory) as well as connectivity and user requirements.

## Chime supports Firefox/Chrome screen-sharing without plugins
Chime users can now use native APIs in Firefox and Chrome to screenshare, meaning they no longer have to download any plugins. This means those in highly-regulated environments can reduce their software footprint, and still take advantage of the collaboration features Chime provides. This is available for those running FF 66 and Chrome 72 and later versions, on Windows, macOS, and Linux!


# News Releases
This new feature comes straight from the blog/twitter.

## Migration Complete: an Oracle no more
Amazon Consumer (that is amazon.com, Alexa et al) have just finished migrating their databases to services on AWS. Some Oracle databses remain for third-party supplied software, but I imagine this will be phased out eventually.
The [blog post](https://aws.amazon.com/blogs/aws/migration-complete-amazons-consumer-business-just-turned-off-its-final-oracle-database/) has some incredible statistics, moving 75 *_petabytes_* of data to AWS. 70% reduction in admin costs for some services.
Admittedly, whilst Amazon is "just like any other customer" at this price range they can of course negotiate discounts. But it's still significant savings compared to Oracle. 
I'd love to know how they moved all that data; obviously they could use a Snowmobile, DirectConnect, as those Amazon DCs would have been meaty. It took several years but it shows that if Amazon can do it, with petabytes of data, most people can!

Take a read, it's worth it.

# TinyLetter signup

<form style="border:1px solid #ccc;padding:3px;text-align:center;" action="https://tinyletter.com/CloudsAtLHR" method="post" target="popupwindow" onsubmit="window.open('https://tinyletter.com/CloudsAtLHR', 'popupwindow', 'scrollbars=yes,width=800,height=600');return true"><p><label for="tlemail">Enter your email address</label></p><p><input type="text" style="width:140px" name="email" id="tlemail" /></p><input type="hidden" value="1" name="embed"/><input type="submit" value="Subscribe" /><p><a href="https://tinyletter.com" target="_blank">powered by TinyLetter</a></p></form>
