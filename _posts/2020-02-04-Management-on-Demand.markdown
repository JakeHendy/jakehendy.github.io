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

# Yes lambda is necessary

You can do *many* things with API Gateway, including launching an instance with a simple REST call. Honestly I did it:
```
GET /vac-list/launch

<?xml version="1.0" encoding="UTF-8"?>
<RunInstancesResponse xmlns="http://ec2.amazonaws.com/doc/2016-11-15/">
    <requestId>b0f2952d-4c1a-412e-a831-623662c82ec8</requestId>
    <reservationId>r-0bbafa6990468fabe</reservationId>
    ...
</RunInstancesResponse>
```
The API Gateway execution log includes
```
Endpoint request URI: https://ec2.eu-west-2.amazonaws.com/?Action=RunInstances&KeyName=aws-ec2_2&Version=2016-11-15&ImageId=ami-0089b31e09ac3fffc&MaxCount=1&InstanceType=t3a.nano&MinCount=1
```
