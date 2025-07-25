---
layout: post
title:  "Creating pull in your factory"
date:   2025-07-24 21:00:00 -0500
categories: shop-floor
---

<iframe data-testid="embed-iframe" style="border-radius:12px" src="https://open.spotify.com/embed/episode/14Nbr9nPnIhBYsYlXJY3xI/video?utm_source=generator" width="624" height="351" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

# 8 Wastes, Unevenness and Overburden

## Summary
To Toyota overburden (asking too much of people) is most important.
Then comes unevenness (fluctuations in people and processes) and finally the wastes.
The way it's seen is overburden causes fluctuations which in turn causes waste.
Eliminating waste needs fluctuations addressed which needs overburden addressed.

Waste is easy to see, you only need to observe a process once.
Fluctuations are harder, you need to observe the process at least once.
The people who know the fluctuations best are the ones on the shop-floor or in my case, the testers.

## Notes
I mapped the 8 wastes as so. More details on [the wastes are here][1]
1. transport, manual tester to automation guy.
2. inventory, too many unexecuted tests or unvalidated automation tests.
3. waiting, waiting for test automation to be created or run, waiting for devs to fix bugs.
4. motion, unnecessary clicking like with doc to dnp which I wrapped with maven.
5. overproduction, unnecessary test cases to meet a metric of x test cases for y days of coding.
6. overprocessing, unnecessary steps in the test case or over complicated test setups or doing e2e testing when a unit test is good enough.
7. defects, test case writing defects.
8. skills, testers who were able to learn to code like Pratik but whose time was wasted doing manual testing.

To me, studying the fluctuations was where [SPC][2] came in. I wanted stuff under statistical control.
I wanted to reduce the occurence of last minute high priority defects which have very little time to be fixed by devs and re-tested by my team.
Another fluctuation was people's utilization. I didn't want to have 100% but I did want to avoid the famine/feast cycles that sometimes appeared. 
Overburden on folks with too much work was reduced with standards so we could swarm to solve problems, having full-stack testers or generalists instead of everyone being a specialist only and automation of test execution.
For example non-SME would use Robot-Framework to automate the tasks for a SME if the non-SME was in a famine of work.

# Stabilizing Fluctuations

## Summary
First goal is to stabilize production.
Are machines stable?
Are work-standards good? Do they exist? Do people know to use them? 
There's always going to be fluctuations, but we want to have less.
There's so much fire-fighting, you can't stop to sharpen the axe because you have so many trees to fell. (Put picture of square wheel here)
If you're in a burning house, a fire-fighter is nice. 
Even better is to not have a burning house.
Just rewarding the fire-fighters creates career arsonists.
Overburden is a lack of safety.
First identify where are things going wrong, you'll need some sort of data.
Then prioritize where should you start.
Estimate the effort and impact (I guess ROI).
Pick a low impact problem.
Work on ones that give you success stories.

The shop-floor knows it already knows the cause.
Team-leads can see it.
Sometimes it's hard to watch and do at the same time so you can't tell.
You can actually notice but it doesn't mean you can make the connection about what's causing it.
Management needs to get rid of the cause.

## Notes
How to free-up the time of an overburdened tester who's super busy. One way is by having standards.
All the testers didn't write test cases in a way that another tester could understand and execute their tests.
If I wanted them to be able to swarm to reduce the load on one tester, I needed those who were free to be able to read the tests.
This is where the ubiquitous language came in; it was to [standardize work][3].
One challenge in getting folks to adopt a standard that requires so much details is fear.
I think folks kept the test cases light on details to protect their job-security.
That is, if nobody can read their work, then nobody can replace them.
By showing the team that the test cases written in the DSL can be automatically converted into automation, I feel it helped reduce the resistance.
Even if they would lose their job as a result of sharing knowledge, at least they would learn Robot Framework with Python.

The overburden caused by lack of safety to me was psychological safety.
Some testers increased the scope of their testing if they didn't find enough bugs.
There was this culture that the good testers find bugs.
So if someone didn't find any bugs, they felt they need to fill their bugs found quota.
This was easy for me, I just told them I didn't care about finding bugs because quality can't be inspected in.
I wonder how many QA directors/managers/leaders actually realise that?
After I left, I'm told, they were told to record how many tests they ran everyday and what percentage they automated.
I'm told this instruction from the top, like the C-suite but without any explanation why.

# Reducing Fluctuations

