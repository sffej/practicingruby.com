---
layout: post
title: Dirty Little Secrets about Testing
date: '2011-01-14'
categories: articles
author: Gregory Brown
permalink: articles/dirty-testing-secrets
---

Today I have a small rant about the test obsessed culture of Ruby. This area in particular is one in which the incredible enthusiasm surrounding the methodology seems to have outpaced the individual practitioner's ability to evaluate its utility. I'm not just talking about beginners here, but seasoned professionals as well. The sheer volume of rapidly changing testing tools and techniques is an indicator that we're nowhere near convergence, but that doesn't stop many from describing automated testing, particularly in the _Behavior Driven Development_ style, as if it were some sort of magic bullet. It isn't.

Speaking only from personal experience, I can tell you that most projects that I've spent more than a few hours hacking on end up better with some automated testing than they would with no testing at all. But I can also tell you that uses all the latest and greatest tools and techniques, and attempting to "test all the fucking time" on large scale, long running projects, has actually hurt rather than helped me at times.

Some tests are a waste of time, and other tests can be actively harmful. If you have ever experienced the pain of refactoring a test suite in which someone overzealously mocked everything except for the object under test, simply to 'decouple the tests from the implementation code', you probably have an idea of what I mean. If you happen to be one of those folks who are still writing tests that way, you should study a bit more about what mocks are actually meant to be used for.

Personally, I've found testing to get in the way when I'm first exploring a new project. I almost always spend a couple hours writing crappy code without any tests at all. Test-first development does help drive interfaces and forces you to think about API design continuously, but it can only really be used to attain a local maximum. When you're trying to get a feel for a whole new concept, what you really need is a lantern, not a laser. Not even story frameworks like Cucumber or Steak give me the level of flexibility I need, so I go without testing frameworks entirely in my initial spikes. The closest thing I get to 'automated testing' in the first few hours of a project is a few lines of example code combined with some printlining to let me see what my code is doing. Pretty much everything else gets done through poking and prodding in irb.

Typically, the tradeoff of velocity for code quality that I make in a spike fairly quickly catches up with me, and that causes me to start to think about adding tests and basically just starting from scratch, only using code if I feel it's good enough to refactor into something more permanent. With enough ideas generated, and a decent high level sense of what my goals are, the laser-like quality of unit testing becomes more useful. But there is still a lot of things I don't test, even once a project is under way.

I don't test complex interactions with users within a system, unless I begin to frequently write code that has system-wide effects. I've definitely been in situations in which integration tests have been vital, but they've been far and few in between. Part of this is because the projects I work on tend to be deeper than they are wide, but it's also because I just trust my design capabilities enough to not introduce too many changes that could break more than one part of my application at a time. I feel like the majority of integration testing goes into way too much detail about the expected paths through a system, and as a result, forces a bunch of false-negatives as minor changes that shouldn't affect users end up breaking tests.

Similarly, I don't place too much emphasis on testing things that I will invariably need to manually inspect. So for example, if I'm generating a PDF report, I don't typically bother testing my output in an automated fashion. What I will do instead is make it dead easy for me to generate that PDF so that I can look at it whenever I need to, and I'll keep a copy of the expected output around so that I can track down issues when they come up by doing some manual comparisons. Things would change somewhat if generating PDF reports was the core purpose of my application, but as a single feature, I feel automated testing would be mostly a waste of time.

There are other areas about testing that concern me, but I'll leave them for another day. For now, I'll try to end things on a positive note by sharing some of the areas where I do think testing is really, really helpful.

  * Dealing with regressions: In most scenarios, once you've created a minimal example to reproduce a bug, it's a small step to convert it into a unit test. As long as you introduce the test as far down the stack as possible, this minor investment is well worth the effort, as it will catch the bug and draw your attention to it if it ever gets reintroduced into your project.

  * Documenting project requirements: When written properly, tests say a lot more about intentions than implementation code does. Some folks feel that something like Cucumber and/or RSpec does a better job at expressing requirements than more low level testing frameworks, but this is primarily an aesthetic argument. No matter what framework you use, the purpose of a test is to describe how some code should be expected to work, which makes test suites a great way to learn about a project.

  * Safeguarding against harmful changes: For long running projects or projects with many developers, automated testing helps detect changes that have undesireable or unexpected side effects on the overall system. This is something that can also be dealt with by being well organized and fairly disciplined, but tests sure don't hurt. Of course, this effect is only accomplished if there is sufficient test coverage to catch those unexpected changes, an investment that may or may not be worth the effort.

Note that in the above, I didn't imply that testing results in writing better code. I also specifically avoided claiming that tests will help you avoid defects in the first place. While I think that occasionally testing contributes to accomplishing these two things, it really depends on the project as well as the individual developer's skill level and coding style. I also didn't claim that writing tests saves time or money. I don't think it actually does, and I wouldn't trust that claim until I saw some concrete evidence.

Even with these caveats, the gains listed in the bullet points above make the
juice worth the squeeze, in most cases. I can also say that automated testing
does make you think about software development in a very different way, and that
change in perspective might make you a better programmer. But testing is just
one of many things that can improve your craft.

So my humble advice to all Rubyists, newbies and seasoned professionals alike, is to cool your jets when it comes to testing. If we remember our main goal is to produce useful software, we can find room to make use of helpful techniques without letting them take center stage. This I think would be a huge step in the right direction.

  
> **NOTE:** This article has also been published on the Ruby Best Practices blog. There [may be additional commentary](http://blog.rubybestpractices.com/posts/gregory/050-issues-18-testing-dogma.html#disqus_thread) 
over there worth taking a look at.