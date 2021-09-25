---
layout: single
title: 15/10's Cloud Landing  ☁
tags: aws, aws-updates
---

Good morning! Welcome to the second post in the series that has a name; _Clouds At LHR_. You can also sign up for the newsletter on Tiny Letter; [https://tinyletter.com/CloudsAtLHR](https://tinyletter.com/CloudsAtLHR), or look at the embed form at the bottom of this post. As always you can send feedback to [@JakeHendy on Twitter](https://twitter.com/JakeHendy) or through any other means you have!

So with no updates applicable to LHR yesterday today—much like the weather in Exeter—isn't looking much more glamorous 🌫🌨 😒

# QuickSight announces Data Source Sharing, Table Transpose, and new filtering and analytical capabilities
Lots of little quality of life updates for QuickSight today.
You can share the data sources across users and groups like you can share data sets, analyses, and dashboards. This can be particularly useful when sharing custom SQL data sets, allowing co-owners to adjust and improve the SQL and results returned in one place.
Data Source sharing is available for all types except S3 Analytics and File-based data sets

You can transpose rows and columns on table charts allowing you to generate and visualise different views of the same data.

SPICE dashboards now support wildcard filters (`contains`, `starts with`, `ends with`, and `equals`), string functions (`toString`, `parseDecimal`) and new date functions (`parseDate`, `formatDate`).

Aggregations are now possible using Nth percentile, median, and standard deviation too!

All available in London, how could you possibly not make beautiful dashboards with all of the above?

# Redshift Inter-Region snapshot transfer performance improved
If your RTO and RPO policies weren't aggressive enough, you can make the _orders of magnitude_ more aggressive as transfer rates across regions of snapshots has been observed at speeds of *40,000 MB/s*. Yes, _megabytes_. 

Redshift Snapshots are created and stored on S3 every 8 hours (for active clusters) or when the amount of data equivalent to 5 GB _per node_ has changed. These snapshots can also be created cross-region, copying incremental changes to a secondary region.
It's now even easier to have a cross-region data warehousing solution at not-massively-higher costs.

All you need is v1.0.2762 or higher, and you're good to go!

# CodePipeline enables setting environment variables on CodeBuild build jobs. 
Your CodeBuild job's environment variable can now have variables set via CodePipeline. Rather than setting the variables in the project's configuration or the buildspec file, you can now set them dynamically with some JSON.
Both plain text and Parameter Store value types are accepted, so you can set secret values within your CodeBuild jobs too. 
This will allow you to simplify your build jobs, allowing you to reuse them for multiple environments (i.e. dev, staging, production) knowing the exact same steps are being performed. 

A great example (and one my team and I will hopefully have running soon) will be combining with CDK. Your CDK apps can be dynamic enough to understand the target environment, so using the same environment variables across your CodePipeline means the synthesise of CDK templates and building your code can all be done in one step. Perfect for monorepos!

That's all for today, hopefully we'll see you tomorrow :) 

# TinyLetter signup

<form style="border:1px solid #ccc;padding:3px;text-align:center;" action="https://tinyletter.com/CloudsAtLHR" method="post" target="popupwindow" onsubmit="window.open('https://tinyletter.com/CloudsAtLHR', 'popupwindow', 'scrollbars=yes,width=800,height=600');return true"><p><label for="tlemail">Enter your email address</label></p><p><input type="text" style="width:140px" name="email" id="tlemail" /></p><input type="hidden" value="1" name="embed"/><input type="submit" value="Subscribe" /><p><a href="https://tinyletter.com" target="_blank">powered by TinyLetter</a></p></form>
