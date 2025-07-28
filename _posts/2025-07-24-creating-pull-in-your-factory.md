---
layout: post
title:  "Creating pull in your factory"
date:   2025-07-24 21:00:00 -0500
categories: shop-floor
---

<iframe data-testid="embed-iframe" style="border-radius:12px" src="https://open.spotify.com/embed/episode/14Nbr9nPnIhBYsYlXJY3xI/video?utm_source=generator" width="624" height="351" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

# Summary

I've summarised the relevant parts of the talk into these sections.

1. **8 Wastes, Unevenness and Overburden** What these were to a QA inspection process and what the SPC chart looked like.
2. **Stabilizing Fluctuations** This was about adhering to already existing standards.
3. **Reducing Fluctuations** This was about introducing changes to the process using PDCA.
4. **Pull Systems** Using Git as a Kanban bin system where each bin is a git commit.
5. **CONWIP** Using a Kanban board and introducing WIP limits.
6. **Levelling systems** Finding the right mix of new features and prod bugs to work on weekly.

# 8 Wastes, Unevenness and Overburden

To Toyota this is the order of importance:
1. Overburden: Asking too much of people.
2. Unevenness: Fluctuations in people and processes.
3. Waste

The way it's seen is overburden causes unevenness which in turn causes waste.
Eliminating waste needs unevenness addressed which needs overburden addressed.

Waste is easy to see, you only need to observe a process once.
Fluctuations (unevenness) are harder, you need to observe the process at least once.
The people who know the fluctuations best are the ones on the shop-floor.

> **NOTE:**  
>
> Overburden was caused by having too many specialists and not enough generalists or full-stack testers.
> This caused fluctuations in people's utilization in the form of the famine/feast cycles that sometimes appeared.
> I mapped the 8 wastes to the QA inspection process [here][1]:
>
> Studying the fluctuations was where [SPC][2] came in; I wanted the process of inspection under statistical control. 
> I wanted to reduce the occurrence of last minute high priority defects which have very little time to be fixed by devs and re-tested by my team.

# Stabilizing Fluctuations

The first goal is to stabilize production by reducing fluctuations.
Questions to ask are:
1. Are the machines stable?
2. Are work-standards good? Do they exist? Do people know to use them? 

Sometimes there's so much fire-fighting. 
It's like you can't stop to sharpen the axe because you have so many trees to fell.
If you're in a burning house, having a fire-fighter is nice but even better is to not have a burning house.
Rewarding only the fire-fighters can create career arsonists.
Reward the fire-safety inspector as well.

Overburden is a lack of safety; folks get hurt and then they slow down.
First identify where are things going wrong, you'll need some sort of data
Once you have data, do this
1. Prioritize where to start.
2. Estimate the effort and impact.
3. Pick a low impact problem.
4. Work on ones that give you success stories.

Even for someone on the shop-floor, it's hard to watch and do a task at the same time; you're too close to the problem to see it.
You can actually notice but it doesn't mean you can make the connection about what's causing it.
Management needs to get rid of the cause.

