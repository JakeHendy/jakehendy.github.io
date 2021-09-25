---
layout: single
title: 09/10's AWS Updates ☁
tags: aws, aws-updates
---

_A lookback of the past 24 hours of updates from AWS, applicable to my x-gov colleagues and I with the occasional interesting piece thrown in._

At some point I'll set up the tinyletter for this series (I even have a name), and create the blog posts earlier. 
_That_ point isn't today, but we do have a wide range of other points to take your fancy from APN Training Courses to TLS on Elastic Load Balancers to Windows on EKS.

_Wow, I even got delayed until 1600 to start writing from here, I do apologise!_

# New Training Courses teach new APN partners to better help their customers
_AWS Solutions Training for Partners: Foundations (Business) has been signficiantly updated, helping APN Partners build their business with AWS. 
_AWS Solutions Training for Partners Foundations - Public Sector - Business_ (type it out 5 times without making a mistake, go on) teaches APN Partners about AWS Best Practices with a specific emphasis on public-sector organisations, opportunities, and the org's priorities (up to and including CxO level).
Useful if you want to sanity check your partners and make sure they're up to date.

# Snowball Edge supports offline software updates in air-gapped environments
Using the CLI you can now download the software update to apply to your Snowball Edge using the device API. This is great if you're using Snowball Edge's in airgapped networks/networks with no internet connectivity. If you're running the device on a higher network, you of course will sheep-dip the software update to ensure it's not contaminated right? :) 

# New courses to help grow and accelerate your AWS Cloud Skills
2 new public classroom courses are available; _Cloud Practitioner Essentials_ is an updated classroom version of the free digital course. _Cloud Practitioner Essentials_ is available as a one-day, instructor led classroom course and is great for those new to AWS Cloud, those seeking an overall understanding of AWS Cloud fundamentals, and it also helps learnings prepare to take the _AWS Certified Cloud Practitioner_ exam. 
_Architecting on AWS - Accelerator_ is new based upon the _Architecting on AWS_ and _Advanced Architecting on AWS_ 3-day courses, consolidating the topics in to a single four-and-a-half day course. The consolidation will enable you to fast-track your training, completing it in a single week. Useful if you're preparing for the _AWS Certified Solutions Architect - Associate_ exam.

# Windows nodes supported by EKS! 
EKS has moved Windows worker node support out of public preview. Providing you're running EKS with K8s 1.14 and above, you can now run Windows workers in your EKS cluster.

# RDS for PostgreSQL adds new minor versions, Transportable Database feature
RDS PostgreSQL now supports 11.5, 10.10, 9.6.15, 9.5.19, and 9.4.24. Each minor release contains security fixes, bug fixes, and improvements. 
PostGIS 2.5 is now supported for all major versions, so you can now upgrade directly from 9.4.24 to 11.5 with PostGIS. 
The precheck processed whilst doing your major version upgrades has been improved to scan for all potential compatibility issues across all databases in the instance, rather than stopping after the first one it finds.

If you're looking to transport data import/export between databases you can now use `pg_transport` to move those large databases between RDS PostgreSQL instances. supporting in PG 10.10, 11.5 and newer. 

# EC2 High Memory Instances with up to 24TB of memory
If you need to run large in-memory databases, like SAP HANA, you're in luck as there are no new instances with 18TB and 24TB of memory generally available. 
EBS-Optimised by default, 28Gbps dedicated storage bandwidth, Elastic Network Adapter-based enhanced networking, 100Gbps total aggregate network bandwdith. Running on 8-socket platforms using _Cascade Lake_ Xeon Scalable processors.
You can use 6, 9, or 12TB instances in Ireland but you must purchase a 3-year reservation on EC2 Dedicated Hosts. 18TB and 24TB instance sizes are available in N. Virginia now, with additional regional availability "coming soon". 
Not in the portal though, you have to speak to your account team... :) 
(But does it run crysis?)

# Athena provides an interface VPC endpoint
You can now submit queries to Athena without using the internet by attaching an interface VPC endpoint to your VPC. You must use the Console, CLI, and one assumes API to create the endpoint and attachment. 
Available everywhere Athena is, _except_ Stockholm and US Gov Cloud. 

# Kinesis Data Firehose adds cross-account delivery to Amazon Elasticsearch Service
As the title says, your target Elasticsearch Service can now reside in any account. Capture, transform, and load streaming data in to S3, Redshift, Elasticsearch Service, and Splunk using Kinesis Data Firehose, transforming it along the way if necessary!
_I think they must reside still in the same region, however_

# ALB/NLB add new Security Policies for Forward Secrecy
There are 3 new security policies enabling forward secrecy:
`ELBSecurityPolicy-FS-1-2-2019-08` will grant you the same set of ciphers as `ELBSecurityPolicy-FS-2018-06` except it will enforce TLS 1.2 only.
If you need TLS 1.1, you can use `ELBSecurityPolicy-FS-1-1-2019-08` too, but you should definitely follow [NCSC guidance on TLS where possible](https://www.ncsc.gov.uk/guidance/tls-external-facing-services). 
`ELBSecurityPolicy-FS-1-2-Res-2019-08` is the most restrictive policy (guess what the `Res` stands for), supporting TLS 1.2 and ECDHE (PFS) and SHA256 or stronger (284) ciphers. 
Available in all AWS public regions for new and existing load balancers. 

# Amazon Redshift announces AZ64
AZ64 is a proprietary compression encoding that's designed to achieve a high compression ratio and improved query performance. 
AZ64 is efficient for small groups of data values and uses SIMD instructions for data parallel processing. 
Available in Redshift Cluster versions 1.0.10013 or later, you can get the following improvements:

> Compared to RAW encoding, AZ64 consumed 60–70% less storage, and was 25–30% faster.
> Compared to LZO encoding, AZ64 consumed 35% less storage, and was 40% faster.
> Compared to ZSTD encoding, AZ64 consumed 5–10% less storage, and was 70% faster.

_[Statistics source](https://aws.amazon.com/about-aws/whats-new/2019/10/amazon-redshift-introduces-az64-a-new-compression-encoding-for-optimized-storage-and-high-query-performance/)_.

# SageMaker notebooks now support diffing
Compare and view the differences between two notebooks when they're version controlled with Git in SageMaker. 
As SageMaker notebooks are Jupyter notebooks, and as Jupyter notebooks are stored as JSON documents so they're very easy to diff in version control, thanks to the JupyterLab-Git extension. 
You can look at a cell-by-cell difference with output and images rendered as well, so you can focus on the content rather than the metadata. Available by default to all SageMaker users.
