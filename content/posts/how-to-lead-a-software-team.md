+++ 
draft = false
date = 2025-04-15T21:28:10-04:00
title = "Random Observations Of Software Management"
description = ""
slug = "random-software-leadership-observations"
authors = ["Stephen Heinde"]
tags = ["leadership", "jobs", "management", "interview", "qa", "tools"]
categories = []
externalLink = ""
series = []
+++

# Random Observations Of Software Management

Recently I was applying for a job and I was asked the following question. The response format was free form, so I ended up monologuing a big about a few things I've noticed about software dev and software teams as of late. This was pretty "off the cuff" and written in about 5 minutes, so maybe I'll clean it up later, but I thought it migth be worth sharing. There is definitely a bias here towards pain points I've felt in my role in the last ~3 years.

## "How would you structure a team working on a diverse SaaS product, and why?"

It is important to ensure that your devs are working on the areas that they will excel in. Some devs are better suited for bug investigation and resolution, and some devs are better suited for more open-ended design and greenfield changes. 

Task management is key. A common tasking system must be used, and metrics related to task progress are helpful in understanding a teams shared metrics. Too often, I've seen disparate team members using their own tasking and documentation because it is "what make sense to them". It is critical for a distributed team to agree on and buy into shared project management and documentation tooling. As such, that tooling should be implemented at as minimal of a level as possible to keep the barrier to entry as low as possible. Once the team is bought into the value of the tooling, then expanding it to more complex use cases will be an easier ask if the entire team is engaged and on board with the tools. 

It is also important to leverage strong logging and instrumentation to ensure that service level issues are caught quickly. This can be especially critical if the team is operating in different time zones as you can then rely on the tooling to help report errors so they can be reported and working on ASAP, assuming a high enough level of criticality. 

Having clear and defined test plans is also important . I don't believe that there is a single testing strategy that will guarantee perfect results. I've seen unit testing, integration testing, instrumentation testing, and manual QA all succeed and fail for varying reasons. Like shared documentation and task management, it is important that your team has a QA mindset, whether dev or dedicated QA, and are on the lookout for bugs and thinking through bug scenarios. All that being said, separate independent QA is also extremely valuable as it is very difficult for devs to break themselves out of the dev + test happy path cycle, and while I would push for deeper understanding of QA principles, practically a separate QA individual or team can be immensely valuable. 