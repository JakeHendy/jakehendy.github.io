---
layout: single
title: 02/10's AWS Updates ☁
tags: aws, aws-updates
---

_A lookback of the past 24 hours of updates from AWS, applicable to my x-gov colleagues and I with the occasional interesting piece thrown in._

Ah, the sunshine is back here in Exeter! 🌞☀
Oh, AWS released some very business-friendly updates too, from Machine Learning to authenticating to an Oracle Database. _Something for everybody!_

# SageMaker supports G4 and R5 instances for Real-Time inference
You can now use the G4 and R5 instance family when running your ML models for real-time inference.
The G4 family features those juicy NVIDIA T4 Tensor Cores, whilst the R5 family features a high memory-to-vCPU ratio. 
When the `G4.metal` instance type launches, you'll be able to run your real-time inference jobs on an instance with 8 T4 GPUs, 284GB of memory, 96 vCPUs, 100Gbps of bandwidth, and up to 1.8TB of NVMe storage. _But does it run Crysis?!_

# Amazon Textract is even more accurate, across more document types
Textract is a ML service designed to make it easier to extract text from a wide variety of documents. As a managed service, everyone should benefit from improvements to the service, like today!
Today:
* Text recognition is more accurate
* Textract corrects document rotation
* Textract is better at isolating documents from their backgrounds. This is more noticeable for documents with sparse text, nonstandard sizes, bent corners, "extreme or unusual backgrounds", and even for documents that are partially covered!
* Confidence scores have been rescaled, better aligning to the accuracy of the ML models underneath.

Get textract-ing! 

# New QuickStart to deploy Boomi Molecule on AWS
There's a new Quickstart to deploy Dell Boomi Molecule on AWS. This Quick Start is:
> ... for users who are looking for an integration platform as a service (iPaaS) that can be hosted on AWS.

Takes 20 minutes but does depend on EFS!

# RDS for Oracle supports User Authentication with Kerberos and Microsoft Active Directory
This is one very long announcement... 
You can now use external authentication to your Oracle databases using Kerberos and AD (of course), enabling you to use SSO to manage access to your databases. 
Your users can reside in AWS Directory Service for AD or an on-prem AD—one assumes that AzureAD is also supported—providing there is a forest-trust relationship established between your on-prem AD and a AWS Managed AD. You can use the same AD for different VPCs within the same region, as well as sharing AD domains across accounts.
There's no additional licening (shocking I know) or cost, but you must be using AWS Directory Service for Microsoft AD Enterprise Edition. You can apply Kerberos authentication to either new or existing DB instances, providing there is a AWS managed AD first. 
To quote AWS: 
>  This feature is supported for 11.2.0.4, 12.1.0.2, 12.2.0.1 and 18c versions of Enterprise edition, and 12.1.0.2, 12.2.0.1 and 18c versions of Standard Edition 2.

# DynamoDBMapper (Java) supports optimistic locking for transactional API calls
DynamoDBMapper, a Java high-level interface for DynamoDB, now supports optimistic locking to help ensure transactional writes are performed on the most recent version of an item. 
Providing you're using transactional API calls, you can use the `@DynamoDBVersionAttribute` annotation to check the version of the item being updated by the transactional write to ensure it has not been changed since it was retrieved from the table. 
Support is available in all regions where DynamoDB is available too; but the pricing is based upon the size of the items in your transaction.

# AWS Amplify Console offers end-to-end browser-based testing with Cypress
The key part of this release isn't part of the headline, but:
Amplify's built in continuous deployment pipeline now contains a test phase to catch regressions and bugs before your code ends up on production. Configure it within your existing build yaml file to run "any testing framework of your choice"...

Additionally, there's an integration with Cypress for browser-based testing. Amplify Console will detect those Cypress tests on connection to a repo, execute them, as well as provide access to videos, screenshots, and other artifacts made available during the build.
