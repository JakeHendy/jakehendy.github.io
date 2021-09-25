---
layout: single
title: 25/09's AWS Updates ☁
tags: aws, aws-updates
---

_A lookback of the past 24 hours of updates from AWS, applicable to my x-gov colleagues and I with the occasional interesting piece thrown in._

The last 24 hours in AWS world can either be full of updates or not, and those updates can be a whole mix of minor or major. Today, we've got a nice mix across 8 updates, so let's dive in!

# Amplify Console provides downloadable access logs for hosted web apps
You can now download the CDN access logs for your distribution containing every user request received by the CDN. Available in CSV format for any two-week period. 
_I'm surprised you weren't able to get the logs beforehand, but also that you can download them for "any two-week period"_

# AWS DataSync now supports all Amazon S3 Storage Classes, with more data controls
You can now transfer your data to any S3 Storage class, control overwrites for existing files (or objects!) and configure additional data verification checks. 

# Transcribe now supports AWS KMS Encryption
You can now specify your own KMS keys to encrypt the transcripts from Transcribe. You can of course still use the default S3-SSE method too.

# vCPU-based On Demand Instance Limits are now available in EC2.
Just over two weeks ago AWS announced a new method for controlling compute capacity within your account in EC2: [vCPU-based On Demand instance limits with EC2](https://aws.amazon.com/blogs/compute/preview-vcpu-based-instance-limits/). 
_Oddly, this announcement included fixed dates that Amazon appeared to stick to!_
Instead of using instance-family limits (i.e. you can have one of the X family, 10 of the C family) you can now specify the maximum number of vCPUs in use across an account across 5 different groups: the standard families (A, C, D, H, I, M, R, T, and Z); accelerated like FPGA (F), graphic-intensive (G), general purpose GPU (P); and the special memory-optimised (X) instace families.
For instance you could prohibit all accelerated and special memory-optimised families by setting their maximum vCPU to `0` whilst setting the standard family to `256`, where you could use 64 `m5.xlarge` instances or a combo of 1 `m5d.metal`, one `c5.metal`, one `z1d.metal` and an `a1.4xlarge` to maximise it. 
This is available now for you to opt-in to. You should opt in, because on October 24th 2019 it'll be enabled across all accounts regardless.

# AWS Marketplace supports Paid Container Software on EKS
You can now find and pay for software using AWS Marketplace and run that software on top of EKS, providing your EKS cluster is running EKS 1.1.3 or later. 

# AWS Limit Monitor now supports vCPU-based instance limit monitoring
The Limit Monitor solution now uses Service Quotas to proactively track your resource usage, sending you notifications when you approach those limits. With EC2 moving to vCPU-based limits, Limit Monitor now supports vCPU-based monitoring.

# ElastiCache announces online configuration changes for all planned operations with Redis 5.0.5
Alongside support for Redis 5.0.5, you can now scale your cluster, upgrade the engine version, apply patches and maintenance updates whilst your cluster stays online and serving incoming requests. Previously this was only supported for ElastiCache clusters with Redis Cluster mode enabled, if you had cluster-mode disabled there was downtime of a few seconds due to DNS updates. Providing your clusters have auto-failover enabled, you can now take advantage of hot planned operations and 5.0.5 in all regions!

# Aurora Serverless PostgreSQL Now Supports Data API
Use a HTTPS API endpoint to make an SQL Query, how Web 2.0! This massively improves the accesibility of Aurora (or at least, Aurora Serverless) when using Lambda, AppSync, and Cloud9. Extending beyond what Amazon put in the announcement, I imagine this would be incredibly useful also for cross-account querying etcetera. The Data API is available in Ireland. 
The Data API uses Secrets Manager so you don't have to pass credentials, but you do need to have the `AmazonDSDataFullAccessPolicy` managed policy enabled for your principle OR the equivalent in an unmanaged policy. 
The Data API is supported for both PostgresSQL and MySQL Aurora Serverless databases. 
