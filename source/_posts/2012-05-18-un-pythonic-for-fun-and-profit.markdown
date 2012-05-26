---
layout: post
title: "Un-Pythonic for Fun and Profit"
date: 2012-05-18 15:01
comments: true
categories: [python, languages, coding]
---

This post isn't meant to play into some hacker holy war, nor is it intended to denigrate the usefulness of Python for various tasks. Steve Yegge has done [a much better job than I can](https://sites.google.com/site/steveyegge2/tour-de-babel) of explicating some of the issues other programmers have with Python, both the language and the community around it; I still agree with his remarks there.

But there *are* some (major, IMHO) issues with the "Pythonic" attitude toward programming. And they start with "The Zen of Python."

## The Zen of Python

There's a lot to like about [The Zen of Python](http://www.python.org/dev/peps/pep-0020/). On the first face of it, it's a pretty good set of principles:

    Beautiful is better than ugly.
    Explicit is better than implicit.
    Simple is better than complex.
    Complex is better than complicated.
    Flat is better than nested.
    Sparse is better than dense.
    Readability counts.
    Special cases aren't special enough to break the rules.
    Although practicality beats purity.
    Errors should never pass silently.
    Unless explicitly silenced.
    In the face of ambiguity, refuse the temptation to guess.
    There should be one-- and preferably only one --obvious way to do it.
    Although that way may not be obvious at first unless you're Dutch.
    Now is better than never.
    Although never is often better than *right* now.
    If the implementation is hard to explain, it's a bad idea.
    If the implementation is easy to explain, it may be a good idea.
    Namespaces are one honking great idea -- let's do more of those!

There's a lot here that would be attractive, if not obvious, to any given Rubyist or Clojurian. I think the problem is that Pythonistas tend to get hung up on the *bad* elements of the "Zen of Python", to the detriment of the positive ones. So I'll just go through some of the ones that cause the most friction with non-Pythonistas.

<!-- more -->

### 1. There should be one-- and preferably only one --obvious way to do it.

I think this is the elephant in the room. Whereas Perl, Ruby, and (my god, to such a degree) Lisp are firmly in the [TMTOWTDI](http://catb.org/jargon/html/T/TMTOWTDI.html) camp, Guido in his infinite wisdom has decreed that this principle (one vital to *programmer freedom*) should be abjured in favor of strict newb-safety, via the principle of having ONE way to do any given thing.

{% img float-right /images/helen-lovejoy.png %}

This is a real design flaw with Python. Valuing newb-friendliness over developer productivity (and happiness?) is great if you're designing a strictly academic language. 

Actually, I take that back. It's still a bad idea. Python shouldn't even be used as a teaching language, because it confuses students. I've had first-year CS majors try to convince me that Python is as object-oriented as Ruby. This simply isn't true; Python combines a hodgepodge of paradigms (granted, Ruby does as well), but at its core, Python is a procedural language with some OO tacked on as an afterthought, and you can still see the bolts. It has more in common with C++ than Smalltalk, in this respect. But if you're learning your entire concept of object-orientation from Python, and you have a teacher or professor telling you it's OO, how are you to know better.

Getting back to the TOOWTDI principle, this is a more egregious violation of programmer freedom than significant whitespace (how I format my code is a personal, or team decision; I don't need a language designer telling me how to indent). It's so severe with Python that Guido originally planned to [remove map(), reduce(), and lambda](http://www.artima.com/weblogs/viewpost.jsp?thread=98196) from Python 3000.

The argument from Python's BDFL was that `map()` and `reduce()` were confusing and only existed in Python because some [Smug Lisp Weenie](http://c2.com/cgi/wiki?SmugLispWeenie) had submitted them 12 years previously, and that list comprehensions were the Pythonical-Canonical way of dealing with lists. Okay, list comprehensions are okay and all (I'll leave aside the debate over whether they are in any way more readable than functional constructs), but _who is it hurting to offer alternatives?_

Ruby has `#map` and `#reduce`, as well as `#collect` and `#inject`, which are aliases for the previous two methods (respectively). This doesn't stop you from iterating over lists instead, using generators, or anything else you'd like to do. It just seems like a combination of "I don't like the functional style, so nobody else can have it either," along with "this might confuse a newb, and we'll lose another convert!", or something.

### 2. Beautiful is better than ugly.

Can't argue with this one. Beautiful is _most certainly_ better than ugly. When it comes to the Zen of Python, however, beauty is most definitely in the eye of the beholder. 

In a [previous post](/blog/2012/05/08/simplicity/) I used David Gelerntner's definition of "machine beauty," i.e., "an inspired mating of simplicity and power." I think this holds true, and is at the core of what we recognize as elegance in software.

Sadly, I think it is quite clear that this is _not_ what the Python community means by "beauty." Python is always only too eager to sacrifice power (and even expressiveness) on the altar of a shallow view of "simplicity." 

I can think of no better example than `lambda` in Python. Not only are Python lambdas a neutered shadow of lambdas in Ruby or Lisp, their mere existence irritated Python's BDFL to the point that he wanted to excise them from the language altogether. (For more on lambas (and other syntax) in Ruby and Python, read [this](http://peepcode.com/blog/2010/what-pythonistas-think-of-ruby) and then go watch [this](http://vimeo.com/9471538).)

Now, I won't go into lambdas and why they matter here, I'm sure you know how to Google. The point is that the Pythonic tendency, when confronted with a "distasteful" construct, seems fall into three categories (with possible overlap):

- Ban it from the language before implementation
- Remove it from the language, breaking backward-compatibility
- Make its userspace implementation impossible.

Pythonistas are typically horrified by the fact that in Ruby, you can monkey-patch `Object` and extend the language in novel ways. I'm not sure how most Python aficionados feel about Lisp ([Peter Norvig](http://norvig.com/python-lisp.html) notwithstanding), but I can't imagine them being too friendly toward macros.

### 3. Simple is better than complex.

The reason I called Python's concept of simplicity "shallow" is that it conflates "simple" with "easy." 

Having multiple ways of doing something does not complect a programming language. Arbitrarily jumping between multiple possible implementations within the implementation of a single program _does_ complect that codebase, but that's why self-discipline is an important programmer trait. 

Self-discipline is important. I don't need a programming language to impose this from without, and I _especially_ don't want Guido making these decisions for me. I don't use [bondage-and-discipline languages](http://c2.com/cgi/wiki?BondageAndDisciplineLanguage), and neither should you.

Seriously, guise.

### 4. Explicit is better than implicit.

I don't care what your philosophy is, passing `self` as an explicit parameter is just evil.

### Finally...

Well, there was more I was planning to cover, but this post is long enough as it is. I'll probably do a follow-up at some point in the future. If you think I'm completely wrong, or just wrong on any of the points here, tell me why (nicely, please) in the comments.