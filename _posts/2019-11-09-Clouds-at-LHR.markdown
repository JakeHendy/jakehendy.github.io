---
layout: post
title: 09/11's Cloud Landing  ☁
tags: aws, aws-updates
---

Good morning! Welcome to the eigth post in the series that has a name; _Clouds At LHR_. You can also sign up for the newsletter on Tiny Letter; [https://tinyletter.com/CloudsAtLHR](https://tinyletter.com/CloudsAtLHR), or look at the embed form at the bottom of this post. As always you can send feedback to [@JakeHendy on Twitter](https://twitter.com/JakeHendy) or through any other means you have!

It's been a busy week for Amazon (and me, sorry!) so we've got (!) 23 updates available for you from the past 5 days, some big, some small. We've got a whole range of updates, from new instance types to improvements for _your_ customers to wider networking support to support for SQL Server 2019.

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
Only available in Ohio (`us-east-2`) but if you can deploy in Ireland or London, you can deploy in Ohio too right? 😉





## News and blogs

From the introduction we have 3 interesting blog pieces here.

## TinyLetter signup

<form style="border:1px solid #ccc;padding:3px;text-align:center;" action="https://tinyletter.com/CloudsAtLHR" method="post" target="popupwindow" onsubmit="window.open('https://tinyletter.com/CloudsAtLHR', 'popupwindow', 'scrollbars=yes,width=800,height=600');return true"><p><label for="tlemail">Enter your email address</label></p><p><input type="text" style="width:140px" name="email" id="tlemail" /></p><input type="hidden" value="1" name="embed"/><input type="submit" value="Subscribe" /><p><a href="https://tinyletter.com" target="_blank">powered by TinyLetter</a></p></form>
