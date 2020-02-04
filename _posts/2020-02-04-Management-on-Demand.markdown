---
title: SSH & Management on Demand
tags: aws, architecture
---

Because sometimes you just need to SSH in and investigate with a terminal.

Following on from _[Bastions on AWS]({% post_url 2020-01-29-Bastions-on-AWS %})_ this post (or series) will look at using some additional AWS tools to grant us the ability to launch bastion boxes for single-use operations with full auditing and shutdown capabilities.

We will use:

* API Gateway so we can hit a URL and kickstart the launch
* Lambda with
  * CloudTrail, so that when an EC2 is shutdown for more than 5 minutes it's terminated
  * API Gateway to provision our bastion
* Cognito for SSO with API Gateway