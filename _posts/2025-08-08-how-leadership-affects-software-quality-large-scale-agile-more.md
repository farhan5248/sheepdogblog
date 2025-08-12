---
layout: post
title:  "How Leadership Affects Software Quality, Large-Scale Agile & MORE"
date:   2025-08-08
categories: engineering-room
---

<iframe data-testid="embed-iframe" style="border-radius:12px" src="https://open.spotify.com/embed/episode/6I5ctJ8fawwV7ncN71N4vh?utm_source=generator" width="100%" height="352" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

# Summary

I liked this episode for the same reason I liked the one with Henry Golding.
Gary's experiences and avoidance of buzzwords to transform an organisation more closely resembles the approach I took.

# 2:28 Leading a complex adaptive system

I [trained my team myself][5], had weekly one on ones and there were no consultants. 
Each week I reviewed what I learnt with my leads and we kept trying new experiments.

I can't say there was a vision or strategy handed to me by the execs.
At most the director who put me in that position was very supportive.
When he was let go by the new VP, the new director (my boss's boss) provided no direction, just the usual exhortation to do better.
I was asked by the new directors what the plan was because they were looking for an improvement programme.
I said there wasn't one, that'd we'd just continually improve opportunistically.
I'm going to assume they left me alone to do so initially because they must have thought I'd be sure to fail with no budget.

During my time on the QA team, Thoughtworks consultants were also brought in but they were basically given the run around.
After that VP left and then the 3rd VP took over, she had an internal DevOps consultant who wasn't technical and that went nowhere.

I too avoid the terms Agile or DevOps because of the pre-conceived notions people have of what those words mean and prepared arguments for why that won't work here.
[My approach][6] was to address common cause variation around time to fix a failing test through PDSA cycles.

# 10:39 Design vs production engineering

I think when we start, software development looks more like a manufacturing engineering problem.
I think companies just set it up this way because they think it's a manufacturing problem.
However by the end of a transformation, we should have something that looks like a design engineering problem.
If everything done by someone manually could be converted into a self-serve platform, then you don't have all the hand-offs that make it look like manufacturing.
For example, instead of handing off the code to operations, we have services that allow developers to do so themselves.
I wanted the same thing but for QA tests; I described my approach to doing so by [developing a platform here][1].

# 17:47 The role of effective leadership

I tried to implement [Dr Deming's 14 points][10] for management.
The system was a legacy tightly coupled system where you have to release the software together. 
The single sign-off required the work of almost 60 QA team members.
The biggest sources of inefficiency were across the team because of the waterfall process and big batches of work.
I could influence people within my team and the COBOL dev team but it was hard to do across the other teams.

I communicated to my team what [my vision was for the team and how we were going to get there][2]. 
Given the size of the QA team and the task of reducing the cost, my salary was pretty much the budget for improvement.
Any talk of consultants/contractors meant that people's jobs would go to India so that wasn't an option for my team in Canada.
Also if I told people what I had in mind, I'm pretty sure I'd have been told no which is why I adopted the [gravity slingshot strategy][3].
If you're familiar with manufacturing and Goldratt then [my post about creating pull][4] explains what metrics I used to measure our progress.

# 28:21 The industrialization of agile

Because of the industrialization of agile, I took a buzzword free approach.
As explained in [Start With Why][7] I only explained what TDD/BDD was to motivate my team.
I showed my team the manifesto for agile software development and explained the Poppendiecks work on lean software development.

In my mind I tried to apply my very limited understanding of Dr Deming's work to the process of inspection; basically to do point 3 and cease dependence.
It's why I adopted the term [Deming Driven Testing][8] to describe that approach

# 34:39 Outcome focused vs process focused

In my case, my QA team was basically 4 QA teams of no more than 15 people each.
The main areas of friction in the span of my control were between those 4 teams when they had to co-ordinate to do system testing
The other areas of friction were the development and BSA teams.
Given I had read everything the Poppendiecks had put out, I leaned heavily on [manufacturing process improvement][4].

I had previously worked with the COBOL developers as a developer on the Java/PLSQL parts of the system.
That and the relationship my COBOL testers had with them gave us some influence in the way they work.
To make it easier for developers to invest their time I fostered a [culture of easy ownership][2].

# 44:31 The challenges of adoption

I agree that most people I've worked with have never seen what good software development looks like.
Even folks who think SCRUM works without TDD do so because they work on such small projects that even waterfall would be fine.
The director who officially took over from the one who moved me to the QA team thought he was doing just fine.
He could find nothing wrong with how he did his job.
At most he thought QA needed to do better because you know, quality is always inspected in.
Him having a PMO agressively defend waterfall and working with big batches wasn't the problem ;)

Just as people would argue with him till the cows came home about TBD, I avoided buzzwords.
My recommended approach is simple, use a process control chart to study the time it takes to resolve a test failure, keep looking for common cause variation and remove it through PDSA.
The reason for developing the testing platform was so that developers could organically opt into new ways of working that progressively gave them more feedback earlier.
Before that though, my testers had to change as well, which is why we had our internal enabling team.

I also agree with not going someplace and just re-organizing everything into small teams or re-architecting into a loosely couple architecture.
Compared to what was in the DevOps handbook, in that org, it's so far from how they're doing things, they could easily find ways to push-back.
In the end my large QA team worked with COBOL developers from another manager's team; they didn't have to be combined into one.

# 1:00:23 The two strategies for scaling software

This system didn't need to become a collection of micro-services.
I think in more cases than people think, you can do with a modular monolith or even a monolith if you have earlier feedback.
You make sure you have feedback to make changes in small steps whatever the size of the system.
You need to work in a way to make sure your system is in a releasable state at all times.
Had the momentum continued, we would have been able to do Continuous Delivery with COBOL.
This was possible with this particular system because almost all functionality was controlled by feature flags.

Because the architecture was outside of my scope of control and the architecture team was the ivory tower type, waiting for micro-services to help solve testing challenges wasn't an option.
There was lots of low hanging fruit that I could go after first simply by identifying and removing waste.
In fact my whole strategy didn't need any team outside my own to change.
Let's say the COBOL developers didn't change.
Then to reduce the waste of incorrect test cases, I'd have invested in model based testing which lets you generate thousands of test cases in a few minutes.

# 1:06:30 AI

When I joined the QA team, I too was trying to answer how to move forward in an org that has lots of manual testing.
Fully automating the system tests wasn't done and instead we focused on unit tests for the most complex component.
We got there by working in small batches and working with developers to prevent defects rather than automate inspection for them.
Eventually we'd be able to remove manual testing as a quality gate.

I think AI can help accelerate that process.
1. My testers were eventually using a [custom DSL in an IDE][9].
Just as developers use AI tools to increase their productivity, so can the testers.
To be clear, I wouldn't use AI to generate the automation, since I want determinism.
Instead I'd use AI to help develop the regular expression for the DSL grammar or to help quickly create a test by querying a graph DB.
Both of these are what I'm currently working on.
2. As a leader, I had also used an AI Slack integration to help answer questions.
Because I wanted an organic adoption of our new ways of working, I wanted the team to ask questions in a safe space.
For example I thought they might be embarrased to ask a question thinking it was dumb or thinking they'd be added to a list of head-count saving opportunities if they did so openly.

[1]: /demingdriventesting/Communicating%20the%20strategy%20to%20QA/ShuHaRi
[2]: /demingdriventesting/Communicating%20the%20strategy%20to%20QA/Culture%20of%20Easy%20Ownership
[3]: /demingdriventesting/Communicating%20the%20strategy%20to%20QA/Gravity%20Slingshot
[4]: /sheepdogblog/shop-floor/2025/07/24/creating-pull-in-your-factory
[5]: /demingdriventesting/Communicating%20the%20strategy%20to%20QA/Coach%20Teams%20Not%20Individuals
[6]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/index
[7]: /demingdriventesting/Communicating%20the%20strategy%20to%20QA/Start%20With%20Why
[8]: /demingdriventesting/about
[9]: /demingdriventesting/about#the-ubiquitous-language
[10]: /demingdriventesting/Deming/points
