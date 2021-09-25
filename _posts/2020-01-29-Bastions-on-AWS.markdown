---
layout: single
title: Bastions on AWS
tags: aws, architecture
---

Sometimes your services and platforms on AWS still require you to have a network, even when you're serverless.
For the platform at work my team is responsible for this is the boat we continually sail in, taking advantage of AWS Fargate, S3, ElastiCache, but not AWS Bastion Service.
Why? Because it doesn't exist yet—fully at least. Sometimes, you just need to get on a local network and play with things. 💻

There is AWS Systems Manager Session Manager (hereafter referred to as AWS SM), but that only works as an interface on to existing EC2s, so in this post I'll provide steps on how to build a secure, cost-efficient way to access your network using AWS SM.

## Repeatable Bastions

Create a specific AMI (as part of your build process, automate it as you need to) or—if internet access is permitted—use a user-init script to create the basis of your bastion:

* updating system dependencies
* installing the minimum/common software
* configuring SSH keys/certificates for communication within the network (but not for user logon)
* configuring logging etc

Don't forget to setup log forwarding to CloudWatch logs as appropriate as well, follow the [NCSC guidance on log retention][NCSC-Log-Retention] as a minimum.

## Bastions lost in the Amazon

We only want our Bastions accessible to Amazon, so create a Launch Configuration with no public IP and the security groups required for internal access.
Add the AWS SSM Agent to your AMI/User Init Script, if you're on a recent version of Amazon Linux{1/2}/Ubuntu/Windows, you'll already have the SSM agent installed.
Provide them with the appropriate security groups to access the internal resources, or alternatively you can create multiple bastions for different security zones.

If your region and required applications permit, you can use AMD-variants of your bastions (e.g. `t3a`, `m5a`) or ARM-variants with the `a1`/`a2` instance families, saving even more money.

## Configure your Session Manager

[Configure Session Manager][SessionManagerGettingStarted] and ensure your operators' IAM roles/users have permission to create SessionManager sessions.
You'll need to ensure your IAM user has the ability to create Session Manager sessions.
Remember Session Manager is on a per account basis, so where you intend to launch your bastions is where you'll need Session Manager set up.

You have the option of forwarding the whole session console to CloudWatch logs. Such a feature will be very useful when you're writing your post-incident report or providing example output for your ops teams.
If your terminal/console session is likely to contain sensitive details ensure you enable encryption in your CloudWatch logs with a suitable KMS key.

## Bastions there when you need them

Use an EC2 auto-scaling group with a min of 0, desired of 0, a max of 1, and then change the desired value when you need—and are subsequently finished with—your bastion.
If your network architecture only allows access within the same AZ, you can create 3 scaling groups for each AZ.

This means that your bastion is only there when necessary, reducing cost and the potential attack surface for your system. You can even go further and add a [Message Of The Day][MOTD] to give some advice to an operator that's using a bastion, or add a crontab to kill the bastion after a number of days (unless a file exists) to help reduce reliance on that single instance.
This pattern is used on a cloud system at `[REDACTED]`, they love it 🤩

## _Fin_

That's all there is; you now have a Bastion that:

* doesn't exist until an operator needs it,
* that contains all the software they'll need,
* isn't open to the internet, but can be accessed using PuTTY or an operators browser,
* is fully auditable using your existing patterns with CloudWatch Logs.




[NCSC-Log-Retention]: https://www.ncsc.gov.uk/guidance/introduction-logging-security-purposes
[SessionManagerGettingStarted]: https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-getting-started.html
[MOTD]: https://www.linux.com/tutorials/put-talking-cow-your-linux-message-day/