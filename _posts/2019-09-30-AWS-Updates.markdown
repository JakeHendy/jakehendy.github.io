---
layout: post
title: 30/09's AWS Updates ☁
tags: aws, aws-updates
---

_A lookback of the past 24 hours of updates from AWS, applicable to my x-gov colleagues and I with the occasional interesting piece thrown in._

How is it Monday already?! There were no updates on the 28th, and now all of a sudden it's Monday again. At least, it's payday. AND, there's some fun AWS Updates.

# Amazon Linux 2 AMI with .NET Core now includes Mono
The AL2 AMI now includes Mono 5.18, as well as .NET Core 2.2 (a LTS release), PowerShell Core 6.2, and of course the AWS CLI. Available in all public regions!

# IoT Core introduces "Multi-Account Registration" in Beta
The new "Multi-Account registration" feature aims to simplify device registration by allowing IoT devices to move between accounts using SNI strings to route to the correct IoT endpoint. 
Devices can also be registered without requiring a Certificate Authority to be registered with AWS IoT. 
This is a closed beta, so head [to the Multi-Account Registration beta page](https://pages.awscloud.com/iot-core-early-registration.html) to sign up!

# New QuickStart for deploying JFrog Artifactory in AWS
You have 3 options to deploy JFrog in to your AWS ecosystem, using EC2, ECS, or EKS! Deployment takes 30-45 minutes, depending on your option!
_Editor's note: There is also Artifactory Cloud which I would encourage you to explore first, unless your actual security/business requirements stipulate you must remain in absolute control of all artifacts at all times_

# ECS supports Automated Draining for Spot Instances
ECS will place Spot instances in the `DRAINING` state when it receives the two minute interruption notice. Tasks will then be scheduled elsewhere on the cluster, and no new tasks will be placed on the to-be-terminated instance(s). ECS will handle all the replacement of tasks and termination of load balancer connections to reduce the probability of service interruptions. 
Set the `ECS_ENABLE_SPOT_INSTANCE_DRAINING` parameter to `true` in the User Data field when you launch an instance, to kick the ECS agent in to action. Available in all regions
