---
layout: post
title: 24/09's AWS Updates ☁
tags: aws, aws-updates
---

What a wet and miserable morning it is here in Exeter. Here's the past 24 hours worth of what's new updates that may interest my colleagues and I. Well, today's there's only one on the list...

# AWS Lambda supports Custom Batch Windows for Kinesis and DynamoDB event sources
There's another parameter available to fine-tune when your lambda function is invoked for a Kinesis or DynamoDB Data stream. As Lambda (the service) reads at a fixed pace, your record sizes were pretty flexible within the function.
You now have the option of waiting until your batch window has reached its maximum size (up to 300 seconds), your batch count has reached its maximum size (e.g. 100 records), or until the payload size for the record set reaches (an unadjustable size of) 6MB.

Whilst the announcement says you can use this to increase the number of records passed to your lambda (by waiting longer) it could also be useful to have a roughly consistent number of lambda invocations (e.g. once every minute). 

On an unrelated note, I wonder where the 6MB limit comes from, perhaps it's something to do with Firecracker? Time to DuckDuckGo. 
