---
layout: post
title: "Code Typos Got You Down? Stop Worrying with close_enough"
date: 2013-03-01 18:32
comments: true
categories: [ruby, ruby-jokes]
---

From the crack team ([Micah Gates](https://twitter.com/micahjgates) and [myself](https://twitter.com/canweriotnow)) that brought you [job_interview](https://github.com/ruby-jokes/job_interview), I'm proud to announce the availability of [close_enough](https://github.com/ruby-jokes/close_enough), a gem that will save you from all of those niggling `NoMethodError`s that occur when you mis-type a method name.

The concept is very simple, and based on an algorithm used in most spell checkers and autocorrect systems currently in use. Calculating the [Damerau-Levenshtein distance](http://en.wikipedia.org/wiki/Damerau%E2%80%93Levenshtein_distance) between two words can reliably (within a certain margin of error) indicate whether a known word was inteded when an unknown term was encountered in user input.

In Ruby, we have a wonderful metaprogramming facility in `method_missing`. What we've done in close_enough is to monkey-patch `method_missing` on `Object` to calculate the Demerau-Levenshtein distance between existing methods and the non-existent called method, and invoke the nearest one if it's "close enough" (close enough currently being an edit distance of < 3).

<!-- more -->

## So how does it work?

It's pretty straightforward. Let's say you're speed typing, maybe on an unfamiliar keyboard (I use a Sun Type 5 at home, but usually Dell QuietKeys at work... very different layout and key responsiveness). Sure, typos are going to happen, and it can be annoying and slow you down. But with close_enough...

{% codeblock Close Enough Examples lang:ruby %}

require 'close_enough'

obj = Object.new
obj.closs

=> Object

str = "foo"

str.lentgh
=> 3

str.reserve
=> "oof"

ary = [1,2,3,4,5]

ary.mpa {|a| a + 2}
=> [3,4,5,6,7]

ary.reduck(:+)
=> 15

{% endcodeblock %}

It's that easy. Quick, inaccurate typing becomes a non-issue. Or, at least, a minor issue. Okay, really, you should never use this in any kind of production environment. 

It's available from [Rubygems](https://rubygems.org/gems/close_enough), and the source is on [Github](https://github.com/ruby-jokes/close_enough).

