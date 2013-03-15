---
layout: post
title: "The Myth of The \"IT Department\""
date: 2013-03-15 01:53
comments: true
categories: [information technology, management, programming]
---

So in the comments on my [last post](/blog/2013/03/11/confessions-of-a-job-destroyer/) I mentioned my fandom for what is, in my opinion, the most insightful and important blog currently published, that of [Michael O. Church](http://michaelochurch.wordpress.com/). His recent series of posts have been reviewing and analyzing the MacLeod theory of [organizational structure](http://michaelochurch.wordpress.com/2013/03/14/gervais-macleod-9-convexity/) (link is to the latest post in the series, but if you haven't been following it, therein are links to the previous eight).

I want to focus on the differential between concave (in which the difference between failure and middling is greatest) and convex (in which the difference between middling and superior is greatest) work.

### The "IT Department"

I have to start by saying "Information Technology" is a leaky abstraction. It covers everything from internal software development to the help desk call center. I'm not suggesting that either line of business is superior. Both are absolutely necessary, at least until developers start to become psychic or users stop being stupid, or (preferably) both.

The real problem comes when the same management structure is imposed in the guise of an "IT Department" on such divergent areas as the help desk, desktop support, network engineers, developers, and hardware techs. Going beyond theories [X, Y, Z, or A](http://michaelochurch.wordpress.com/2013/03/12/gervais-macleod-8-human-nature-theories-x-y-z-and-a/) of management, having a "Central IT" department is (without a revolutionary management strategy that will probably raise HR issues for most entrenched organizations) an attempt to shoehorn concave and convex work into the same tiny box, and is going to fail at appropriately managing one or the other (or perhaps more likely, both). 

<!--more-->

### Concave Work

Let's face it, help desk work is typically concave. I've done it (briefly), and it's probably an acceptable use case for [Theory X](http://en.wikipedia.org/wiki/Theory_X_and_Theory_Y#Theory_X), since it's (in this writer's opinion) rote, unrewarding work that I would [automate out of existence](/blog/2013/03/11/confessions-of-a-job-destroyer/) if I had the time and resources. But, it's also necessary work, and a place where "managing to the middle" works because achieving the Socially Acceptable Middling Effort (SAME) is a decent departmental average. 

I'd place much of the responsibility of the average sub-division of IT in the scope of "concave work."  Desktop support, Windows administration, etc., are really about uniformity of outcome, and SAME is an acceptable goal. 

When it comes to efforts like software development, or big data, or even "cloud services", SAME is the same as failure. We're now into the realm of convex work, and the standard has to be different.

### Convex Work

I've [written before](/blog/2012/10/31/feedback-loops/) about how programmers are just _weird_ from a standard, organizational point of view. Or any standard point of view. Programming is the ultimate convex work; from Joel Spolsky's warnings about [The Perils of Java Schools](http://www.joelonsoftware.com/articles/ThePerilsofJavaSchools.html), to Jeff Atwood's plea that [not everyone learn to code](http://www.codinghorror.com/blog/2012/05/please-dont-learn-to-code.html), it's clear that not only is programming a highly specialized thing to excel at, but also that there are [certain factors that determine capability in advance](http://www.codinghorror.com/blog/2006/07/separating-programming-sheep-from-non-programming-goats.html).

It's probably the epitome of convex work. The difference between the worst programmer and the middling programmer is a fraction of the difference between a middling programmer and (even) a 90th percentile-or-above programmer. And there are probably other areas in IT where this is true; from my experience I'd say they're in software-heavy areas like managing large datasets properly, or providing true "cloud services", i.e., computing and storage in a multi-tenancy environment with computation and storage as a metered service. I haven't seen any of these done well in an "enterprise" environment.

### The Enterprise

The "enterprise" only works by "managing to the middle." Which explains the self-defeating attitutdes of vendor lock-in and risk aversion. When you're not in a "tech company," IT is invariably a "cost center," which a) is why [you shouldn't call yourself a programmer](http://www.kalzumeus.com/2011/10/28/dont-call-yourself-a-programmer/) (obligatory reference), and b) why it needs to maintain a low-risk profile. When you work for a large organization, "low-risk" means "the buck stops elsewhere than my desk."  So there needs to be a vendor to blame. So much of the acknowledged efforts will be in contract negotiations for the purchase of almost-suitable software from an established vendor, that doesn't really meet the needs of the organization, but can be marginally tweaked to fit by middling engineers.

It also means that internal innovation can't be acknowledged or rewarded too highly. When most of your "software teams" are doing maintenance on the last failed vendor purchase, how can you be seen to give accolades to the projects which have truly broken new ground?

At the same time, do you _want_ front line support innovating to that degree? Sure, if one of your help desk reps replaces some annoying customer interaction with a Perl script, they'll either be promoted to convex work, or fired from concave work, right? I think this only reinforces the difference between the two categories.

### Programmer, Wat Do?

That's where the [MacLeod Paradigm](http://michaelochurch.wordpress.com/2013/02/19/gervais-principle-questioned-macleods-hierarchy-the-technocrat-and-vc-startups/) really comes into play again... when most of your developers are 9-to-5ers who [take no joy in their craft](http://decomplecting.org/blog/2012/05/22/passion/), you have a team of MacLeod "losers," which fits perfectly well into the "enterprise" IT paradigm. It's hard to practice something sensible like [open allocation](http://michaelochurch.wordpress.com/2012/11/25/programmer-autonomy-is-a-1-trillion-issue/) when you manage business analysts in the same manner as developers.

If you really care about good, clean, beautiful, (even) elegant code, well... you might luck out. I'm on a small team which is probably considered "rogue" by most "enterprise" standards. I love my job, and it affords me significant autonomy and creative freedom, but I also know how bizarre and rare that is. I don't see how "non-technical organizations" (a future post will debate whether such a thing exists anymore) can afford to treat developers' work the same as concave work without having the whole house of cards come tumbling down at some point.