---
layout: post
title:  "How We Made Minecraft Using Continuous Delivery"
date:   2025-08-04
categories: engineering-room
---

<iframe data-testid="embed-iframe" style="border-radius:12px" src="https://open.spotify.com/embed/episode/5u3vGwdZwlqzhSGDZrx85q?utm_source=generator" width="100%" height="352" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

# Summary

Instead of summarizing by topic, I've added the timestamps/questions that Dave asked. 
A lot of what Henry describes is similar to what I experienced working with my QA team and the corresponding development team.

# 3:07 What triggered your interest

I was a developer and also found myself in a QA team.
I joined with the intention of making the lives of developers easier by changing the QA team to focus on earlier, not faster feedback.
When I stared on the QA team, I knew nothing about QA processes, half of which appeared to be [testing theatre](https://dannorth.net/blog/we-need-to-talk-about-testing/).

# 4:56 It takes a long time to find and fix things

The benefit adjudication engine was fairly complex.
When a mistake was made a low level, it would take a long time for the QA team to identify where the issue was so that they could assign the bug to the right person.
Then the developer had to setup all the data to try and test it which would take them a while.
What my QA team did for them in the end was make it easier for them to recreate the setup data in their dev environment.
If a defect was found later on in the QA environment, it was more likely that the source was one of the less complex components.

# 5:41 What are some of the challenges of adoption

Even though we had enough requirements to fill a phone book, I'd say nobody really knew what we were making.
This is because the system was so complex that nobody could fully understand the downstream impacts of any change.
There were times where the requirements simply stated "preserve existing functionality" because the BSA just didn't know what that was.

# 10:09 Relationship between development and QA

There was a stigma of being in QA at the company I was at; being in QA was a thankless job.
I remember a concerned BSA had asked me if I was forced to join the QA team, as a sort of demotion.
When I replied that it was what I wanted, she looked like she was thinking "you poor thing, you actually believe that".

What was interesting is that my testers had a lot of knowledge about the system and some of them were very highly respected.
What worked really well was where my QA and the COBOL dev silos were bridged and they worked well together.
The other 3 QA teams I had had no such luck and so even with the same tools, we couldn't improve as much.

# 11:04  Having professional test people

In an ideal world, my testers wouldn't be running most of the tests.
They'd write the tests and manage the test data or even do exploratory testing to develop a better understanding of the system.
I found that most developers just aren't interested in doing that work but it needs to be done.
The best person to run the test is the developer who's going to fix the code.
The more other people get involved, the longer the feedback loop and the more expensive it becomes to fix the code.

# 12:04 Leveraging humans as computers

Most folks in my QA team didn't come from a technical background.
When one of my testers left the job shortly after I joined the team, it was suggested to me by development director that I could find good testers at the call centre.
This is because there was this view that to be a tester, you need to know how to use the application and the call centre folks knew how.
Interestingly enough, to be a developer you needed no such knowledge and so jobs could be outsourced ...

# 12:56 When first approaching automation

Typically, folks try to automate a manual test which is the least useful because e2e is really slow.
Also as he says, there's lot of implicit asserting. 
Not just the asserting but even data setup.
When I first suggested to my testers that the developers would run the same automation they're running, they had their doubts about it finding defects.
This is because they weren't putting in all the data needed for the setup or assertions.
In fact, some tests were written like mental notes; a developer just couldn't tell what was being tested specifically.
I aimed to test the most complex component automatically because it created the most difficult and time-consuming defects.

# 14:02 Best approach to start adopting the automated testing mindset

I started with coarse grained unit tests.
I actually at the time thought of them as component tests.
Later I saw that the developers were testing the system the same way as my QA team.
I wasn't sure whether to say the developers were doing component tests or my team was was doing unit tests.
Eventually I came across [Ian Coopers presentation](https://www.youtube.com/watch?v=EZ05e7EMOLM) and I'd now say they were unit tests.
As for tools at the level of whatever you're writing, this is where being able to transform our DSL into whatever COBOL code/files were needed was helpful.
Even though we were using Robot Framework or Cucumber, we didn't need the COBOL developers to know or use Java just to run a test.

# 15:24 Cultural barrier to automated testing adoption

The biggest barrier for me was not the technology, it was the culture.
In the COBOL dev team, the developers and testers had a great relationship long before I got there.
Sadly in the other teams, they and their managers thought it was someone else's job.
A director literally told me to shut-up and go do my job over a really low severity defect that I wanted the dev team to unit test.

# 16:30 Technical barrier to automated testing adoption

Trying to retro-fit the code base to make automated testing work is constrained by the architecture.
The system was developed without the constraint of being testable except by end-to-end testing and so they were untestable.
One example was that in production, customers couldn't delete a record, they could just terminate it and create a new one with a different effective date.
So the architects prevented any deletion operations being implemented which would make it hard to re-run tests in QA without creating more new data.

Because of such constraints, we started at a high level or component/coarse-grained unit tests.
This meant we needed the entire engine and database spun up just to run one test.
We'd then work on the edge of this reduced system and inject data via its file upload processes.

# 19:16 Approval testing

At the time I didn't know what approval testing was but I think my testers did something like it.
When they worked with developers in the lowest environment, they'd make a test, and then run it.
Though the test had some assertions, they'd see if what the code did matched it and if it didn't, they would have updated the assertion.
The reason for this is because some of the math was really complex and depending on where the rounding would take place in the system you'd get false failures.

# 26:26 Impact of testing on performance

This made me think of test automation performance.
When I joined the QA team, the COBOL testers used to run test automation for new features only at the end of the manual testing cycle.
Their automation would submit all the claims and then extract all the response from a database table.
When I suggested running each test and its assertions, folks hesistated thinking it would take them longer and slow them down.
The reality is that it did, it was twice as slow tbh. 
The trade-off was that it could be run more frequently with the possibility of one test being executed at a time.

# 30:30 How to change the development culture

It's a prerequisite that devs want to run the tests.
They don't need to even automate it, my enabling/platform team would help with that.
I waited for a developer that really wanted to and he became the tip of the spear.
Once he felt good and shared his positive experiences, only then would I approach others.
Whatever tools we used had to make it easy.
So if they were using a CPHA3 simulator that was homegrown, I started with that.
I didn't try to sell them on SoapUI or Cucumber etc, that came later.

# 31:29 Enabling team

My test automation developers eventually stopped automating tests.
They worked on the platform that let developers and testers auto-generate tests in whatever tools they were using.
They also worked on coaching and upgrading the manual testers.
We made it less work for the developer to run the test than not run the tests.
In fact as more time went by, and I learnt how the developers worked, I had a bias to make it easier for them to run the tests than my own testers.

# 35:13 Test framework constraints

I mentionned that the testers used Cucucmber (with Java) but the developers were COBOL developers.
So how does that work out? Basically the .feature files were converted into a UML model which then was converted into whatever we wanted.
When Dave talks about the framework constraining you, I realised that there was no version of Cucumber for COBOL or Cucumber for PLSQL or Cucumber for webMethods etc.
Just because my team liked writing tests in Cucumber doesn't mean it would work for the developers.
In order to decouple the specification from test automation implementation, I had hoped my team would just move to AsciiDoctor or Markdown.
That would then give us the flexibility to support any language via a library or REST API that could query the test model for the data.

# 43:30 To be continued