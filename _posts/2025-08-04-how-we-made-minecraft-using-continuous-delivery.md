---
layout: post
title:  "How We Made Minecraft Using Continuous Delivery"
date:   2025-08-04
categories: engineering-room
---

<iframe data-testid="embed-iframe" style="border-radius:12px" src="https://open.spotify.com/embed/episode/5u3vGwdZwlqzhSGDZrx85q?utm_source=generator" width="100%" height="352" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

# Summary

A lot of what Henry describes is similar to what I experienced working with my QA team and the corresponding development team.

# 3:07 What triggered your interest

I was a developer and also found myself in a QA team.
I joined with the intention of making the lives of developers easier by changing the QA team to focus on earlier, not faster feedback.
When I started on the QA team, I knew nothing about QA processes.
Later I found that half of which appeared to be [testing theatre][13].

# 4:56 It takes a long time to find and fix things

The benefit adjudication engine was fairly complex.
When a mistake was made at a low level, it would take a long time for the QA team to identify where the issue was so that they could assign the bug to the right person.
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
The other 3 QA teams of mine had no such luck and so even with the same tools, we couldn't improve as much.

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
Also as he says, there's a lot of implicit asserting. 
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
Eventually I came across [Ian Coopers presentation][14] and I'd now say they were unit tests.
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
Though the test had some assertions, they'd see if what the code did match it and if it didn't, they would have updated the assertion.
The reason for this is because some of the math was really complex and depending on where the rounding would take place in the system you'd get false failures.

# 26:26 Impact of testing on performance

This made me think of test automation performance.
When I joined the QA team, the COBOL testers used to run test automation for new features only at the end of the manual testing cycle.
Their automation would submit all the claims and then extract all the response from a database table.
When I suggested running each test and its assertions, folks hesitated thinking it would take them longer and slow them down.
The reality is that it did, it was twice as slow to be honest; instead of 5, it would take 10 minutes etc.
The trade-off was that it could be run more frequently with the possibility of one test being executed at a time.

# 30:30 How to change the development culture

It's a prerequisite that devs want to run the tests.
They don't need to even automate it, my enabling/platform team would help with that.
I waited for a developer that really wanted to and he became the tip of the spear.
Once he felt good and shared his positive experiences, only then did I approach others.
Whatever tools we used had to make it easy.
So if they were using a CPHA3 simulator that was homegrown, I started with that.
I didn't try to sell them on SoapUI or Cucumber etc, that came later.

# 31:29 Enabling team

My test automation developers eventually stopped automating tests.
They worked on the platform that let developers and testers auto-generate tests in whatever tools they were using.
They also worked on coaching and upgrading the manual testers.
We made it less work for the developer to run the test than not run the tests (find and fix defects).
In fact as more time went by, and I learnt how the developers worked, I had a bias to make it easier to run the tests for them instead of my own testers.

# 35:13 Test framework constraints

I mentioned that the testers used Cucumber (with Java) but the developers were COBOL developers.
So how does that work out? Basically the .feature files were converted into a UML model which then was converted into whatever we wanted.
When Dave talks about the framework constraining you, I realised that there was no version of Cucumber for COBOL or Cucumber for PLSQL or Cucumber for webMethods etc.
Just because my team liked writing tests in Cucumber doesn't mean it would work for the developers.
In order to decouple the specification from test automation implementation, I had hoped my team would just move to AsciiDoctor or Markdown.
That would then give us the flexibility to support any language via a library or REST API that could query the test model for the data.

# 43:26 Bias for adoption and scaling

Adoption is a journey, you can't just tell someone to go do the thing.
I agree with Henry that you should first have a bias for adoption and then for scaling because adoption is the hard part.
I couldn't tell testers to just switch to Cucumber. 
I mean I could but I assumed back then and still do think that it would have either been stressful or they wouldn't have stuck with it.
This is why [Start with Why][1] was so useful, I needed to focus on the early adopters before I focused on the majority.
Just as he did, I noticed that once the developers could run our QA tests (which were basically unit tests) they now had more time and were more willing to create their own more low level tests.
Their tests would now focus on failures rather than meeting the requirements.

