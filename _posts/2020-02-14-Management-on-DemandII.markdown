---
title: Management on Demand II
tags: aws, architecture, series_mgmtondemand
---

To make up for this shortfall in the EC2 API we're going to use lambda to do the heavy lifting for us.
We're going to start with a simple API Gateway which returns a JSON array of objects detailing the VPCs in a given region, defaulting to `eu-west-2`:

```
GET /information/vpcs
```

```json
{
    "region": "eu-west-2",
    "vpcs": [
        {
            "id": "vpc-xxxxxxx",
            "name": "TheBestVPC"
        }
    ]
}
```


The [EC2 DescribeVpcs][EC2DescVPC] gives us all of this with pagination if required, so this lambda should be nice and simple.


_Posts in this series:_
{% assign posts = site.posts | where_exp:"item",
    "item.tags contains 'series_mgmtondemand'"  %}
{%- for post in posts -%}

* [{{ post.title }}]({{ post.url }})

{%- endfor -%}
