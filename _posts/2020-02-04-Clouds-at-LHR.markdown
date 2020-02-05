---
layout: post
title: 04/02's Cloud Landing  ☁
tags: aws, aws-updates
---

HAPPY NEW YEAR! Yes even though it's February... overwhelmed by the re:Invent news, _Clouds At LHR_ returns with a tighter focus. You can also sign up for the newsletter on Tiny Letter; [https://tinyletter.com/CloudsAtLHR](https://tinyletter.com/CloudsAtLHR), or look at the embed form at the bottom of this post. As always you can send feedback to [@JakeHendy on Twitter](https://twitter.com/JakeHendy) or through any other means you have! Perhaps through the [online form](https://forms.office.com/Pages/ResponsePage.aspx?id=DQSIkWdsW0yxEjajBLZtrQAAAAAAAAAAAAMAALQXYjNUMDYyQ0o0MEkyUVIxUFdWNzhSVlZFVVBPUC4u)...

The features today are small, AWS didn't release any updates for a number of days and then a few little ones have trickled out, so I'm expecting a large swathe of updates to be released soon.

## Feature and Service updates

We're talking about advice, storage, and voices today.

### AWS Compute Optimizer Available In London

AWS Compute Optimizer is one of those products that will save you money and Amazon resources. It uses Machine Learning (of course) to analyse the metrics of your instances and suggests different instance families to use. What's more the service is free, you only pay for EC2 and CloudWatch costs; which you were paying for anyway!

Available in London.

### Amazon Polly Launches Brand Voice

Amazon tout that they have over 60 voices in 29 languages available in Polly, but if you wanted something more specific for your brand you can now "engage the Polly team" to build "high-quality Neural-Text-to-Speech" voices to represent your "brand persona". These voices are then exclusively enabled for you. I imagine this is very useful for products and games which want to have a consistent voice across their products; from web to mobile apps to IoT things.
You can even use these voices in your own Alexa Skills and Connect centres.

There's a [companion blogpost](https://aws.amazon.com/blogs/machine-learning/build-a-unique-brand-voice-with-amazon-polly/) which uses KFC on Alexa and National Australia Bank on Connect as examples.

### Cloud9 launches support for tagging new and existing environments

Our cloud estate at the Met Office uses tagging a lot, to make sure that we know who owns and is responsible for service use (and who to charge it to!) so now that you can tag up Cloud9 IDE instances this is very nice.
I'm certain this also lends itself to working with AWS Systems Manager Automations so that you can use Run Command etc across your Cloud9 estate for patching and auditing purposes.

### AWS Storage Gateway is now available on Linux KVM hypervisor

If your organisation wants to use Storage Gateway it might be easier now that you can deploy it on KVM hypervisors on-premise.
There are a few requirements like using Intel processors, _and_ that it supports

> QEMU-KVM on Red Hat Enterprise Linux 7.7, CentOS 7.7, and Ubuntu 18.04 LTS and 16.04 LTS

only, but it's a start. You can use Storage Gateway to access "virtually unlimited cloud storage", providing you have the bandwidth to back it up.

## News and blogs

We're highlighting one of my blogs today because.

### [Bastions on AWS](https://jakehendy.com/2020/01/29/Bastions-on-AWS/)

I wrote a blog post with 4 steps for running Bastions on AWS which allow you to SSH in without ever having to open an instance to the internet.
It's a very loose guide and speaks about the services you want to use rather than step-by-step, but you'll hopefully find it useful all the same!

## TinyLetter signup

<form style="border:1px solid #ccc;padding:3px;text-align:center;" action="https://tinyletter.com/CloudsAtLHR" method="post" target="popupwindow" onsubmit="window.open('https://tinyletter.com/CloudsAtLHR', 'popupwindow', 'scrollbars=yes,width=800,height=600');return true"><p><label for="tlemail">Enter your email address</label></p><p><input type="text" style="width:140px" name="email" id="tlemail" /></p><input type="hidden" value="1" name="embed"/><input type="submit" value="Subscribe" /><p><a href="https://tinyletter.com" target="_blank">powered by TinyLetter</a></p></form>
