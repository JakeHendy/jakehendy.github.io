---
layout: single
type: posts
title: What does the console actually do?
tags: aws, amazon, api
---

The AWS Console is in my opinion a cornerstone of the AWS ecosystem.  Some laud it's simplicity, some rank it at the bottom for usability.
Undoubtedly, it's an important tool for anyone interacting with AWS whether they're building, maintaining, or learning.

I generally find the AWS Console easy enough to use, whether that's honed from nearly 10 years of using it I'm not sure. Likewise, I feel quite comfortable using the AWS CLI, the official SDKs like `boto3`, or IaC tools like CDK, CloudFormation, or Terraform.
When doing something for the first time I plod around the console to get a feel for timings and seeing it work before taking it to the API (for automation) or IaC (for infra).

AWS is very good at making sure the Service Teams use the same public APIs we all use in the console; there are a few notable exceptions such as Dead-Letter Queue Re-drive in SQS which is a Console-only API. This gives us the familiarity we all expect from AWS and helps them dogfood and keep that customer obsession: if a Service Team can't confidently build using their own APIs and their internal knowledge, how can a customer?

There is, however, one area that I'd like to see AWS improve going forwards, and that's the transition from the console to the API.
If you open the Network panel of your favourite browser's Developer Tools you can watch the requests go out and how the API is used, if you can avoid the plethora of telemetry requests and `List`/`Describe` actions that power the console and keep the user experience.
Otherwise it's down to you to take what you just typed/clicked through and then turn it in to an API call, or even translate it in to IaC.

Depending on your browser, you might have to click around to find the Request Payload like I did in Safari: it's normally a bit easier in Chromium-based browsers.

![A sample of network requests](/images/2023-05-02-what-does-the-console-actually-do/01-devtools-network-overview.png)
![A sample network request for creating an SQS queue](/images/2023-05-02-what-does-the-console-actually-do/02-devtools-sample-payload.png)

## What about the competition?

If we look at a competitor like Azure, after going through the verbose (which admittedly has it's pro's) wizard to launch a Virtual Machine we can download a template for automation. Is it perfect? No, it takes you to another screen to decipher Azure Resource Manager templates but it does give you JSON of the template _and_ JSON of the parameters, a tree view of the JSON model, and a Scripts tab which links you to additional documentation on _scripting_ these templates.

![The end of the Azure Virtual Machine Creation wizard, with an option to view the template](/images/2023-05-02-what-does-the-console-actually-do/03-azure-vm-wizard-overview.png)

Is it pretty? No, it's JSON rather than Azure CLI. Is the UI better? Not massively no, but it's functional. I am not an Azure user, but I roughly know what I'm going to get with that template already. Can I transpose it to Terraform for Azure? Not directly, but I can reference values as necessary.

![The generated Azure Resource Manager template for a sample Virtual Machine](/images/2023-05-02-what-does-the-console-actually-do/04-azure-vm-template.png)

## What would I like?

For some way to see what the API payload is for public APIs, and for private APIs I'd like to be told that it's a private API. I'd like to see this visualised in the console, hidden by default unless necessary. I don't want it to translate it to `boto3` or anything, I'd like to see the JSON payload it just fired. Heck, for those services that still prefer XML like EC2 and SQS I'll take that, too.

I'd like to see this persist for my session, stored in the browser's Local Storage so I can look back at the last few events to see how they replay.

To expose this as an option, I could see it as another icon next to CloudShell to show your API activity.
This could, as a quick example, take you to a new page containing a typical two-pane setup: the left-hand pane with the list of API events, each item has a header with the service name and action and a line underneath of the datetime, and the right-hand pane contains the JSON payload and a link to the API documentation.

## Isn't this CloudTrail?

CloudTrail does indeed record management API activity by default, and you absolutely should get used to using the CloudTrail UI in the console because it is really powerful.
CloudTrail does monitor _all_ API activities, and unless you export (or run CloudTrail lake) you can only put one filter on.

You could be in a shared account with other individuals doing ClickOps, or other automated systems could be manipulating resources too. You're reliant on being able to filter out activity in CloudTrail to find your own, similar to the Network tab, and there's additional data to sort through in the CloudTrail response. Useful data, but remember we want the API action rather than the management event.

My suggestion focuses on developer experience rather than auditing like CloudTrail does: supporting the building and maintenance of infrastructure.

## Who is this for?

I know this isn't a simple feature to implement and of course comes with its own maintenance headaches, but I think a sizeable group would find this beneficial. We've seen a number of community projects spring up around AWS provided content, and I could see this feature providing more: AWS provides the API payload, and a community service (or vendor, like Hashicorp) provides an API Payload to Terraform translation.

There are benefits across the full range of experiences, from those starting out new to AWS wanting to experience the command line, to those familiar with AWS but wanting to automate, to seasoned engineers writing automation against new services.
In fact, I'm pretty sure some elements of the AWS console already have this where you can copy out CLI commands.

I don't think this will be implemented any time soon, but I do hope it makes its way to the browser team as a possibility for a hack day. I'd love to write a bookmarklet/browser plugin to do this I don't have the time (I've had this idea since before re:invent 2022!), and I suspect there's additional security in play which will stop sideloading additional scripts etc. I'm not a front-end developer, so it wouldn't work as well either.
