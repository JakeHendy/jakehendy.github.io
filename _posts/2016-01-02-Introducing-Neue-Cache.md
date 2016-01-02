---
layout: post
title: Introducing Neue Cache
---

What do we all love? A new framework! Here's the obligatory [xkcd](https://xkcd.com/927/) to go with it.

# Why oh lord did you write a new framework?
Like all frameworks, there are many caching frameworks out there. Normally, I'd use a Guava [LoadingCache](http://docs.guava-libraries.googlecode.com/git/javadoc/com/google/common/cache/LoadingCache.html), but there's some times when that doesn't quite give you what you want, like:

- If a subsequent update of an item fails, give me the stale item. It may be stale, but that's cool. If that item doesn't exist in the cache and the first fetch fails, return null -- I asked for potentially stale items!
- Expiration based on time. Time is the most popular way to expire an object, in some cases though I can think of a polling mechanism which would be better.
  
    Assuming that the object is already in the cache, we could poll our backing store (database, microservice, file...) and act on that. Say your backing store is a RESTful microservice -- you could poll that 