> **Note:**  
> The tree analogy reminds me of [the cart with square wheels comic](https://www.linkedin.com/pulse/thanks-we-too-busy-daniel-white/)  .
>
> Questions I asked:
> 1. Is the test automation stable? Are the environments?
> 2. Are there work-standards for writing tests? Are they effective, can someone execute tests written by someone else? Can you pair up basically.
> 
> How to free-up the time of an [overburdened tester who's busy][11] with their own work or helping put out fires? One way is by adhering to standards.  
> If I wanted those who were free to be able to swarm to reduce the load on one tester, there had to be a test writing standard that would allow this.
> Other times, a non-SME would use Robot-Framework to automate the tasks for a SME.
> This is where the ubiquitous language came in; it was to [standardize work][3] and then reap the benefits.  
>
> Finding an overburdened tester is easy, they'll be falling behind schedule.
> The overburden caused by lack of safety to me was psychological safety.  
> There was this culture that the good testers find bugs and so they'd keep increasing the scope of testing till they found some afraid that not finding any reflected poorly on them.
> Only management (I) could change that.  

# Reducing Fluctuations

You can't get rid of fluctuation but it can be reduced with PDCA. 
In Western companies, it's little planning, lots of doing, then even less checking and acting (sharing).

At Toyota, there's huge emphasis on plan, way more than half. 
They try to understand what's happening, with who, when. 
You need to stratify the problem, make a prioritised problem.
Multiple factors might contribute to quality problems but pick the one that has the biggest impact.
Now that you know the problem, what's the root cause? Is it a process, worn-out tool, a setting?
Sometimes you use the fishbone diagram or a mind-map.
Develop multiple root-causes.
In the Western world, the minute you find a root cause, there's a rush to solve that.
In Japan, for each root cause you ask this about the solution: 
1. Is it effective, 
2. Is it safe, 
3. Is it cost effective
4. How fast can you do it
5. How much effort to do that.

Then finally you get to the D in PDCA.
Then check if it's gone or only gone when no manager is looking. 
If it's gone, then share the fix with others, that's the act part.
Sharing at Toyota is done by uploading their A3 to a common database so that their employees can Google that.
If it's not gone, restart the PDCA.

> **Note:**  
> Stabilizing the fluctuations by standardizing work to me was different from reducing them through PDCA.  
> Standardizing didn't need me to change anything like the PDCA cycles did.  
> The former was easier than the latter because introducing something new has more resistance to it.
>
> To me the first goal was to reduce common cause variation through PDCA cycles.
> Each week [I met with everyone on my team for 1:1][4] to ask what's bugging them so we can fix it.   
> Together we'd come up with an [Kaizen][5] which was either a [Jidoka][6] or a [Poka-Yoke][7].  


# Pull Systems

How to change from push to pull.
Pull is a system to manage inventory for made to stock or manage workload if it's made to order.
Inventory is a necessary evil used for short term decoupling of fluctuations. 
You need at least one part to produce and more than one to buffer.

Kanban is a inventory management system.
You set your kanban system to represent your target inventory.
Let's say you want to have 500 hinges, it should cover the time to replenish the inventory and reduce the fluctuations.

Kanban is typically understood as a two bin system which is a system with two Kanbans (information) but can be more than 2.
1. If you get an empty bin, use the information to fill the bin.
2. If you get a card, make what's on the card.

How many bins you need depends on the replenishment time, how long to get the bin back.
You need 1 bin per day, if you can fill a bin in half a day, two bins are enough.
If it takes 2 days to fill the bin, then after two days, you have a day without parts so you need 3 and for safety maybe a 4th bin.
The equation is replenishment time divided by takt time but don't take the average, take the extreme to be safe.
Ideally you want to have a long replenishment time divided by short takt time but you don't want to have millions of hinges. 
At some point you will run out and then it's OK to start fire-fighting with rush orders etc.

> **Note:**  
> This is about using [kanban bins (git commits)][9] to manage made to stock.  
> What's the stock here? Instead of orders or hinges, it was unexecuted test cases/stories/scenarios.  
> The goal is to keep the number commits on branches in git close to 1.
> As explained in the [just in time][8] section, the testers aimed to produce enough test cases for a developer so they could code for at least a day.  
> They had to make enough test cases for the day and even the next day in case something came up and they couldn't work that day etc.
> No inventory is the goal but with the dev managers and I having different priorities, we needed this buffer as a mitigation.
> If the developer was moving fast, the testers would do overtime and relax the next day. 

# CONWIP

IKEA is an exception by making to stock and then you mix and match but kitchens are usually made to order.
For made to stock, you want high stock availability with least material to produce it.
For made to order, you don't have the parts and the customer always has to wait.
How fast to make it aka lead time is influenced by utilization.
If you want a shorter lead time, you need higher utilization, but then parts must always be available.

For a made to order system, you use CONWIP; Constant Work in Progress.
It's like a Kanban card but you attach a paper to it with the kitchen spec (I'd say it's like an envelope).
When the kitchen is made, the paper (letter) is archived and the card (envelope) goes back to the start.
You limit the number of kitchens being worked on by cards where a card represents a bay to make a kitchen.

Assume you have limited capacity such as a person who is needed for 10 kitchen projects.
They need time to understand what's going on so all the time spent on the project is just catching up.
Perhaps they'll do bare minimum for 8 projects and only work on 2.
Statistically 3 is a good number per person to balance the work load.

If people are spread too thin, efficiency goes down.
Too many projects creates overburden, then you have fluctuations (unevenness) and lead times increase.
Pull systems for made to order limits the number of kitchen projects worked on at any time.
For that system to work, we need a pool, a funnel of work waiting so when the card comes back, you can start the next project.
If there's no orders, you have the problem anyways of people idling, pull system or not.

> **Note:**  
> What he describes here to me is the [Kanban board][9] that everyone uses where CONWIP is a WIP limit.  
> I see my QA team working on features as a made to order process because like a custom kitchen, no two were the same.
> That said, some of the internal processes were treated as made to stock with git as the inventory management system.
>
> I tried to set strict WIP limits, basically one feature per person and at most 1 production issue at any time.  
> However we spent quite a bit of time waiting for information on the prod issues so then we had to increase those WIP limits.   

# Levelling systems

You have small and big kitchen orders for eg and you order parts, sometimes too many at once.
This was seen with cars during COVID; there were no orders and then there was an avalanche.
The suppliers weren't happy because they had all the parts but no orders and then they had orders but no parts and had the costs of expediting the ramp up.

A pull system doesn't improve or prevent fluctuation, but prevents it from becoming worse because the CONWIP acting as a limiter reduces the effect.
By limiting the number of projects in progress, you make it more predictable to see how long it takes to do the project.
If the project quantity fluctuates from 5 to 50, your lead time also fluctuates and that makes it harder to predict.

The pull system is a good platform to make systems on top of them like [leveling systems][10].
Let's say you're making 2 door and 4 door cars.
If you do all 2 doors and then all 4 doors, you'll have bored folks and then overworked folks.
Instead alternate 2 door and 4 doors, this is levelling.

Levelling is tricky, first stabilise system (standards, good maintenance), then have a pull system to reduce fluctuations and then think about levelling.
You want to first get your car running reliably before tweaking the performance or fuel-efficiency.
Different ways to do levelling.

1. Make the same number everyday. 
275 crankshafts every day, more than 10% change from month to month, this is a daily production plan and it's difficult.
The Germans have a monthly pattern rather than alternating.
The problem is you stick to a plan for the whole month which is hard since most companies can't do today what they planned yesterday.

2. Easier is to mix them to the smallest possible lot size, ideally 1 which isn't always possible. 
Don't do all 2 doors this week and all 4 door next week, you keep both sub-assemblies equally busy by intermingling them.
This is constrained by the time it takes to switch over from one way to make them to another.
The more often you switch tool, the lower the inventory, the lower the work for all systems around it.

Levelling needs high reliability and stability aka low fluctuation of your system.
Capacity, inventory and time are the ways to decouple fluctuation.
Toyota can do it because they control the time when you're getting your car.
The dirty secret is that that you would increase your lead-time just to do more levelling.
It's like intentionally slowing down the flow rate by buffering for a smoother experience.
This only works if you have a pattern you can stick with.

> **Note:**  
> When I think of [levelling][10], there's two types, levelling with new features and production bugs.  
> The goal is to not have accumulation of untested code commits in git.
> Put another way, for two features of the same size, you don't want to have two vastly different lead times as a result of working on them in sequence.


[1]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Muda
[2]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Mura
[3]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Standardized%20Work
[4]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Gemba
[5]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Kaizen
[6]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Jidoka
[7]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Poka%20Yoke
[8]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Just%20In%20Time
[9]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Kanban
[10]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Heijunka
[11]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Muri

