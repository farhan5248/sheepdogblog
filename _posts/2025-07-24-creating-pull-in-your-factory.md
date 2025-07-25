---
layout: post
title:  "Creating pull in your factory"
date:   2025-07-24 21:00:00 -0500
categories: shop-floor
---

# The 8 Deadly Wastes 

To Toyota overburden (asking too much of people) is most important.
Then comes unevenness (fluctuations in people and processes) and finally the wastes.
The way it's seen is overburden causes fluctuations which in turn causes waste.
Eliminating waste needs fluctuations addressed which needs overburden addressed.

I focused on:
1. transport, manual tester to automation guy.
2. inventory, too many unexecuted tests or unvalidated automation tests.
3. waiting, waiting for test automation to be created or run.
4. motion, unnecessary clicking like with doc to dnp which I wrapped with maven.
5. overproduction, unnecessary test cases to meet a metric of x test cases for y days of coding.
6. overprocessing, unnecessary steps in the test case or over complicated test setups or doing e2e testing when a unit test is good enough.
7. defects, test case writing defects.
8. skills, testers who were able to learn to code like Pratik but whose time was wasted doing manual testing.

To me, studying the fluctuations was where SPC came in. I wanted stuff under statistical control.
I wanted to reduce the occurence of last minute high priority defects which have very little time to be fixed by devs and re-tested by my team.
Another fluctuation was people's utilization. I didn't want to have 100% but I did want to avoid the famine/feast cycles that sometimes appeared. 
Overburden on folks with too much work was reduced with standards so we could swarm to solve problems, having full-stack testers or generalists instead of everyone being a specialist only and automation of test execution.
For example non-SME would use Robot-Framework to automate the tasks for a SME if the non-SME was in a famine of work.

# Advantage of wasters

Waste is easy to see, you only need to observe a process once.
Fluctuations are harder, you need to observe the process at least once.
The people who know the fluctuations best are the ones on the shop-floor or in my case, the testers.

# Stabilizing production

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

How to free-up the time of an overburdened tester who's super busy. One way is by having standards.
All the testers didn't write test cases in a way that another tester could understand and execute their tests.
If I wanted them to be able to swarm to reduce the load on one tester, I needed those who were free to be able to read the tests.
This is where the [ubiquitous language](/demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Standardized%20Work) came in.
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