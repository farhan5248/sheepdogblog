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
What he didn't do is design only and then hand the design file to another team to press the simulate button.
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
