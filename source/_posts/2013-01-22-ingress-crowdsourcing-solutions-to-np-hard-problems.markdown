---
layout: post
title: "Ingress - Crowdsourcing Solutions to NP-Hard Problems?"
date: 2013-01-22 19:12
comments: true
categories: [Ingress, Google, games, computation]
---

So I don't blog much about my gaming habit, but I recently got my invite to [Ingress](http://www.ingress.com), Google's new location-based MMORPG. Much has been written about the extensive (one might even say brilliant) [viral marketing campaign](http://www.nianticproject.com) that launched the game, and there has been some interesting speculation as to Google's motivation in producing such a game, ranging from the [begrudgingly admiring](http://www.reddit.com/r/Android/comments/138res/google_launches_ingress_a_worldwide_mobile/c71v7yv?context=2) to the [borderline paranoid](http://pandodaily.com/2012/11/19/googles-ingress-is-more-than-a-game-its-a-potential-data-exploitation-disaster/).

True, a persistently location-aware app that collects GPS and accelerometer data the entire time it's active has obvious implications for a data-ravenous company like Google. And I've seen a few reasonable theories so far as to the "real" motivation behind the game (and Google's "real" motivation - always and everywhere - is surely data). A breakdown of what I've seen so far:

1. Ingress is about tracking player "areas of operation" - the assumption being that you'll be playing most in the areas you habituate anyway - harvesting data for better location-targeted ads. Google is essentially an advertising company, so this makes sense.
2. Ingress is about improving Google Maps with pedestrian and footpath data - the Maps product is pretty great for driving, but as for routing pedestrian traffic, well... I've had it suggest a longer route because the shorter would involve _walking_ the "wrong way" down a one-way street. Walking directions are improving, but they rarely suggest cutting through a park, for instance, even when it would save 20 min. traveling time. And that kind of data is hard to get in an automated fashion, and often involves undocumented local knowledge. Using Ingress not only gets players to collect footpath data, but leverages local knowledge of pedestrian routes.

I think both of these theories are probably accurate, but they don't go far enough. 

It was actually during an extended period of playing Ingress last week that it occurred to me... I was plotting a run around the college campus where I work and thought to myself, wouldn't it be a neat feature if the game could help me plot the most efficient route between all these portals.

##### Yeah. See it yet?

<!-- more -->

My first reaction: "LOL, Jason, you so crazy... you want an app to solve the Travelling Salesman Problem problem for you?"

{% img center http://imgs.xkcd.com/comics/travelling_salesman_problem.png xkcd - Travelling Salesman %}

##### How about now?

My second reaction recalled something I'd read on Wikipedia a while back:

{% blockquote Wikipedia http://en.wikipedia.org/wiki/Travelling_salesman_problem#Human_performance_on_TSP Human Performance on TSP %}

The TSP, in particular the Euclidean variant of the problem, has attracted the attention of researchers in cognitive psychology. It is observed that humans are able to produce good quality solutions quickly. The first issue of the Journal of Problem Solving is devoted to the topic of human performance on TSP.

{% endblockquote %}

Gah.

[Comparisons have already been drawn](http://betabeat.com/2012/11/much-like-goog-411-googles-new-augmented-reality-game-ingress-is-a-genius-ploy-to-get-you-to-collect-data/) between Ingress and GOOG-411, but typically in the realm of "collecting data for an unrelated purpose." 

My theory is that it's much more similar than that; just as GOOG-411 was an attempt to crowdsource spoken phonemes to build an incredibly massive training set for voice-recognition machine learning algorithms, Ingress is an attempt to see how people heuristically solve the Travelling Salesman problem, create a training set based on all of the data collected, and tune new algorithms to compute the best routes (accelerometer and GPS-based rate-of-speed data can easily be used to account for both walking _and_ driving solutions).

So, yeah, it's probably all of the above, but IMHO the most interesting is the theory (it's just a theory, Google are being characteristically tight-lipped about their plans for all that Ingress data) that it's a new (hitherto infeasible) approach to one of the classic hard problems of computability theory.

##### Okay, fine, but what about gameplay?

Yeah, the point of this post was speculation on the really cool stuff Google's (potentially) doing with all that data, but a blag post about a video game wouldn't be complete without at least a bit about the game itself.

So, Ingress is fun. Like, incredibly fun. I've played other location-based MMORPGs, and some of them are decent, but none as immersive or addictive as Ingress. What started as a viral marketing campaign (the [Niantic Project](http://www.nianticproject.com/) website) is now a big part of Ingress "intel"; it ties in to gameplay in other ways as well, publishing puzzles that lead to scanner activation codes (i.e., publically-available game invites for the first one to solve the problem) and to in-game passcodes that provide resources and AP (Ingress' version of experience points, used for levelling). 

The puzzles are complex and extensive. Some remind me of the recruitig billboards Google had a few years back... I wouldn't be surprised if the codes at the end of the more difficult puzzles eventually resulted in recruiter emails from Google.

As for the game itself... I think it's one of the more positive and beneficial games I've seen... I used to walk about two kilometers a day, to work and back again. Now I walk at least twice that, and possibly up to 10km if I go out for an extensive "run" (my phone's battery won't last much beyond that, not with the Ingress "scanner" running).

The social aspect is also pretty damn great... our local 'Resistance' cell coordinates activities on a Google+ group, and thanks to that coordination, I was able to cover the campus where I work with beautiful, blue Resistance control fields - it was completely Enlightened-controlled just last week.

{% img /images/post-img/ingress-intel.png %}

The graphics are also incredibly stylish, abandoning the typical cartoonish mobile-game graphics for a style reminiscent of Tron, or the sort of data visualization I used to imagine reading William Gibson novels as a kid. Quite appropriate for a game with a heavy cyberpunk-dystopia vibe.

So, it's a fun game, that's making me healthier and more social. As a rather sedentary, introverted hacker, that's not a bad thing. If Google is managing to train some incredible new algorithms for routing pedestrian traffic as part of the bargain, I'm happy to help. The great thing about software is that when you get right down to it, when done well, it's usually a postivie-sum game. I know we live in a reduced-privacy world, but the typical kneejerk reaction toward zero-sum analyses is a bit misguided, in my opinion. Then again, as Scott McNealy famously said, more than a decade ago: 

{% blockquote Scott McNealy http://www.pcworld.com/article/16331/article.html Private Lives? Not Ours! %}
You have zero privacy anyway. Get over it.
{% endblockquote %}

Oh, well. Guess I'll just have to...

{% img center /images/post-img/keep-calm-claim-portals-resistance.png 500 %}