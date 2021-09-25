---
layout: single
title: 03/10's AWS Updates ☁
tags: aws, aws-updates
---

_A lookback of the past 24 hours of updates from AWS, applicable to my x-gov colleagues and I with the occasional interesting piece thrown in._

Rather niche updates coming out today, but for those they apply to they should be good quality-of-life upgrades. Let's begin!

# Amplify CLI simplifies starting work on existing projects and CLI plugins
Amplify is a nice service that allows you to build "cloud-enabled mobile and web applications", one of the components within is a nice toolchain to "create, integrate, and manage the AWS cloud services for your application".
From today, the CLI now has a single command to clone the git repo, deploy the backend and configure the frontend (web, iOS, and Android supported) to use said backend. Web applications will then be launched in to your default browser too. Your getting started guide can now be condensed nicely to `amplify init --app [url_to_repo]`.

On the back of this you can now easily extend the Amplify CLI, using `amplify plugin init`. Add additional commands, events, and configuration for your plugin.

There's a nice [blog post that accompanies this feature release](https://aws.amazon.com/blogs/mobile/amplify-cli-adds-scaffolding-support-for-amplify-apps-and-authoring-plugins/) for Amplify, I think I'll be getting started with it very soon... 

# AWS Thinkbox Deadline 10.1 released, with performance enhancements and ease-of-use improvements
"Scale bigger and faster than ever to complete your projects", with the new release of Thinkbox Deadline 10.1
SideFX Houdini can be used in AWS Portal, usage-based licening for Houdini Engine is available on Thinkbox Marketplace. Modo 13 support with updated submitter, and a number of updates to plugins for Maya, Octane, Cinema 4D, Nuke, ftrack and more. 

Licening for Deadline is also simplified, there's no upfront payment required and Deadline will automatically detect if it's running on AWS and as such no longer require any licening setup. 

On a (more) technical note, Deadline leverages .NET Core everywhere for Windows, Linux, and MacOS; removing the Mono dependency. Deadline now standardises on .NET Core, "enabling more frequent updates with the latest perforamnce and security improvements".

# AWS Certificate Manager Private Authority includes 9 certificate templates
AWS Certificate Manager Private Certificate Authority (ACM Private CA) has additional templates to control/specify which X.509 certificate extensions are in play for the certificates issued with Private CA.
These extensions include signing code and OCSP responses, client-only or server-only TLS certificates. 
_Shame it still costs $600 a month..._

# Industrial Software Consulting Partners
If you work in process and discrete manufacturing and want to move to AWS, there are now 10 APN Premier and Advanced Consulting Partners as part of the Industrial Software Competency Program, featuring the ones you'd expect like Accenture, Capgemini and WiPro. Take a look at the [APN Blog post](https://aws.amazon.com/blogs/apn/introducing-the-aws-industrial-software-competency-program/) to find out more.

# Amazon Lightsail now provides automatic snapshots
Schedule daily snapshots of your Lightsail Linux/Unix instance at a time you specify, and Lightsail will kepe the seven most recent snapshots. You can use these snapshots to restore an instance to a previous state as well as create new instances that are almost-perfect replicas of the original. 
The feature is free, but you pay for the storage ($0.05USD per GB per month) of those automatic snapshots. Additionally, you can choose to keep automatic snapshots for as long as you wish and continue to take manual snapshots. Lightsail also features de-duplication so successive snapshots only contain the data that's changed from the previous one.

# ECS now supports IntelliSense in VS Code
If you use VS Code (why wouldn't you?) to write your ECS Task Definitions, you're in luck as there is now IntelliSense support to help you reduce the copious manual typing and catch those easy-to-miss errors.
If you're using the VS Code toolkit for AWS with auto updates enabled you should receive this update shortly. Then, follow the [step by step guide](https://docs.aws.amazon.com/en_pv/toolkit-for-vscode/latest/userguide/ecs-definition-files.html) to how to best make use of it. If you don't have the toolkit, there's a simple guide to [install it from the VS Code toolkit homepage](https://docs.aws.amazon.com/toolkit-for-vscode/latest/userguide/setup-toolkit.html).
For reference purposes there is a [list of parameters supported](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task_definition_parameters.html) today, which will be expanded upon in the future. 
