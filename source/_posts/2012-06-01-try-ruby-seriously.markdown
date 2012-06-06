---
layout: post
title: "Try Ruby... Seriously."
date: 2012-06-01 20:05
comments: true
categories: [Ruby, coding]
---

Every now and then someone comes to me for advice because they (or someone they know) wants to learn to code and has no idea where to start. Usually, the first thing I do is send them to [tryruby.org](http://tryruby.org), the awesome web-based REPL and tutorial the [Code School](http://codeschool.com) folks put together, based on [_why's (poignant) guide to ruby](http://mislav.uniqpath.com/poignant-guide/).

Lately, I've been wondering if that's the best advice. Only because I constantly re-evaluate *everything* on the chance that it might be sub-optimal. Ruby is pretty easy to learn, but it's also easy to learn terrible, terrible habits. Maybe a more constraining language would be more suitable?

I have to admit, as much as I generally [dislike Python](http://decomplecting.org/blog/2012/05/18/un-pythonic-for-fun-and-profit/), it probably _is_ the easiest language to learn, and it rarely gives you enough rope to hang yourself. So am I just letting my own prejudices guide my recommendations to other people?

<!-- more -->

Upon reflection, the language matters a lot less than the person. My egalitarian sensibilities make the idea that any reasonably intelligent person can learn to code, given the desire and determination, quite attractive. But alas, we must be wary of cognitive bias. It's become increasingly clear that [programming isn't for everyone](http://www.codinghorror.com/blog/2006/07/separating-programming-sheep-from-non-programming-goats.html). So as much as I like the idea that [everyone should know how to code](http://www.codinghorror.com/blog/2012/05/please-dont-learn-to-code.html), I have to admit that whatever innate ability it is that makes for a Real Programmer, not everyone has it. [Not even all of us working as software developers](http://www.codinghorror.com/blog/2007/02/why-cant-programmers-program.html).

I recently came across [this question](http://cs.stackexchange.com/questions/1954/criteria-for-selecting-language-for-first-programming-course) asking for "Criteria for selecting language for first programming course" on the [CS StackExchange forum](http://cs.stackexchange.com/). Answering that question ([here](http://cs.stackexchange.com/questions/1954/criteria-for-selecting-language-for-first-programming-course/1967#1967)) helped me to clarify some of the reasons I usually recommend Ruby.

#### Simplicity

Ruby is incredibly simple to pick up. Now, like anything, Ruby is hard to do _well_, but it is fairly straightforward to learn. My first language was BASIC on a [Texas Instruments 99/4A](http://en.wikipedia.org/wiki/Texas_Instruments_TI-99/4A). It was hard, but rewarding. I wrote stupid little games, and it was entertaining. Of course, I was 5 or 6 at the time... 

The point here is that you want two things for people who have never coded before: immediate positive reinforcement (it's fairly straightforward to make *something* that runs successfully), and a syntax that's easy get your mind around. Ruby fulfills those goals quite nicely.

#### Richness

Once you get past "Hello, World!" there's an almost infinite range of possibilities. Ruby does a very, very good job of providing a massive [collection of libraries](http://rubygems.org), and a flexible language that makes creating damn near anything not only possible, but at some point intuitive.

#### Multi-paradigm

Pretty much everyone starts with procedural code. That's okay, it's a start. But object-oriented and functional paradigms have many, many advantages. Ruby's pure-OO nature makes it very easy to transition into writing object-oriented code. It borrows enough concepts from Lisp that you can get a feel for functional styles as well. Contrast this to C++ or Python, where the object-orientation is tacked-on, and the bolts are definitely showing. 

#### Se habla Ruby

When it's a friend asking for advice, I'm fully expecting to be answering questions when they can't find an answer on [StackOverflow](http://stackoverflow.com). If they're learning Ruby, there's the advantage that I will probably be able to help with > 99% of their problems without Googling. Granted, this is true of a number of languages, but I probably wouldn't suggest that someone completley new to programming start out with C, Java, Scheme, Javascript, Clojure, or Perl just because I happen to know my way around them.

Finally, I like introducing people to Ruby because it's a language optimized for programmer happiness.

{% blockquote Yukihiro Matsumoto, http://www.artima.com/intv/rubyP.html %}
For me the purpose of life is partly to have joy. Programmers often feel joy when they can concentrate on the creative side of programming, So Ruby is designed to make programmers happy.
{% endblockquote %}

My hope, when someone shows an interest in creating software (or at least, learning what goes in to creating software), is that they'll fall in love with it like I did. I was bitten by the software bug when I was a little kid; it's been a hobby ever since. But it really wasn't until Ruby came along that I was certain I wanted to spend damn near every waking hour on this stuff. 

Why should I subject others to something less wonderful and joy-inducing than what I use every day?