## Summary
Can you make the work not fluctuate?
You can't get rid of fluctuation, just reduce it with PDCA. 
In Western companies, it's little plan, lots of doing, then even less check and act.
At Toyota, there's huge emphasis on plan, way more than half. 
They try to understand what's happening, with who, when. 
You need to stratify the problem, make a prioritised problem.
Don't improve all quality, narrow it down.
20-30 factors might contribute to quality problems but pick the one that has the biggest impact.
Now that you know the problem, what's the root cause like process, worn out tool, a setting?
Sometimes you use the fishbone diagram or a mind-map.
Develop multiple root-causes.
In the Western world, the minute you find one, just solve that.
In Japan, for each root cause you ask: are they effective, safe, cost effective, how fast can you do it, how much effort to do that.
Then finally you get to the D in PDCA.
Then check if it's gone or only gone when no manager is looking. 
If yes, then share the fix with others, that's the act part.
Toyota uploads their A3 to a common database so that their employees can Google that.
If not, restart the PDSA.
Peter Drucker's SMART target, not always possible, but if so, it would be perfect.

## Notes
So the goal was to reduce common cause variation.
At the company I worked, they had a 6 step version of the PDCA so I used that.
If I remember correctly, the first step would be go to the [Gemba][4].
Another one of the steps was Plan split into two or something like that.

Each week I met with everyone on my team for 1:1 to ask what's bugging them so we can fix it. 
Together we'd come up with an [Kaizen][5] which was either a [Jidoka][6] or a [Poka-Yoke][7].
Rarely did anyone come up with an improvement that didn't need my support as the manager.
I'd then prioritise which improvements would have the biggest impact for the team and work on those.
Though step 1 was initiatied during the 1:1, the remaining 4 happenned throughout the week through Slack conversations.
Step 6 was a weekly/monthly/quarterly review of all changes to the process depending on the impact of the change.
The company also recommend the use of SMART goals for the quarterly goals so we used that for each improvement.

# Pull Systems

## Summary
How to change from push to pull.
Pull is a system to manage inventory for made to stock or manage workload if it's made to order.
Inventory is bad but necessary. 
You need at least one part to produce and more than one to buffer fluctuations.
Inventory is for short term decoupling of fluctuations
It's hard to manage and might have too much or too little of stuff.

Pull is a way to manage your inventory for make to stock.
You set your kanban to represent your target inventory.
Let's saw you want to have 500 hinges.
The 500 should cover the time to replenish the inventory and reduce the fluctuations.
Kanban are inventory management system.
Since inventory is bad, an inventory management system is good to manage a pull system.

Kanban is typically understood as a two bin system.
Two bin system is a system with two Kanbans.
Kanban is just information, it could be the box, if you get an empty box, fill it.
It could be a card, if you get a card, make what's on the card.
It depends on the replenishment time, how long to get the box back.
You need 1 box per day, if you can fill a box in half a day, two boxes are enough.
If it takes 2 days to fill the box, then after two days, you have a day without parts.
Now you need 3 and for safety 4 boxes.
The equation is replenishment time divided by takt time but don't take the average, take the extreme for safety.
You should have a pretty long replenishment time divided by pretty short takt time.
You don't want to have millions of hinges, you accept that you ran out and then start fire-fighting with rush orders etc.

## Notes
Instead of orders or hinges, I was working with test cases/stories/scenarios.
Since the tests were driving the development, imagine each batch of scenarios as requisitions for code to be created.
As explained in the [just in time][8] section, the testers aimed to produce enough test cases for a developer so they could code for at least a day.
They had to make enough test cases for the day and even the next day in case something came up and they couldn't work that day etc.
We didn't make [Kanban cards][9] for each daily chunk of test cases.
Instead the bucket/bin was the git commit. 
I taught the testers to amend their git commits and only when they had the next batch of tests, they would push it.
I was aiming for Continuous Delivery and Trunk Based development

This is why my testers had to get a head start.
The developers would do their initial analysis while my testers created some key test cases as they'd call it.
Then with this lead of a few days of tests for developers to run, they'd replenish one per day.
Developers then could keep doing a fetch and only merge with the next git commit and work on those tests.
I think some developers just did a pull but that was ok since there would only be 1 git commit added each day.
Why did I care about this? Well, what I didn't want to have is failing tests all the time.
Let's say the tester is a little ahead, then you'd never see all the test suites pass.
This isn't great for TBD, your pipeline would never complete successfully.
I wanted the developer and tester to learn to synchronise (reduce variation/fluctuation)

# WIP Limits

## Summary
IKEA is an exception by making to stock and you mix and match.
In many cases, you produce only when customer orders which is made to order.
For made to stock, you always want to have material and the least material to do so.
You want high stock availability with least material to produce it.
Made to order, you don't have the parts.
Customer always has to wait
How fast to make it aka lead time is influenced by utilization.
If you want 100% util, then parts must always available.
High utilization leads to shorter lead time.

