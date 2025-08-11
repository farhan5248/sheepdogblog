---
layout: post
title:  "How Leadership Affects Software Quality, Large-Scale Agile & MORE"
date:   2025-08-08
categories: engineering-room
---

<iframe data-testid="embed-iframe" style="border-radius:12px" src="https://open.spotify.com/embed/episode/6I5ctJ8fawwV7ncN71N4vh?utm_source=generator" width="100%" height="352" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

# Summary

I think this is the episode where Dave talks about software engineering being similar to design engineering vs manufacturing engineering.
I'll come back and update this page after re-listening to the episode but I'll put my notes here for now.

I think when we start, the process looks more like an manufacturing engineering problem.
However by the end, we should have something that looks like a design engineering problem.
To me, it looks like an manufacturing engineering problem because you have hand-offs; the code goes to QA and then to operations.
If you convert every hand-off point to a self-service platform, it'll get closer to design engineering.
My goal then was to eliminate the hand-off to QA so that developers could run the tests themselves by creating a platform.

I took inspiration from two practices:
1. When I joined the QA team, I asked a friend's brother who is a professional civil engineer to show me how he worked.
He demonstrated the use of [STAAD](https://www.bentley.com/software/staad/).
Their website claims that STAAD is not a CAD software. STAAD is specifically designed for structural analysis and design.
What I saw was basically him creating/designing and running a simulation (testing) every few minutes.
What he didn't do is design only and then hand the design to another team to press the simulate button.
The simulation was based on data and mathematical models which to me is just test data and model based testing models.
2. Docker deploys don't care about what's inside them.
You can code in Python, Java, JavaScript etc and the deployment process stays the same.
I wanted the QA team de-coupled in the same way, ideally using a REST API but we used a Java library as the API client.
An API gives them access to the data and they could use that in whatever framework they wanted.
It de-couples the QA team from every development team and they can all preserve their own frameworks and practices.
This is why I agree with [Dave when he spoke to Henry Golding about](/sheepdogblog/engineering-room/2025/08/04/how-we-made-minecraft-using-continuous-delivery#3513-test-framework-constraints) frameworks being intrusive.

In the lean world, I like that we prefer pull and not push; I wanted people to opt in.
Therefore the platform had to make adoption easier and so I applied Shu-Ha-Ri to its design.
1. Shu: Follow the rules
2. Ha: Understand the rules and then bend them
3. Ri: Break the rules and remake them

Shu was basically making it easy for developers to run QA's tests in QA's environment using QA's frameworks by providing a service.
The idea was that after doing a bug-fix deploy, they could just run the failing test and see if they fixed it.
Only if it was fixed would my tester need to switch context and update the defect etc.
The alternative was waiting for QA to test it and then the developer would have to switch context later.
It was implemented as a collection of Jenkins jobs that they could schedule and run for a specific Cucumber tag.

Ha was making it easier for developers to run QA's tests in their environment using QA's frameworks which their code had to work with.
The goal was to show them how the API could be used to create data that could be inserted into their databases or test automation like SoapUI (a tool they were familiar with)
This way they prevent bugs because they'd run the tests earlier.
Ambassador Spock said, [the adoption needs of the many outweighs the adoption needs of the few](https://www.youtube.com/watch?v=Xa6c3OTr6yA).
Eventually the COBOL developers had to learn to use Eclipse, Java etc because my team wanted to use Cucumber.
This didn't feel good to me, to impose a new language and framework on developers just to run a test.

Ri was about making it easier for developers to run QA's tests in their environment using their frameworks.
Unfortunately, we never got that far; I left my job and the new manager of my developers didn't do so.
Ideally if the Java library was converted to a REST API, then you could run COBOL code that did REST querries.
The REST API would let anyone retrieve test steps and their data or just the setup data as insert statements per DB table.
We only used the API this way in our own test automation, that is, even the QA automation itself was auto-generated from the Xtext DSL files.
A partial example is [here](https://github.com/farhan5248/sheep-dog-cloud/blob/main/sheep-dog-dev-svc/src/main/java/org/farhan/mbt/controller/UMLController.java); I'll complete it in September.

The last thing to remember is that the API providing access to the data was only possible because of Xtext.
It gave us a way to have parseable tests by enforcing a grammar.
Without it, we couldn't extract information from what would basically be free-text.
If garbage went in, what came out wouldn't be useful to developers.


# 2:28 The moment Gary realised he was onto something

Towards the end of my time on the QA team, I once again went looking for information on how to transform a QA team the way I did.
That is using Deming, TPS and DSLs etc, upskill non-programmer testers so that developers can get feedback earlier.
When I still couldn't find any examples, I decided I had to slowly start making notes so that I could make this site for the possible benefit of others.

# 3:46 Leading a complex adaptive system

-> Software is a complex adaptive system, people had to learn and adjust.
-> He did agile upside down, the scrum team was him and his staff.
They were learning and adjusting the whole way.
They were constantly learning and adapting.
-> One of the worst thing is tell managers that they had to support the teams and get out of the way.

-> We don't need evidence that this agile thing works, the main barrier is the behavior of executives.
-> It's a behaviour and cultural change.
When managers did that, the teams became adaptive.
The executives still wanted a prescriptive approach and a deterministic system.
When you're leading a complex adaptive system, you need a different approach.
You need to be move involved.
-> They higher consultants to come in and train people on Agile and DevOps 

-> Gary tries to avoid the terms Agile or DevOps.
-> People have pre-conceived notions of what those words mean and prepared arguments for why that won't work here

# 10:39 Design vs production engineering

# 17:47 The role of effective leadership

Need vision and objectives.
Struggling to get new system up and going.
There were lots of branches. 
If they don't have software to deal with the product layers, they make a lot of branches, that had to change

-> if you have a tightly coupled system where you have to release the software together.
-> They biggest sources of inefficiency are not on the team, but across the team.

-> when driving a change like this, you need people to embrace new ways of working
-> you can maybe influence within your team and it's hard to do across teams
-> they didn't go to consultants, they learnt themselves how to learn and adapt 

-> they couldn't make a plan to come up with more resources because they won't get anymore
-> if you would have told them that was possible, running so many tests per day, they'd have told you that is crazy.

-> if you were to make a prescriptive plan to do this, how do you plan for something you don't think is possible
-> what can we do now that's going to have an impact within a few days or next week or next month.
-> we don't know what all the steps are and we're going to define the route as we learn more.

-> what are we going to monitor
-> it should metrics to measure how the system is evolving, not how far are we from the deadline.
-> Deming says leaders job is to create systems that enable employees to be successful
-> I see very few software leaders playing that role. 
-> they need to find the friction in the system and remove it.

-> What's the point of trying to hit the deadline if you're doing the wrong thing. 
-> Release dates matter but everything didn't need to go into production on that date.
-> Agile projects fail more than other kinds of projects based on whether they hit deadlines or not.

# 28:21 The industrialization of agile

Which agile are you doing, the manifesto one or the ritual one with consultants?
The leaders micro-manage so lets get a scrum-master to micro-manage and call it agile.
He came up with very basic common sense principles that are harder to argue with.

Continuous Delivery is a holistic approach based on inspect and adapt.
-> You need the freedom to make mistakes, to try stuff out.
-> Which direction are you going, prototype and thin slice of code.

-> The goal is agility, to try things out and see what works.
-> It's waterfall in disguise because of how it's interpreted.

# 34:39 Outcome focused vs process focused

what's the role of leaders to help achieve those goals?
if you've got a larger complex tightly coupled systems a lot of the friction comes from across teams. mb/drug qa + dev/qa drug
teams focus on what's in the span of their control and not take on bigger challenges.
manufacturing had create a system of continuous improvement and software hadn't.
When you walk into a plant floor, you can see the process but not in software, it's harder to see/feel.
How to think of it as a process and make it visible.
The ways to improve stuff is well known, the hard part is getting people to invest.
If the leadership team is taking an adaptive approach and trying to learn what the system is capable of, then the org has the wind at its back.
He used the metrics to tell him how the system was evolving and to learn where to go have conversations to learn.
His job is to learn how it's evolving and influence priorities.

# 44:31 The challenges of adoption

People have never seen what good software development looks like.
If you don't recognise it's a problem, how do you get people to get started.

We don't know how to do TBD but we're going to do it.
People would argue with him till the cows came home.

Don't use buzzwords, instead use simple terms to explain it.

If we want to help devs, we need a system that provides them with earlier feedback.
How slow is the feedback now? Focus on getting people to take small steps.
Make it try-able, make it easy

Mistake of devops community, this is how you do it, need pizza sized team, need pager, need to know everything.
If Gene or jez came in with that, they'll be told to go away.
nicoles book, accelerate, how to deal with large complex systems, loosely coupled systems.
if you now say you need to re-architect just to have small teams, they'll also say no.

when you say devops, in these orgs, it's so far from how they're doing things, they can say it doesn't work.
we just need a system that provides better feedback as quickly as possible.
smaller batch sizes gives feedback better -> qa testing in dev instead of after integration.

in software product and process is same team, but in manufacturing, it's two different teams.
the production process of all the steps he describes can be automated by platforms.

# 1:00:23 The two strategies for scaling software

Not every system needs to become a collection of micro-services.
I think in most cases you can do with a modular monolith or even a monolith if you have earlier feedback.
You make sure you have feedback to make changes in small steps and whatever the scale of the system.
You need to work in a way to make sure your system is in a releasable state at all times.
if you're starting with a large tightly couple system, there's lots of low hanging fruit that you can go after first.
take an evolutionary approach instead of big bang.
There aren't many people out there trying to help organisations trying to help themselves.
It's ok to make mistakes, just make new ones, not the same ones again and again.

# 1:06:30 AI

how to apply AI as a leader -> doc my features
vs AI as a developer.
Lots of stuff about AI for developer, not leader.
How to move forward in an org that has lots of manual testing?
worst tests are system tests because they're difficult to write, unit tests are better.
how long to put unit tests in place to remove manual testing.
First learn to work in small batch sizes to avoid debug and triage.
Ideally remove manual testing as a quality gate.
When using AI, start with stepwise approach and ask it how it would solve the problem.
given all the manual tests, how would approach writing the gherkin type code for this. -> I'm making an AI that reads the tests and makes a regex for a DSL.

