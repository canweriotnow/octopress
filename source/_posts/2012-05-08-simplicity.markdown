---
layout: post
title: "Simplicity"
date: 2012-05-08 10:15
comments: true
categories: 
---

In his essay [Machine Beauty](http://www.goodreads.com/book/show/107615.Machine_Beauty), David Gelernter defines "machine beauty" as an inspired mating of simplicity and power. In software, I think this is also what we mean when we talk about "elegance." 

{% img http://photo.goodreads.com/books/1171573120l/107615.jpg 250 %}

The Dijkstra quote that serves as a tagline for this blog is actually truncated; the full quote reads: 

{% blockquote Edsgar Dijkstra %}
"Elegance is not a dispensable luxury but a quality that decides between success and failure."
{% endblockquote %}

This is not (necessarily) an economic truth; few people would describe any product from Microsoft as elegant, but they have been economically successful. However, the painful experience of using Microsoft software, the unreliability of both systems and applications, the general clunkiness of Windows applications, indicates that the software here is indeed a failure.

Software is a failure when it becomes an obstacle to productivity rather than an aid to it; when you must serve the compiler (or interpreter) rather than the compiler serving you (think Java boilerplate). From an end-user standpoint, the failure comes when the interface imposes unnatural workflows and ceremony that interrupts the natural flow of completing a task.

One of the most interesting (inspiring?) talks at [RailsConf](http://railsconf2012.com/) this year was Rich Hickey's keynote entitled "Simplicity Matters". Here's the video, you should watch it:

<iframe width="560" height="315" src="http://www.youtube-nocookie.com/embed/rI8tNMsozo0" frameborder="0" allowfullscreen></iframe>

One of the most important points he makes, early on in the talk, is that we often tend to conflate "simple" with "easy," and this is far from accurate. It's all too easy to complect the design of languages, systems, and applications, rather than maintain simplicity and elegance. He's kind of (allusively) hard on Rails, but not without reason. One of the ongoing efforts in the refactoring and continued development of Rails is to simplify the codebase as well as the APIs. 

There are two modern programming languages that I think exemplify the marriage of power and simplicity that constitutes elegance. The first, which I use every day, is Ruby. 

For instance consider the following accumulator generator in C++:

``` c++ Accumulator Generator http://www.paulgraham.com/accgen.html

template<typename T>
struct Acc {
  Acc(T n)
  : n(n) {}
 
  template<typename U>
  Acc(const Acc<U>& u)
  : n(u.n) {}
 
  template<typename U>
  T operator()(U i) {
    return n += i;
  }
 
  T n;
};

```

Super clear, right? Readable? Avoids mutable state? 

Hardly. But maybe it's not fair to pick on C++, simplicity was (sadly) never a design goal.
Python is a more modern programming language, it's designed to be easy for new programmers to learn.

``` python Accumulator Generator http://www.paulgraham.com/accgen.html

class foo:
  def __init__(self, n):
    self.n = n
  def __call__(self, i):
    self.n += i
    return self.n

```

Simpler than C++, sure. But you still have all these explicit calls to self, and a class definition that should be unnecessary in a functional construct like an accumulator generator.

Now let's look at Ruby:

``` ruby Accumulator Generator http://www.paulgraham.com/accgen.html

def foo (n)
  lambda {|i| n += i } 
end

```

Wow. Three lines of code (although it could be written in one). If you understand lambdas, it's obvious what's going on here at a glance. You initalize `foo` with a value, and it returns a lambda that will accumulate any values passed to it.

Accumulators are important constructs, and Ruby makes their generation completely obvious.
