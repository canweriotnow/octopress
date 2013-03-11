---
layout: post
title: "The Social University That Could Have Been"
date: 2013-03-10 22:21
comments: true
categories: [Social Media, Higher Ed, Ruby]
---

This is a post I've wanted to write for a while, but I've needed time and distance to do it justice. This is a post about (from my perspective) the greatest failure of my professional career.

## The Social University

Sometime in 2011, I was joking with my team lead about connecting [Blackboard Transact](http://www.blackboard.com/platforms/transact/overview.aspx), the OLTP product used for access control, stored value account transactions, and meal plans at my work, to Twitter, just for fun. The short answer was "that's silly." The longer answer was "that's silly, but it would be pretty neat."

So on lunch breaks and when I was waiting on other things to move forward with my "official" projects, I played around with creating a system to connect our system to Twitter.

Since I had already worked on a service layer for (really, a generalized SOA for systems connecting to) Transact, it was pretty easy to leverage APIs from not only Twitter, but also Foursquare and Facebook to tie into transactions from our internal system; door access could tweet your location, and check you in on Foursquare; buying a coffee could do the same. 

Eventually, the idea gained some traction, and we started building in a system of social gamification, that would award badges and achievements for usage of the system, ranging from customer loyalty rewards for particpating vendors, to seemingly "silly" things like a "Speed Demon" achivement for swiping two doors on opposite sides of campus within ten minutes.

The system also allowed students (well, also faculty and staff) to connect to Facebook to share badges/achivements and compete in a university-wide leaderboard. This is just an overview of the social media integration and gamification elements, but you might very well ask, what's the point?

<!--more-->

## The Univerity Lifecycle

There are three major phases in the lifecycle of the relationship between a university and its students: recruitment, retention, and alumni devleopment.

What this comes down to is attracting students, making sure they stay long enough to graduate, and then soliciting donations from alumni. The brilliance (if I may be pardoned a lapse in humility) of our software was the long-term goal of uniting all three. Students would be able to opt-in to the social media components as soon as they were accepted; the core components (targeted toward current students) would be integrated with their day-to-day activities on cmapus; and participants would be able to remain "in the game" long after graduation, creating a lasting bond between the university and alumni (far beyond attendance at the occasional lacrosse game). 

Our eventual goal was to connect these three phases through social media to make the university experience tightly integrated with the lifetime online experience of students, faculty and staff.

## It's All About The Data

So, making college more fun and exciting across the three phases of invovlement is well and good, but where does it start to get interesting? In the data. 

Once you go beyond the immeidate day-to-day, and start harvesting data like tweets and facebook posts (for sentiment analysis), Foursquare and other location-based data (to track geographical patterns), and LinkedIn for career trajectory data, you can start to analyze interesting patterns and create predictive analyses based on the large volume of voluntarily supplied data. 

In the end, it's a positive-sum game; students have a more engaging experience, the univeristy has a better dataset to analyze to make informed decisions about resource allocation, recruitment, and alumni giving, and it's a damn fun project to work on.

## Failure

Why do I consider this the greatest failure of my professional career? 

In some ways, it was a resounding success. Departments from athletics to applied math were clamoring for it; we were asked to present the project at the annual conference for Blackboard Transact, and then asked to do an encore ([You can find the slides here, by the way](https://speakerdeck.com/canweriotnow/j-card-social)). Our student focus group thought it was one of the best things they'd ever seen.

I consider it a failure because we never got to ship. ([If it doesn't ship, it doesn't exist.](http://johndbarry.com/2012/07/if-it-doesnt-ship-it-doesnt-exist/)) Sure, it was functional, and even "live" on our production server for about a week before our official launch date. But in that last week, the project was "indefinitely shelved". 

{% img center /images/post-img/remove-that-code.jpg %}

I never really got a clear reason for that (there were meetings between deans and lawyers and managers to which I was not privy), but the official, documented reason was that the project itself (which we worked on over the course of a year or more) was "never requested or approved", which is why I'm blogging about it now. I may never be able to share the source code (work-for-hire is pretty explicit), but I think the idea, which originated with me, should be free to the world if my employer disavows any ownership of it.

## That Vision Thing

Okay, this header is the title of an episode from Seson 3 of _Angel,_ but I'm also referencing one of the Bible verses my mom likes to quote. It's from Proverbs, not sure exactly where, but the line is, "My people perish for a lack of vision."

This could be the most relevant prophetic statement to higher education in our current economic and technological climate. Last year, Sebastian Thrun, Stanford prfessor, Google researcher, and founder of [Udacity](http://udacity.com/) famously stated in a [Wired article](http://www.wired.com/wiredscience/2012/03/ff_aiclass/all/) that "Fifty years from now...there will be only 10 institutions in the whole world that deliver higher education." My argument is that those will be the insitutions with the vision to risk everything to remain at the forefront of the marketplace. 

Does allowing students to tweet their lunch purchases accomplish this goal? Certainly not. But the lack of vision that hedges its bets and plays it safe certainly does not bode well for the university that wishes to survive the next several decades.

