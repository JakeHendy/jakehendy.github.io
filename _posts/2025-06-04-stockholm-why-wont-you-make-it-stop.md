---
layout: single
type: posts
title: Stockholm? Why won't you make it stop
tags: aws, awsconsole
---

_I'm a little impressed that the Foo Fighters almost sung about this_.

The AWS Console, the ability to control hundreds to thousands of resources across the 27 regions AWS operates in. A single pane of glass for multiple millions of pounds of spending, a UI marvel—at least relative to Microsoft Azure or Google Cloud.

If you've been in the AWS Console recently, in a new account or logging in for the first time in a while, you might have noticed you defaulted to the Stockholm `(eu-north-1)` region.
Even if you typically spend most of your time anywhere else like Ireland or London, or if you're physically located anywhere else; you'll be in Stockholm.

## Why Stockholm

It's an open secret that AWS/Amazon assign codes to their buildings. In fact, it's not a secret, if you look at your favourite Online Map the offices in London have the code on them.

The naming strategy for these is closest major international airport's IATA code and the distance, as the crow flies, in miles. Amazon Shoreditch's code of LHR16 is because it's 16 miles from London Heathrow, which has an IATA code of LHR.

Stockholm's biggest international airport is Stockholm Arlanda, with the IATA code of ARN. See where this is going?

When you log in to an account for the first time, via that identity provider, the AWS User Preference Service has to drop you _somewhere_.

Given that the User Preference Service has a list of all regions, and they're *always* referred to internally by their codenames, that list will be sorted alphabetically. As such, even though you might run workloads in North Virginia or London and only those Tier 1 regions, Stockholm is the first in the list because of its IATA code.

If you've got to pick somewhere to put someone, the place that's first on the list is as good as any, right?

## Could they do this more intelligently?

Now, I don't know this for a fact, but Amazon/AWS values consistency above all else. Customer Obsession is though, a tenet held by all teams.

They could drop you in to the region you're geographically closest to based on your IP address, but with global proxies and networks that's not guaranteed. If you're sat at your desk in Chicago or London you might appear in London, or Chicago, or New York, or Singapore, or anywhere.

You've now introduced inconsistency in to a user's workflow and possibly problems.

> *login for first time in a while*
> Why is this instance running?!
> *shutdown*
> *alarms go off*
> ! Ooops

Could you drop the user to a region with their oldest resource? Could you drop the user to a region with their biggest set of resources?
AWS has no idea what's important to you, and after that first drop the User Preference Service will remember which region you selected last time so it doesn't matter.

The safest, and most consistent option, is to drop the user to a region that's top of the list.

## Foo fighters?

The last verse of _Arlandria_... if we change Arlandria to Arlanda. Of course, the first region that was launched of the _proper_ AWS Network is of course `us-east-1`, (North) Virginia.

> You are not me, Arlandria, Arlandria
> You ain't what I mean, Arlandria, Arlandria
> Oh God, you gotta make it stop
> My sweet Virginia
> Oh God, you gotta make it stop

## How can you tell

Luckily at work, we block most regions since we've no reason to run in them, so nice big red banners appear everywhere and _most_ people twig they're in the wrong region.

If you don't have SCPs kicking you out though, well, here's hoping you don't panic too hard when you see nothing running.
