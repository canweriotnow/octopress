---
layout: post
title: 'Be Willing To Let Go; or, "The Big Rewrite"'
date: 2013-04-05 02:10
comments: true
categories: [software, engineering, elegance, coding culture]
---

{% blockquote Alan J. Perlis %}

Is it possible that software is not like anything else, that it is meant to be discarded: that the whole point is to always see it as a soap bubble?

{% endblockquote %}

One of the most nerve-wracking things you can tell a manager is that it's time to rewrite a major software component, system, or application. In fact, it's considered (in some circles) such a mortal sin that Joel Spolsky addresses "The Big Rewrite" in a post entitled [Things You Should Never Do, Part I](http://www.joelonsoftware.com/articles/fog0000000069.html).

In many cases, he's absolutely right. If you have a working-ish production codebase, throwing it out the window can seem a bit like throwing out the baby with the bathwater. But from an engineering standpoint, software is weird. On the one hand, you have the engineering side: If a bridge is just working-ish, the assessment of a structural engineer might be that it must be torn down and a new bridge built in its place. Software is much more ethereal and abstract; of course, we can continue to patch the old application, and extend it, and patch it, and sacrifice virgins to Great Cthulhu, and keep it chugging along. For a while.

Eventually, however, with a typical enormous, legacy codebase, you just end up mortgaging massive technical debt. 

<!--more-->

### Refinancing and Bankruptcy

A large, enterprise-y system will usually be so entrenched in technical debt that we can (metaphorically) view it as being double- and triple-mortgaged. Test coverage is spotty (if it even exists), and more time is spent dealing with regressions than actually implementing new features in a sane manner.

Eventually, technical debt piles to the point at which it's time to claim bankruptcy. And the problem is that the beancounters financing software projects (or IT managers who have no business managing software projects) see it as bankruptcy in the traditional sense.

If the original project was poorly architected, rife with Demeter violations and cross-dependencies, this might be a somewhat accurate assessment. But sometimes a project with a sensible class hierarchy, composable elements, and a modular structure needs "The Big Rewrite", and it becomes difficult to explain what this really entails.

### Reusable code

I'm thinking about this in terms of a Rails app that I built some time ago, which really should have been considered a "throwaway prototype", except that the busness needs dictated it went into production right away. It works, but... lousy test coverage, bizarre performance issues, and regression issues make each new deploy a new headache. 

It took me some time, but I've finally made the argument for the "big rewrite."

Now, in the mean time, I've created a REST API for the backend as part of an SOA for the systems involved. And I've demonstrated that much of the model layer from the "deprecated" application was reused (or improved) for the API that I'm using to abstract the legacy system the inital application was designed to interface with.

The "big rewrite" entails rebuilding the tools in the old application to work through the API instead of directly hitting the DB (an Oracle monstrosity with ~460 tables and an incomprehensible collection of package functions and stored procedures). But the code was reusable in a new context, and the "rewrite" is really a protracted refactoring and rebuilding of the data layer.

### That Lisp Thing

The quote at the head of this article was taken from the preface to the second edition of [The Structure and Interpretation of Computer Programs](http://mitpress.mit.edu/sicp/), aka the "Wizard Book." SICP uses the Scheme dialect of Lisp for its examples, and Lisp is a beautiful language for writing disposable code. It simply _makes sense_ to write small, composable functions, and to use those functions to build abstractions for higher-level programming. This is what Paul Graham calls [Programming Bottom-Up](http://www.paulgraham.com/progbot.html). 

I think when Rails programming is done well, it has a similar bottom-up aspect, in that one starts with the data model, then deals with the controllers, and the views are the final consideration. Certainly not everyone approaches Rails development from this perspective, but I think the best Rails apps exhibit this approach. The Windows development model of "Visual Foo" and "Big Design Up Front" are the anithesis, and I think this is why most Windows programs are terrible (apologies to the good ones out there), and why most Windows programmers are okay with terrible code.

### Lewis's First Rule

{% pullquote %}

I've never even thought to come up with a "rule" of software design before, but this is the most important lesson I've learned in my 26 or so years of hobbyist, amateur, and professional software development. I think it's more important than any single design pattern (although many of the patterns in the Gang of Four book embody this rule), architectural principle, or other aphorism (excpet, of course, for [Hanlon's Razor](http://en.wikipedia.org/wiki/Hanlon's_razor), but that extends beyond software). Lewis's First Rule is simply this: {"All application code must be either composable or disposable."} By composable, I inherently imply "reusable." This is at the heart of the Go4 directive to "favor composition over inheritance." But I also want to insist that getting rid of code is okay. It's not only okay, it's downright _desirable._ There's no greater feeling than a git commit that
