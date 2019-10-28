---
layout: post
title: 28/10's Cloud Landing  ☁
tags: aws, aws-updates
---

Good morning! Welcome to the sixth post in the series that has a name; _Clouds At LHR_. You can also sign up for the newsletter on Tiny Letter; [https://tinyletter.com/CloudsAtLHR](https://tinyletter.com/CloudsAtLHR), or look at the embed form at the bottom of this post. As always you can send feedback to [@JakeHendy on Twitter](https://twitter.com/JakeHendy) or through any other means you have!

Hey it's Monday again! Which means it's time for fun with more updates from AWS. We've got some authentication bonuses, a nice Alexa for Business feature, including our Australian friends in the real-time speech-to-text fun, and more! 

Grab your coffee/tea/cold-drink/snacks and let's ease ourselves in, it is Monday afterall!

## Feature and Service updates

The latest feature and service updates that are either juicy, in Ireland or London, or all 3/4!
### Elastic Inference Accelerators now with 8GB of memory

A new series of Elastic Inference Accelerators have been announced, known as _EIA2_. _EIA2_'s can have up to 8GB of GPU memory, double the previous limit.
Accelerators can be attached to any EC2, SageMaker instance, or ECS task to reduce the cost and complexity associated with deep-learning tasks, with some cost savings up to 75%!
These EIA's support TensorFlow, Apache MXNet, and ONNX models; more frameworks are on the way soon!
Available in Ireland

### "Alexa, I'm running late"

Ever been sat in a meeting wondering why the chair isn't there? If you use Alexa for Business in your org, you can now receive notifications from people when they're running late, along with an ETA. I imagine this can be useful in setting expectations (let's just cancel the meeting) but also to help wrap an over-running meeting up...
The notification comes as an email, rather than announcing it to a meeting room as well.
Whilst this feature hasa gone live in the US I'm sure it'll run through to other regions soon, and it does require the same tight integration with Office 365/Outlook, Gsuite or Gmail, or iCloud. However, it works with Alexa on your desk, the Alexa app, or [Echo Auto](https://www.amazon.com/dp/B07VTK654B).
_Interesting..._

### AWS licence Manager better discovers Windows and SQL licences

Licence Manager can now determine which instances are licenced using BYOL or the Amazon-provided licences, for Windows Server Datacenter, SQL Server Enterprise, SQL Server Standard, and SQL Server Web edition.
Don't forget you can manage your on-prem licences too, not just those in AWS. Licence Manager runs at no extra cost!

### Transcribe supports Australian Speech-to-Text in real-time

Alongside British English and American English, Transcribe supports Australian English in real time as well!
You may need a second service of course; you know, to turn those words round the right way... 

### ECS Service Patterns are now generally available in the CDK

With the new Cloud Development Kit growing (we're using it for our service and it's _fantastic_) it's easy to find services where it's not as fully fledged as others. Cross ECS Services off that list, as new constructs have been released.
There are [ECS Examples available](https://docs.aws.amazon.com/cdk/api/latest/docs/aws-ecs-readme.html) on the reference page. Additionally, I'll be writing a blog post soon on our journey to adopting the CDK across several of our platforms, so stay tuned!

### AWS SSO supports MFA with apps

Initialism soup right there, but SSO now supports authenticator applications such as Authy and Google Authenticator (other authenticator apps are available, like Microsoft!) to generate TOTP codes. This can be mandated for logins, and is smart enough to understand when the context changes such as from a new network or geographical location; reducing the burden to login during standard practice.
Adminstrators can adminstrate all MFA functions through the SSO portal, as well as enabling users to self-enroll within their SSO User Portal.
See the [MFA documentation](https://docs.aws.amazon.com/singlesignon/latest/userguide/enable-mfa.html) to understand if/how you can take advantage.

## News Releases

There are no news releases at this point, but check back again soon to see what we have in store!

## TinyLetter signup

<form style="border:1px solid #ccc;padding:3px;text-align:center;" action="https://tinyletter.com/CloudsAtLHR" method="post" target="popupwindow" onsubmit="window.open('https://tinyletter.com/CloudsAtLHR', 'popupwindow', 'scrollbars=yes,width=800,height=600');return true"><p><label for="tlemail">Enter your email address</label></p><p><input type="text" style="width:140px" name="email" id="tlemail" /></p><input type="hidden" value="1" name="embed"/><input type="submit" value="Subscribe" /><p><a href="https://tinyletter.com" target="_blank">powered by TinyLetter</a></p></form>