Meeting the code base where it is reminds me of [the Neo Nurture incubator][2].
We met the code base where it is by generating data or automation in a format that worked for the developers.
These were files uploaded by their COBOL scripts or submitting claims via the homegrown claim submission tool.
Later they moved to SoapUI and then Cucumber.

# 45:53 The problem with unit tests

How to write units tests without letting the whole system run? Well you let the whole system run as described [above][15].
One of the constraints of this approach is that we'd have leaky tests if we ran them concurrently.
Everything was run sequentially as a result which could take several hours.
Thankfully most legacy suites ran in a few minutes and by the time we got to Cucumber we were running individual tests in fractions of a second.
We also did functional isolation, the QA team was already doing this.

# 53:42 Domain Specific Languages

I'm going to start with stating that if it wasn't for a DSL and Eclipse Xtext, my entire transformation would have failed.
You start with why but you also need a how.
The reason we were able to move as fast is because of auto-generation of the test automation.
This meant that test automation developers were no longer automating any tests, they were out of a job.
They're new job was to automate the creation of test-automation.
This is no different that someone manually assembling a car was a robotic assembly line.

Let's say in the case of the COBOL dev and testers, there was a third person, the test automation developer.
How would that work out? Everytime the dev and tester had a conversation, you'd need this third person like a third person on a date.
Each time you finish having a conversation, you'd need to make sure this person is also on the same page.
Each time they make the code, there's a chance it's automating the wrong thing.
Each time they make the code, there's a delay, a non-value added activity in the lean world.
Instead by automatically creating automation from a formal DSL, from the moment an tester and dev have a conversation, there could be automated tests on the developers laptop in less than a minute.

What Henry describes about no-one writing tests reminds me of how the UAT team approached it and so it's interesting how they had the same outcome.
I think it's because both treated these tools as test automation authoring tools rather than a language for communicating with the business.
Also interesting about my QA team's test case writing style was that it was so clear that it could be given to our customers for review.
It was truly living documentation in my biased eyes :).
I should note that we didn't use Gherkin even though we used Cucumber. 
Instead of given, when, then, we just used the asterisk for every step.

When we were using Robot Framework, for various reasons, the DSL grammar wasn't very strict.
That meant that we'd wind up with keywords like:
1. click the button
2. click on the button
3. click button
4. click on button

Later, I could use regular expressions to find similar keywords and remove duplicates.
Eventually we adopted the Xtext framework with [prevented these mistakes][3] from happening.

# 56:59 Building your own DSL

I too only use DSL for higher levels of testing.
My current GitHub projects that demonstrate what I did on the QA team use the DSL editor to write tests and generate test automation.
The problem is when you want really low level tests, it's no longer a trans-literation exercise and so gets very challenging.
You can attempt it but then the code that creates the automation becomes really hard to understand which adds its own complexity and therefore sources of bugs.
Admittedly I don't have as many [plain solitary unit][4] tests as I'd like.

I mentioned [earlier][16] that I preferred we left Cucumber.
One thing I had experimented with is letting the team write .feature files and I extended the language.
That is, in our xtext editor allowed for a .feature file to have a Step-Object keyword followed by Step Definition, Step Parameter etc.
I was continually trying to make writing the test case as easy as possible.
Specifically I was trying to make writing a test case from which test automation could be derived as easy as possible.
I was also trying to make it easier for a non-SME to write a test case, kind of how I as a developer can use APIs to make something.
Also when a Cucumber test would fail, the stack trace would be really hard for someone to go through.
Being able to have our own plain junit/TestNG automated tests would have reduced that [toil][6] on the team.

I didn't think of it this way until Henry mentioned it but since we made the framework we could change it.
My team organically evolved through the tools, almost one per year until we got to Cucumber.
Every change was the result of the [PDCA and Kaizen][5].
Had I just forced the adoption of some testing framework, I don't think we'd have been as successful because folks wouldn't suggest improvements thinking they have to use it as is.

