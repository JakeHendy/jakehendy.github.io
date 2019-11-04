---
layout: post
title: 04/11's Cloud Landing  ☁
tags: aws, aws-updates
---

Good morning! Welcome to the seventh post in the series that has a name; _Clouds At LHR_. You can also sign up for the newsletter on Tiny Letter; [https://tinyletter.com/CloudsAtLHR](https://tinyletter.com/CloudsAtLHR), or look at the embed form at the bottom of this post. As always you can send feedback to [@JakeHendy on Twitter](https://twitter.com/JakeHendy) or through any other means you have!

We're wrapping up several days worth of updates here. Amazon are really pushing the developer assistance front, with CodeStar helping to generate more production-ready apps, EMR notebooks supporting Git integration, and Amplify making it easier to integrate Authentication, Authorisation, and Accounting inside your Amplify applications. Alongside that there's updates for the AWS for Wordpress plugin, some IoT updates, Chime, and more.
There's 3 decent blog posts at the bottom of this edition, where we look at the AWS for Wordpress plugin allowing you to add a CloudFront distribution, how it's now much easier to get started with Lambda applications, and again using Amplify for that AAA integration. 

Grab your coffee/tea/cold-drink/snacks and enjoy!

## Feature and Service updates

The latest feature and service updates that are either juicy, in Ireland or London, or all 3/4!

### CodeStar supports toolcahin setup with CloudFormation

You can now create CodeStar projects using CloudFormation, backed by CodeCommit or GitHub repositories.
CodeStar can configure the CloudFormation templates for you, enabling you to move from a point-and-click build style to production usage very quickly. Have a [goosey-gander through the documentation](https://docs.aws.amazon.com/codestar/latest/userguide/transition-project-prod.html) for more information. 

### EMR Notebooks supports git-based repositories and JupyterLab

Sounds [familiar right](https://jakehendy.com/2019/10/09/AWS-Updates/#sagemaker-notebooks-now-support-diffing)?
Associate git repositories with your EMR Notebooks and better collaborate to take advantage of your EMR clusters.
The Git integration goes so far as to include clone, push, and merge support including the `nbdime` tool to help you diff.
Additionally, when you now launch a Notebook you can launch it in Jupyter or JupyterLab.
Available in London and Ireland!

### ElastiCache supports modifying auth tokens

Set and rotate your authentication tokens (aka a _password_) on a live cluster serving requests, as of Elasticache for Redis 5.0.5.
You can add new tokens to existing encryption-in-transit clusters that didn't have auth tokens configured, as well as modify those active tokens whilst being used.
Aavailable everywhere except Osaka and China, for some reason.

### Secure Elements in Amazon FreeRTOS

FreeRTOS 201910.00 features enhanced support for Secure Elements. Two reference integrations have been qualified using the IoT Device Tester for Amazon FreeRTOS.
To quote the news release:

> [The] first, the [Amazon FreeRTOS windows simulator implementation is connected to the Microchip ATECC608A](https://docs.aws.amazon.com/freertos/latest/userguide/getting_started_ecc608a.html) secure element and the second is the [Infineon XMC4800 IoT Connectivity Kit with OPTIGA Trust-X](https://docs.aws.amazon.com/freertos/latest/userguide/getting_started_infineon_trust_x.html).

### AWS for WordPress plugin is now available

The Amazon Polly and Amazon AI plugins and been renamed to the AWS for WordPress plugin, which now features a workflow to create a CloudFront distribution.
That CloudFront distribution has been optimised by AWS engineers for WordPress sites; utilising various cache behaviours as appropriate. 
The plugin is free to download, with an accompanying blogpost, which we will summarise and review below!

### Amazon Chime now supports an in-room experience on Dolby Voice Room

"Alexa, start the meeting" you whisper and the meeting starts in crisp clear audio.
Amazon Chime with Alexa for Business provides you an _integrated room experience_ with Dolby Voice Room; allowing you to share content, get a visual roster, and use _enhanced whiteboard features_.
Available everywhere that has a Dolby Voice Room setup, (anyone?)

### Create Serverless Applications from the AWS Lambda Console

When you're interested in prototyping your Lambda applications, bootstrapping can be a real pain. Now, with the Lambda console you can make use of quick start templates that include source repositories as well as build, package, and release pipelines.
Available in London and Ireland, alongside another blogpost we will summarise below!

### New AWS Deep Learning AMIs; Ubuntu 18.04, Elastic Fabric Adapter, PyTorch 1.2, MXNet 1.5.0

The Deep Learning AMIs are now available on 18.04 in addition to Ubuntu 16.04, Amazon Linux 2, and Amazon Linux.
The AMIs now come with PyTorch 1.2, MXNet 1.5.0, and support for Elastic Fabric Adapter; the high-performance inter-node connection framework.

### Secrets Manager supporst larger secrets, resource policies, and request rate

Store secrets up to 10Kb in size in Secrets Manager today!
Interestingly, your resource policies can be up to 20 Kb in size; which means your access control can be even more verbose and complex as you need it to!
Probably the biggest part of this announcement is the default quota of 1,500 requests per second to the GetSecretValue API.
No further action is required for you to take advantage of these new features!

### Amplify CLI helps you create and manage permissions and user management with Cognito

Amplify CLI can now create Cognito User Pool Groups and configure fine-grained permissions on those groups to access S3, API Gateway endpoints, DynamoDB tables and more.
For users that are part of more than one group you can set a precedence order for those groups, so users are granted the right set of credentials.

You can also now add a User Management solution to your app with the CLI, which creates an API Gateway and associated lambdas to configure as appropriate.
There's _another_ blog post available which we will summarise below!

### AWS IoT Device Tester v1.5.0 for Amazon FreeRTOS

The latest version of Device Tester now supports FreeRTOS 201910.00, enabling you to qualify your secure elements to the AWS Device Catalog 
There are also improvements to SecureSockets and WiFi test groups, providing an ability to configure the preferred port for the Echo server.
Available now!

### Service Catalog enables transfer of provisioned product ownership

If your teams or their makeup change, you can now transfer the responsibility for provisioned Service Catalog products to new members or roles, providing they're within your organisation. You can also see the complete ownership history of products so you to monitor and audit the ownership of those products throughout their lifecycle. 
Available everywhere Service Catalog is available!

### Embed AppStream 2.0 streaming sessions in websites

Yes, you can embed desktop applications within an `iframe` on your websites with the AppStream 2.0 EmbedJS SDK. You can show or hide AppStream 2.0 options, or the entire session toolbar, and register event callbacks for session state changes or to end the session programatically.
Available everywhere AppStream 2.0 is, so Ireland but not London... 😒

### S3 Inventory reports Intelligent-tiering tier

Inventory can now report the actual tier of objects stored with the Intelligent-Tiering storage class.
Using this feature you could for example see how data moves between the Frequent and Infrequent storage tiers when assigned to the Intelligent Tiering storage class.
These reports are available as CSV, Apache ORC, or Apache Parquet output files; on a daily or weekly basis.
Available everywhere!

## News and blogs

From the introduction we have 3 interesting blog pieces here.

### [Self-hosting Wordpress](https://aws.amazon.com/blogs/networking-and-content-delivery/accelerating-wordpress-with-cloudfront-using-the-aws-for-wordpress-plugin/)

An interesting post covering a brief history of WordPress, the AWS plugins for WordPress, and a tutorial for setting up CloudFront and Amazon Lightsail.
The new plugin works for Lightsail, EC2, and even sites hosted on WordPress.com, though one supposes that you won't need CloudFront if you're using WordPress.com.
The walkthrough is by itself simple to follow and demonstrates that the plugin does a lot of the heavy lifting for you, but there is some setup you must do.
Included towards the end though is a step regarding the [Mozilla Observatory](https://observatory.mozilla.org/) to score and understand how to improve the security posture of your site, then with a small additional guide on how to get a better score too. To me, these things make a difference when people try to self-host as it improves security (or at least, security awareness) for everyone.
If you're in UK Public Sector, don't forget there is [NCSC Active Cyber Defence Web Check](https://www.ncsc.gov.uk/section/products-services/active-cyber-defence#section_2) which you should take advantage of!

### [Getting started with AWS Lambda](https://aws.amazon.com/blogs/compute/improving-the-getting-started-experience-with-aws-lambda/)

Lambda is such a simple service, especially for point-and-click go experiments. When those experiments start to grow however, or you know that your experiment will be the foundation of an operational service, then a quick prototype can be quite daunting with setting up a code repository, publishing etcetera.
The Lambda Console now supports a much better Getting Started experience, enabling you to get a code repository, Continuous Delivery/Integration pipelines and more out of the box from the console.
Eric's post here walks you through creating one of those Serverless Applications, and a testament to the quality of the service as the post is rather short!
_Editor's Note: This was posted on October 3rd, but I missed it then and it's been rolled out to many regions since then_

### [Amplify enables Cognito User Group management](https://aws.amazon.com/blogs/mobile/amplify-cli-enables-creating-amazon-cognito-user-pool-groups-configuring-fine-grained-permissions-on-groups-and-adding-user-management-capabilities-to-applications/)

I remember using the AWS API Gateway Portal reference implementation to set up a simple user->API Key management portal for a service a couple of years back.
It was relatively simple, but User Authentication, Authorisation, and Accounting (AAA) has always been one of the scarier topics of my career so far.
Amplify's attempt here to categorise applications and services really helps assuage these concerns, and this new feature really helps.
The post walks you through creating a new app and adding AAA to it. There are less steps involved with creating whole new functionality for your application than adding a CloudFront distribution to your WordPress site.
Amplify is developed in the open, so expect to see security and tooling improvements (to name but a few) work their way in as either Pull Requests or Issues/RFCs very soon. 


## TinyLetter signup

<form style="border:1px solid #ccc;padding:3px;text-align:center;" action="https://tinyletter.com/CloudsAtLHR" method="post" target="popupwindow" onsubmit="window.open('https://tinyletter.com/CloudsAtLHR', 'popupwindow', 'scrollbars=yes,width=800,height=600');return true"><p><label for="tlemail">Enter your email address</label></p><p><input type="text" style="width:140px" name="email" id="tlemail" /></p><input type="hidden" value="1" name="embed"/><input type="submit" value="Subscribe" /><p><a href="https://tinyletter.com" target="_blank">powered by TinyLetter</a></p></form>
