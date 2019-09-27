---
layout: post
title: 27/09's AWS Updates ☁
tags: aws, aws-updates
---

_A lookback of the past 24 hours of updates from AWS, applicable to my x-gov colleagues and I with the occasional interesting piece thrown in._

For the first time in this (public) series we have an update that's slipped in between other older updates. Admittedly this public series has only been going for 4 days, but in the past several months of the private updates it happens too. 
Dates and releases are tricky yo, even for hyperscalers...

# Amazon Polly voices are now available in Windows applications
This is—to me—quite incredible. Windows has a native Speech API (SAPI) that applications can take advantage of for speech synthesis. There are 2 defaults included (one male, one female), and any application running on Windows can take advantage of this API.
There is now a native Polly interface you can use to power SAPI, meaning well over 50 voices in over 25 langauges are available to your applications. This still follows the pay-as-you-go model for Polly via AWS APIs. You still need an internet connection, as well as installing the AWS CLI on end-user devices and creating an IAM user for an appropriate account.
Still, really neat though 💬🗣.

# SageMaker Neo is now available in 12 additional regions
Train your ML models in London now, and then run them anywhere, "in the cloud and at the edge". Neo allows you to make your models up to 2x as fast with less than a tenth of the memory footprint, creating executables optimised for either Intel, NVIDIA, or ARM platforms.
How? With Machine Learning of course, the Neo compiler will use ML to understand what optimisations are available for _your_ ML, and then apply them. 

# Glue Python Shell jobs now support `wheel`s
Use `wheel`s to specify dependencies within your Glue Python Shell jobs, instead of `egg`s. You can then take advantage of all the features of new [`wheel` packaging format](https://www.python.org/dev/peps/pep-0427/). 
Available everywhere that Glue is. 

# Execute "complex" playbooks with Ansible using AWS Systems Manager
You can now use Systems Manager to run Ansible playbooks from GitHub or S3 against both your on-prem and in-cloud EC2 estate, using either Run Command or State Manager.
The snark in the title isn't justified, as you can zip up/store in a directory a series of playbooks and AWSSM will execute them as instructed, preinstalling any dependencies required. 
Useful for hybrid and pure-cloud deployments, you can then also integrate with the other features available in Systems Manager.