I think the developers should maintain the test automation.
There are tools like cucumber that have both specification and implementation.
They don't give you an API or library to browse through the specification and make your own implementation.
This makes it harder to adopt and organically merge into an existing way of working in the dev teams.
This is where Xtext helps because it creates that API that lets you do this.
I frequently told my dev team that paying someone else to automate a test or even run it was like delegating someone else to go to the gym for you.
They'll use the tools, have the community and know what to eat to get the awesome bod but it should be you doing those things.

# 1:01:59 Developers treating developers as users

I described in the [Deming Driven Testing site][7] that the dev teams were users of the data/feedback platform my QA team was trying to create.
In order to create empathy for the dev side of things, I slowly tried to get the testers to work like developers.
An example was having them understand the value of earlier feedback and how without it, there's more mistakes and rework like they experienced with writing tests.
I had the same QA team as their long time manager yet things were markedly better when I managed the team.
The difference was that it wasn't the people but the [system within which they work][10].
I was simply applying my novice level understanding of Dr Deming's 14 points and SoPK.

# 1:10:38 What value does this produce

I took a lean or continuous improvement approach for reasons I explained [here][11].
I described this process in this [blog post][12], basically I never needed a budget because of the small steps are removing rather than adding.
The goal was to reduce the waste after identifying the overburden that caused the fluctuation or in lean terms, reduce muda after identifying muri that caused the mura.
The metrics that showed things were getting better were QA execution time or defect remediation time or test automation creation time; everything went down.
Test automation coverage went up and so did developer and tester utilization.
I also agree that the moral argument isn't the way to go. 
My own team would hesitate at dropping test cases thinking it was the wrong thing to do.
I had no problem with doing so because I knew that quality can't be inspected in.
Dr Deming showed the Japanese how quality can be used for their competitive advantage, it wasn't about being morally right.

# 1:13:39 Support from leadership

So if everything was going as well, why did I leave my job.
Well, it was all going well until it didn't.
At some point the managers of the COBOL developers didn't like the idea of their devs running the tests.
They even [tried to get them to stop it][8].
I think it's because folks weren't comfortable with the idea that the QA team wasn't the last to touch the code.
This place was [pathological][9], if there were problems in production, QA was asked why didn't you test that.
With QA no longer running the tests, and the developers taking a bigger role, that wasn't going to fly.
I also mentioned that my boss's boss didn't like me much and neither did [my boss's peers][17]
I think the usual push back of there's no money for this didn't apply since we didn't need it.
The other push back of are we doing development wrong also didn't work because the developers willingly and enthusiastically adopted it.
Everyone just wanted things to stay the same; all the lean stuff was really foreign to the culture.

[1]: /demingdriventesting/Communicating%20the%20strategy%20to%20QA/Start%20With%20Why
[2]: /demingdriventesting/Communicating%20the%20strategy%20to%20QA/The%20Neo%20Nurture%20Incubator
[3]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Poka%20Yoke
[4]: https://martinfowler.com/articles/microservice-testing/
[5]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Kaizen
[6]: /demingdriventesting/Migrating%20from%20defect%20inspection%20to%20prevention/Muri
[7]: /demingdriventesting/Communicating%20the%20strategy%20to%20QA/Coach%20Teams%20Not%20Individuals
[8]: /demingdriventesting/Recipe%20for%20next%20time/Motivation
[9]: https://itrevolution.com/articles/westrums-organizational-model-in-tech-orgs/
[10]: https://deming.org/quotes/i-should-estimate-that-in-my-experience-most-troubles-and-most-possibilities-for-improvement-add-up-to-the-proportions-something-like-this94-belongs-to-the-system-responsibility-of-management6-sp-3/
[11]: /demingdriventesting/Communicating%20the%20strategy%20to%20QA/Gravity%20Slingshot
[12]: /sheepdogblog/shop-floor/2025/07/24/creating-pull-in-your-factory
[13]: https://dannorth.net/blog/we-need-to-talk-about-testing/
[14]: https://www.youtube.com/watch?v=EZ05e7EMOLM
[15]: #1630-technical-barrier-to-automated-testing-adoption
[16]: #3513-test-framework-constraints
[17]: #1524-cultural-barrier-to-automated-testing-adoption