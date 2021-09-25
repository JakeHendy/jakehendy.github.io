---
layout: single
title: A whale in the alpine forests...
tags: docker, alpine
---

It all started on a bright Friday afternoon, I'd seen [Jess Frazelle](https://blog.jessfraz.com/)'s post about closing pull requests/patch requests when they're just not quite right (_[The Art of Closing](https://blog.jessfraz.com/post/the-art-of-closing/)_, well worth a read) and I ended up landing on the _[Ultimate Linux On The Desktop](https://blog.jessfraz.com/post/ultimate-linux-on-the-desktop/)_ post, which in turn led me to the presentation. This presentation contains a screenshot on slide 73 where I spotted the phrase "gitiles"... I've wanted to put up an instance of gitiles at work for ages since I browsed the [Chromium repo](https://chromium.googlesource.com/chromium/src.git) but in the brief few minutes I played with it I couldn't really find a great way to get it worked. When I saw the repo full of `dockerfiles` and gitiles being one of them, my mind 

My interested was piqued and I pinged Jess a few questions. I carried on with my work (mmmm the smell of freshly baked JIRA tickets) and then tonight whilst my girlfriend showered and wrapped up ~~some~~ quite a lot of presents my investigations began.

# A whale appeared, but how?

My Surface was playing up after various upgrades from Windows 8 to 8.1 to 10, and hadn't updated to 1709 (nor the various Insider builds). After 2 dead memory sticks and some faffs I'd restored it, and with a clean build I decided to take the plunge and install docker. Why wait until now? I'd been reluctant to use docker because I read The HFT Guy's _[Docker in Production: A History of Failure](https://thehftguy.com/2016/11/01/docker-in-production-an-history-of-failure/)_ and as we'd been using Lambda's/Elastic Beanstalk at work (more on that in a later post) I decided we'd (in my team) containerise by using AMIs etc. 

After talking to [Mark Thebault](https://twitter.com/markthbt) with him showing me how easy docker was to use, I decided to turn the leaf over...

# But how is it in the Alpine forest?

Jess' Gitiles dockerfile uses Alpine Linux and it just makes for a nice title.

# So how'd it go?

Really well, except for some reason docker decided not to download any images. A restart of docker and then we're sorted.
First command:

```
docker run r.j3ss.co/gitiles
```

No ports assigned, but hey look it started, that's nice...

```
docker run -p 8080:8080 r.j3ss.co/gitiles
```

Hey I can connect to it, but `/home/git` doesn't exist.

In a new PowerShell session:
```
PS C:\jake.hendy\Dev> docker exec d6ce73 "ls"
bin
dev
etc
home
lib
media
mnt
proc
root
run
sbin
srv
sys
tmp
usr
var
``` 

Hmmm...
```
PS C:\jake.hendy\Dev> docker exec d6ce73 "ls /home/"

oci runtime error: exec failed: container_linux.go:265: starting container process caused "exec: \"ls /home/\": stat ls /home/: no such file or directory"
```

Okay? 

```
PS C:\jake.hendy\Dev> docker exec d6ce73 "ls /"
oci runtime error: exec failed: container_linux.go:265: starting container process caused "exec: \"ls /\": stat ls /: no such file or directory"
```
Guess I can't `cd` or `ls` around, it's my first time with Alpine Linux. 
At this point I start to wonder how I'm going to get the git repositories in the magical `/home/git`...

I remember now I can mount docker volumes and directories etc!
```
PS C:\Users\me> docker run -p 8080:8080 --mount source=C:\jake.hendy\Dev,target=/home/git r.j3ss.co/gitiles

C:\Program Files\Docker\Docker\Resources\bin\docker.exe: Error response from daemon: create C:\jake.hendy\Dev: "C:\\jake.hendy\\Dev" includes invalid characters for a local volume name, only "[a-zA-Z0-9][a-zA-Z0-9_.-]" are allowed. If you intended to pass a host directory, use absolute path.
```

What? After some googling, I try the shorthand

```
PS C:\Users\me> docker run -p 8080:8080 -v C:\jake.hendy\Dev:/home/git r.j3ss.co/gitiles

C:\Program Files\Docker\Docker\Resources\bin\docker.exe: Error response from daemon: driver failed programming external connectivity on endpoint clever_perlman (658564367b7f47780362728203b1be5b2c3d4de8b2571e56555f6accd335dbc2): Bind for 0.0.0.0:8080 failed: port is already allocated.
```

Oooh there's another container running! How do I kill again? Oh yeah, `docker kill`.

```
CONTAINER ID        IMAGE               COMMAND               CREATED             STATUS              PORTS                    NAMES
25e30ee2c555        r.j3ss.co/gitiles   "/usr/bin/start.sh"   8 minutes ago       Up 8 minutes        0.0.0.0:8080->8080/tcp   heuristic_lovelace
97b765b50cb2        r.j3ss.co/gitiles   "/usr/bin/start.sh"   2 hours ago         Up 2 hours                                   blissful_babbage
PS C:\Users\me> docker kill 25e
25e // boom...
PS C:\Users\me> docker kill 87b7
Error response from daemon: Cannot kill container: 87b7: No such container: 87b7 // Why can't I type
PS C:\Users\me> docker kill 97b7
97b7 // BOOM
PS C:\Users\me> docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
PS C:\Users\me> docker run -p 8080:8080 -v C:\jake.hendy\Dev:/home/git r.j3ss.co/gitiles
[main] INFO org.eclipse.jetty.util.log - Logging initialized @305ms
[main] WARN org.eclipse.jetty.server.handler.ContextHandler - Empty contextPath
[main] INFO org.eclipse.jetty.server.Server - jetty-9.3.17.v20170317
[main] INFO org.eclipse.jetty.server.handler.ContextHandler - Started o.e.j.s.h.ContextHandler@39c0f4a{/+static,null,AVAILABLE}
[main] INFO org.eclipse.jetty.server.handler.ContextHandler - Started o.e.j.s.ServletContextHandler@1794d431{/,null,AVAILABLE}
[main] INFO org.eclipse.jetty.server.AbstractConnector - Started ServerConnector@fcd6521{HTTP/1.1,[http/1.1]}{0.0.0.0:8080}
[main] INFO org.eclipse.jetty.server.Server - Started @688ms
// BOOOOOOOOOMM!!!
```

![Screenshot of the repositories](https://pbs.twimg.com/media/DQjbbsBX4AESP3c.jpg:large).

I even cloned down my blog (fresh laptop...) to see if it was also shown and it was. 

I'm looking forward to playing with this at work, and will blog my adventures shortly... alongside me playing with some kubernetes...