For a made to order system, a pull system helps, not just Kanban.
You use CONWIP Constant Work in Progress.
It's like a Kanban card but you attach a paper to it with the kitchen spec. (I'd say it's like an envelope)
When the kitchen is made, the paper (letter) is archived and the card (envelope) goes back to the start.
You limit no of kitchens by cards or if you have 5 bays to make kitchens, then each card represents a bay.
You have limited space and capacity.
If people are spread too thin, efficiency goes down.
Assuming you have a project to develop a product. If you have 2 projects, a person has to handle both and if you have 10, they're part of all of them.
They need time to understand what's going on and if you have a person but all the time spent on the project is just catching up.
So the person does bare minimum for 8 projects and only works on 2.
Statistically 3 is a good number per person to balance the work load.
Too many projects creates overburden, then you have fluctuations and lead times increase.
Pull system for made to order limits the number of kitchen you're making at any time.
For that system to work, we need a pool, a funnel of work (backlog) waiting so when the card comes back, you can start next project.
If there's no orders, you have the problem anyways, pull system or not.

## Notes
I see my QA team working on features as a made to order process.
That is, each feature they worked on is new.
While each feature worked on some re-usable business rule, that combination of business rules and modifications to it were new like introducing new soft-close slides to a cabinet's drawers.

What he describes here to me is the [Kanban board][9] that everyone uses where CONWIP is a WIP limit.
I tried to set WIP limits, basically one feature per person and at most 1 production issue at any time.
This helped by reducing the time context switching from one feature to another every day or multiple times in a day.
The challenge was that we had a system where half the time is spent fixing production issues.
That means that we needed to get information from the business users and so we spent quite a bit of time waiting so then we had to increase those WIP limits. 
The scope of my system was the QA inspection process and things like code coming in or information from business users about production issues were just seeing as orders from customers with a high degree of fluctuation.

# Levelling systems

## Summary
A pull system doesn't improve fluctuation, but prevents it from becoming worse.
Customers order irregularly and bare bones pull system doesn't prevent it but the CONWIP is a limiter and reduces the effect.
You have small and big kitchen orders for eg and you order parts, sometimes too many at once.
This was seen with cars during COVID. There were no orders and then there was an avalance.
The suppliers weren't happy because they had all the parts but no orders and then they had orders but no parts and had the costs of expediting the ramp up.
Sooner or later, the customer pays for the expedited costs.
By limiting the number of projects in progress, you make it more predictable to see how long it takes to do the project.
If the project quantity fluctuates from 5 to 50 you lead time also fluctuates and that makes it harder to plan.

Pull systems are good to make systems on top of them like [leveling systems][10].
The pull system is a good platform to manage fluctuations and get it more level.
Let's say you're making 2 door and 4 door cars.
If you do all 2 doors and then all 4 doors, you'll have bored folks and then overworked folks.
Instead alternate 2 door and 4 doors.
Levelling is tricky, first stabilise system (standards, good maintenance), then have a pull system to reduce fluctuations and then think about levelling.
First get your card running reliably before tweaking the performance, fuel-efficiency.

Different ways to do levelling.
Make the same number everyday.
275 crankshafts every day, more than 10% change from month to month, this is a daily production plan and it's difficult.
Easier is to mix them to the smallest possible lot size, ideally 1 which isn't always possible. 
Back to the doors, you keep both sub-assemblies equally busy.
Don't do all 2 doors this week and all 4 door next week, intermingle them.
This is constrained by the time it takes to switch over from one way to make them to another.
The more often you switch tool, the lower the inventory, the lower the work for all systems around it.
The Germans try to do it a sucky way, they have a monthly pattern rather than alternating.
The problem is you stick to a plan for the whole month which is hard since most companies can't do today what they planned yesterday.

Levelling needs high reliability and stability aka low fluctuation of your system.
Toyota can do it because they tell you when you're getting your car.
capacity, inventory and time are the ways to decouple fluctuation.
The dirty secret is that that you would increase your lead-time just to do more levelling.
It's like intentionally slowing down the flow rate by buffering for a smoother experience.
This only works if you have a pattern you can stick with.

## Notes
When I think of levelling, the production issues come to mind.
The usual feature work in the release was stable enough.
As we removed sources of defects we had a pretty stable system of how we worked.
However there'd still be times when the developers weren't ready or the BSA didn't finish writing the requirements documents.
So we filled in these gaps in work with the production issues of which there were countless.
Like he stated, we'd also increase our lead time. So even if we could typically write and execute tests for an issue in a week, we'd typically tell folks it'll be ready in a month. 
That way, if there was a slow day we could just work on a prod bug.
Eventually it kind of worked out that 4 days were spent on a feature and 1 day on a prod bug each week.

[1]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Muda
[2]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/SPC
[3]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Standardized%20Work
[4]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Gemba
[5]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Kaizen
[6]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Jidoka
[7]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Poka%20Yoke
[8]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Just%20In%20Time
[9]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Kanban
[10]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Heijunka

