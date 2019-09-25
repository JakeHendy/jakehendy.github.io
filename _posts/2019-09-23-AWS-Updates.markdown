---
layout: post
title: 23/09's AWS Updates ☁
tags: aws, aws-updates
---

Here's the roundup of AWS updates from the past 24 hours that are most applicable to my cross-government colleagues and I, with occasionally an interesting one thrown in. 

{:toc}

# New G4 instance family launched!
There's a new G4 instance family available, featuring nVidia T4 Tensor cores. If it's anything like the GTX RTX launch we saw several months ago these promise some good performance improvements for your graphical applications, and the improvements for your ML workloads should be significantly higher. Plus, they're available in London! 💯

# New DISA-STIG compliant Windows Server AMIs
If you need to run out-of-the-AMI secure instances (you always make sure they're well configured after don't you?) then these AMIs are for you. There's 6 new AMIs; supporting 2019, 2016, and 2012R2. 

# Redshift announces automatic workload management and query priorities
Redshift can now utilise some ML magic ✨ to maximise query throughput by dynamically managing memory and concurrency. Create a new parameter group and you too can start saying you use ML within your workflows. 
Redshift also supports assigning a priority to your queries now, where Redshift will ensure higher-priority queries will get the most amount of resources, even when executing hundreds of queries. 

That's all for today, let's see what tomorrow brings...
