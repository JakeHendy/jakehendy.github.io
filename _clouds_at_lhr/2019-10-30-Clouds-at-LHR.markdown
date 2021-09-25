---
layout: single
title: 30/10's Cloud Landing  ☁
tags: aws, aws-updates
---

Good morning! Welcome to the seventh post in the series that has a name; _Clouds At LHR_. You can also sign up for the newsletter on Tiny Letter; [https://tinyletter.com/CloudsAtLHR](https://tinyletter.com/CloudsAtLHR), or look at the embed form at the bottom of this post. As always you can send feedback to [@JakeHendy on Twitter](https://twitter.com/JakeHendy) or through any other means you have!

A bumper series of announcements today from Image Scanning in ECR (woo 🎉) to improved Oracle ops support.
The ECR Image Scanning is a particularly welcome feature and one which we'll be integrating in to our own workflow soon!
I don't want to spoil the news for you though, so grab a hot beverage on this cold winter's morning and read on!

## Feature and Service updates

The latest feature and service updates that are either juicy, in Ireland or London, or all 3/4!

### Image Scanning for ECR

ECR can now scan your docker images for vulnerabilities, helping to improve the security posture of your infrastructure and your organisation.
You can enable ECR Image Scanning on image push, or perform on-demand scanning.
When ECR performs a scan it'll check against an aggregated set of CVEs and create a report in the ECR console.
[Integration with Security Hub](https://github.com/aws/containers-roadmap/issues/17#issuecomment-545260526) is coming later, however if you have a custom SIEM tool that allows you to integrate other sources, you can use the ECR APIs to add the CVEs and images affected. There's a [blog post](https://aws.amazon.com/blogs/containers/amazon-ecr-native-container-image-scanning/) which (we will summarise later on) that has a more detail, including an example app to continually rescan your images.
Available at no extra cost in all commercial regions (and GovCloud US)!

### RDS for Oracle supports EMCTL Commands for Enterprise Manager Cloud Control

RDS Procedures have been added which in turn can invoke certain EMCTL commands on the management agent. 
To quote the news release:
> you can get the Management Agent's status, restart the Management Agent, list the targets monitored by the Management Agent, clear the Management Agent's state, force the Management Agent to upload its [sic? _Should it be upload to?_] associated Oracle Management Server (OMS), and ping the Management Agent's OMS

Available where RDS for Oracle is!

### ElastiCache supports online migration from Redis on EC2

Move your data from a Redis instance on EC2 to an ElastiCache cluster, providing it's in the cluster-mode disabled configuration.
ElastiCache will then replicate the data from your existing EC2 cluster in real time, where you can then flick a switch to move to the ElastiCache cluster.
Available everywhere ElastiCache is!

### RDS for PostgreSQL supports Kerberos and AD Authentication

If this sounds familiar, it's because almost a month ago this feature was [launched for RDS for Oracle](https://jakehendy.com/2019/10/02/AWS-Updates/#rds-for-oracle-supports-user-authentication-with-kerberos-and-microsoft-active-directory).
In addition to password-based and IAM-based authentication, you can use AWS Managed Microsoft AD Service to auth to your PostgreSQL systems, whether it's through a pure AWS managed forest or if there's a forest trust relationship set-up with an on-prem AD system.
PostgreSQL version 11.4 and 10.9, and above are supported for integration. 
Available where RDS for PostgreSQL is!

### Elastic Beanstalk adds support for PHP 7.3 and .NET Core 3.0

You can now run PHP 7.3 and .NET Core 3.0 applications on Elastic Beanstalk.
Sadly, Elastic Beanstalk doesn't support running .NET Core 3.0 on Linux instances, nor does it have any Windows Server 2019 capabilities for Windows instances.

However, if you do need to run PHP or .NET Core workloads in a pinch, amongst many other languages supported, I recommend you try out Elastic Beanstalk!

### AWS Certificate Manager Private CA enforces name constraints

AWS CM PCA, to use the full initialism, now enforces name constraints in imported certificates.
Administrators can set these constraints to allow or disallow certain names, as well as deny public or private DNS names.
Available everywhere Private CA is available.
Remember that you get 30 days of Private CA for free, for your first CA. After that, you pay a hefty price ($600 per month) plus additional costs for issuing certificates, so be careful!

### AWS Snowball Edge supports volume sizes up to 10TB

Snowball Edge now has a ten times higher limit for block storage volumes, up to 10TB.
Using block storage you can add/remove volumes from EC2 instances running on your device with them persisting independently of those instances.
You can use either an SSD (attached via NVMe for Compute Optimised devices, and via SATA SSD for Storage Optimised) or a capacity optimised HDD; with the HDD supported on any Snowball Edge device.
Available worldwide, literally anywhere.

### Global Accelerator supports EC2 Instance Endpoints

Global Accelerator now directly supports EC2 instances, providing a single internet-facing access point to your EC2 instances.
Previously you had to use a Application Load Balancer, Network Load Balancer, or Elastic IP address to enable Accelerator to front your EC2s.
Global Accelerator will still preserve the source IP address, enabling you to do fancy magic all the way to the EC2. 

Additionally, Global Accelerator will create two fully-qualified domain name A records and two pointer (`PTR`) records for each new accelerator, with records for existing accelerators already created.
There is now also integration with Route53 ALIAS records.
There's no additional charge for the direct integration with EC2s or DNS records. 
Available in London and Ireland!

## News and Blog posts

### [Image Scanning for ECR](https://aws.amazon.com/blogs/containers/amazon-ecr-native-container-image-scanning/)

This blog post from individuals on the ECR/AWS Containers team walks you through the basics of container scanning (static vs dynamic) and a sample use-case (with an example app) for on-demand re-scanning of images in an ECR repository.
The blog post highlights their rationale for making this free (ensuring it's part of your workflow thus increasing everyone's security posture) and the limitations in place; you can only scan once every 24 hours. AWS don't actually recommend scanning more than once every 24 hours, zero-day vulnerabilities are relatively rare and in theory will take more than 24 hours to react, mitigate, and respond to the vulnerability before it can be published.
Of course, this doesn't prevent you from using your own container scanning tools, but this is a great tool to integrate in to your workflow regardless.
It's a short, sweet, and concicse blog post that is well worth even just to brush up on the basics of container security.

## TinyLetter signup

<form style="border:1px solid #ccc;padding:3px;text-align:center;" action="https://tinyletter.com/CloudsAtLHR" method="post" target="popupwindow" onsubmit="window.open('https://tinyletter.com/CloudsAtLHR', 'popupwindow', 'scrollbars=yes,width=800,height=600');return true"><p><label for="tlemail">Enter your email address</label></p><p><input type="text" style="width:140px" name="email" id="tlemail" /></p><input type="hidden" value="1" name="embed"/><input type="submit" value="Subscribe" /><p><a href="https://tinyletter.com" target="_blank">powered by TinyLetter</a></p></form>
