---
title: Management on Demand
tags: aws, architecture, series_mgmtondemand
---


## Because sometimes you just need to SSH in and investigate with a terminal

Following on from _[Bastions on AWS]({% post_url 2020-01-29-Bastions-on-AWS %})_ this post (or series) will look at using some additional AWS tools to grant us the ability to launch bastion boxes for short term operations with full auditing and shutdown capabilities.

The goal of this series is to have a simple portal that allows a user (signed in via SSO) to launch a bastion in a given VPC.
In the spirit of agile though, we'll work our way up; which you can follow along with [in the GitHub project](https://github.com/JakeHendy/management-on-demand-blog).

In this post we'll start with the bare basics; no authentication, no pretty URLs, a single API Gateway providing us the capability to launch and delete the bastion.

## API Gateway

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
_(`vac-list` I hear you ask? It's because I typo'd)_
The API Gateway execution log includes:
```
Endpoint request URI: https://ec2.eu-west-2.amazonaws.com/?Action=RunInstances&KeyName=aws-ec2_2&Version=2016-11-15&ImageId=ami-0089b31e09ac3fffc&MaxCount=1&InstanceType=t3a.nano&MinCount=1
```

API Gateway provides responses to API calls via "Integrations" with other services: Lambda, HTTP endpoints, Mock endpoints, or AWS.
The AWS integrations allow API Gateway to directly call upon an AWS API endpoint without any middleware, an underused yet very powerful feature.
At some point I hope to post about one of our core APIs which is API Gateway with an integration to DynamoDB, but let's finish this post first.

As you can see above, the response is in XML and thus you can't use API Gateway's very powerful response mapping functionality with it to provide a neater representation.
It seems this is a limitation with the EC2 API, other APIs accept the `Content-Type: application/json` header and respond accordingly but not the one API we want!

To make up for the EC2 API's shortfall in a later post we'll use a lambda to do the heavy lifting for us.
As the XML is readable (if verbose) we'll use that for now with 2 endpoints: one for describing the VPCs in the account; and one for launching an EC2 in a given VPC

## `/network/vpc`

We'll use a simple GET call to list the VPCs in this account. As we're going to use the AWS integrations to start with this will be a regional-specific call.
This limitation is due to the role you assume (to make calls against the API) being in a specific region, and that role is "hard-coded" to the API's configuration. It's a safe rule that (in most cases...) that regions shouldn't depend on other regions, we'll work around that later.

We're going to create two resources, one for `/network` and then a sub-resource at `/network/vpc`, then apply a GET method on `/network/vpc`, but before that we need an IAM Role for API Gateway.

### A quick IAM detour

It's great practice to have super-tight IAM roles and policies throughout your AWS estate, and even though the resulting Bastion will be inaccessible to those who don't have the right IAM policy themselves and the gateway will require SSO, it's always good to practice defence in depth.

We're going to create 2 IAM roles for API Gateway to use: `BastionService_DescribeVpcs` and `BastionService_CreateInstance`.
Both need a trust-relationship with `apigateway.amazonaws.com`, later we'll add in Lambda as well.
The `DescribeVpcs` role needs to have the `ec2:DescribeVpcs` action, with the `CreateInstance` role needing the `ec2:DescribeVpcs` and `ec2:RunInstances`

That GET method will have the following properties:

| Setting | Value |
|---------|-------|
| Integration | AWS |
| AWS Region | `eu-west-2` _(or your preferred region)_ |
| AWS Service | Elastic Compute Cloud (EC2) |
| AWS Subdomain | _[blank]_ |
| HTTP method | `GET` |
| Action Type | Use action name |
| Action | `DescribeVpcs` |
| Execution role | _[the ARN of the role we created above]_ |
| Content Handling | Passthrough |
| Use Default Timeout | Enabled |
 
If you deploy that however, it'll fail with `The action DescribeVpcs is not valid for this web service.` because the EC2 API is one of the oldest services Amazon offers, and the Version defaults to one that predates VPCs. 


_Posts in this series:_
{% assign posts = site.posts | where_exp:"item",
    "item.tags contains 'series_mgmtondemand'"  %}
{%- for post in posts -%}

* [{{ post.title }}]({{ post.url }})

{%- endfor -%}
