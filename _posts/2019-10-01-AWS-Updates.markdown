---
layout: post
title: 01/10's AWS Updates ☁
tags: aws, aws-updates
---

_A lookback of the past 24 hours of updates from AWS, applicable to my x-gov colleagues and I with the occasional interesting piece thrown in._

HOORAY IT'S OCTOBER AND PAYDAY HAS BEEN and it's gone again. However, more AMD instances have arrived in (AWS) London and much more!

# Use PrivateLink Endpoint Policies to better control access to ECR
ECR now supports PrivateLink Endpoint Policies, enabling granular API level access to container image repositories.
The policies allow grant and deny access, using explicit IAM resource policies.
You can apply these policies to existing PrivateLink VPC Endpoints or new ones. 

# EC2 AMD Instances are now available in additional regions:
`M5a`, `M5ad`, `R5a`, and `R5ad` instances are now available in London! Current `*a` instance families use 2.5GHz EPYC 7000 series processors, offering you similar-to-same performance at a 10% cost saving! I'm really looking forward to when the new Ryzen 3-equivalents hit AMD, based on their current perforamnce-per-dollar metrics it should be pretty sweet 💸🎉
Also, it looks as if the `M5ad`s and `R5ad`s launched in Ireland and London at the same time! Hopefully the pace of delivery to London after Ireland is improving... 

# AWS Client VPN now supports MFA for Active Directory
If you use AD for your Client VPN—either Managed AD or using AD Connector—you can now use MFA with your VPN; such as verifying a push notification or an email-based OTP. There is no additional cost for this service!

# EKS now supports G4 instances as worker nodes
The G4 family features NVIDIA T4 GPUs, custom INtel Cascade Lake CPUs, and up to 100Gbps of throughput with 1.8TB of local NVMe Storage. 
Providing you're running 1.5.4 or later of the VPC CNI plugin, you too can run your containers on G4 workers! (Providing they're available in your region...)

# Amazon MQ introduces vertical scaling for message brokers
"Right-size your message broker" isn't something you hear everyday, but now you can modify the instance type on demand, either immediately or during the next maintenace window. Interestingly, vertical scaling is endorsed for "seasonal changes" and to "increase capacity as your applicaion grows". MQ is a managed broker service for Apache ActiveMQ, allowing you to use JMS, NMS, AMQP, STOMP, MQTT, and WebSocket. 

# New, AWS IQ!
> AWS IQ is a new service that enables customers to quickly find, engage, and pay AWS Certified third-party experts for on-demand project work. AWS IQ offers video-conferencing, contract management, secure collaboration, and integrated billing.  
This could be very interesting. Reading [Jeff Barr's blog post](https://aws.amazon.com/blogs/aws/aws-iq-get-help-from-aws-certified-third-party-experts-on-demand/) on the topic it reads a bit like a streamlined [Digital Marketplace](https://www.digitalmarketplace.service.gov.uk) specific for AWS services, with AWS ensuring billing and access management are done well between your account group and the contractor.
Hopefully the requirement for an AWS certification will ensure good quality responses, and that AWS will moderate this.
Speaking to a industry veteran, hopefully it's not a race-to-the-bottom money-wise and thus quality wise. Time will tell!

That's all for today, do enjoy :) 
