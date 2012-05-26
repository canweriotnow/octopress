---
layout: post
title: "Simplicity"
date: 2012-05-08 10:15
comments: true
categories: simplicity, coding, beauty
---

### Machine Beauty

{% img float-left http://photo.goodreads.com/books/1171573120l/107615.jpg 250 %}

In his essay [Machine Beauty](http://www.goodreads.com/book/show/107615.Machine_Beauty), David Gelernter defines "machine beauty" as an inspired mating of simplicity and power. In software, I think this is also what we mean when we talk about "elegance." 



The Dijkstra quote that serves as a tagline for this blog is actually truncated; the full quote reads: 

> Elegance is not a dispensable luxury but a quality that decides between success and failure.

This is not (necessarily) an economic truth; few people would describe any product from Microsoft as elegant, but they have been economically successful. However, the painful experience of using Microsoft software, the unreliability of both systems and applications, the general clunkiness of Windows applications, indicates that the software here is indeed a failure.

Software is a failure when it becomes an obstacle to productivity rather than an aid to it; when you must serve the compiler (or interpreter) rather than the compiler serving you (think Java boilerplate). From an end-user standpoint, the failure comes when the interface imposes unnatural workflows and ceremony that interrupts the natural flow of completing a task.

Software is successful when you hardly notice it's there; when it becomes a natural extension of the self, an augmentation to human ability. In terms of systems, think of the Macintosh when it was introduced; nothing before had been so intuitive, and enabling. In terms of programming languages, Ruby leaps immediately to mind. It is so expressive that it no longer feels like "coding"; you are just expressing your thoughts in a syntax that feels almost immediately as natural as a spoken language.

<!-- more -->

### Simplicity Matters

One of the most interesting (inspiring?) talks at [RailsConf](http://railsconf2012.com/) this year was Rich Hickey's keynote entitled "Simplicity Matters". Here's the video, you should watch it:

<iframe width="560" height="315" src="http://www.youtube-nocookie.com/embed/rI8tNMsozo0" frameborder="0" allowfullscreen></iframe>

One of the most important points he makes, early on in the talk, is that we often tend to conflate "simple" with "easy," and this is far from accurate. It's all too easy to complect the design of languages, systems, and applications, rather than maintain simplicity and elegance. He's kind of (allusively) hard on Rails, but not without reason. One of the ongoing efforts in the refactoring and continued development of Rails is to simplify the codebase as well as the APIs. 

### Practical Elegance

There are two modern programming languages that I think exemplify the marriage of power and simplicity that constitutes elegance. The first, which I use every day, is Ruby. 

For instance, consider the following accumulator generator in C++:

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

Super clear, right? Readable? Oh, yeah.

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

Simpler than C++, sure. But you still have all these explicit calls to self, and a class definition that should be unnecessary in a functional construct like an accumulator generator. It's an improvement, but still ugly as hell.

Now let's look at Ruby:

``` ruby Accumulator Generator http://www.paulgraham.com/accgen.html

def foo (n)
  lambda {|i| n += i } 
end

```

Wow. Three lines of code (although it could be written in one). If you understand lambdas, it's obvious what's going on here at a glance. You initalize `foo` with a value, and it returns a lambda that will accumulate any values passed to it.

Ruby makes the solution completely obvious.

_Note: all examples above from [Paul Graham's website](http://www.paulgraham.com/accgen.html)_

### Clojure

The other language that has me in awe of its marriage of power and simplicity is [Clojure](http://clojure.org). Clojure is a Lisp dialect targeting the JVM, and I encourage anyone out there to explore it. Here's the above construct in Clojure:


``` clojure Accumulator Generator

(defn accum [n]
  (let [acc (atom n)]
    (fn [m] (swap! acc + m))))

```

Anyhow, it's a little less immediately obvious than in a language like Python or Ruby (or, for that matter, Lisps like Scheme or Common Lisp). Why is this? As I mentioned previously, Clojure, while technically an "impure" functional language (as in, side-effects are allowed), tries to treat side-effects as a special case; so, for instance, most data structures in Clojure are immutable. The `atom` construct in Clojure creates a reference type that can access shared, independent, mutable state. The `swap!` function allows the value of the atom to be updated.

"Wait," you might exclaim, "that seems harder to work with! Aren't immutable data structures introducing complexity!?!?"

Clearly, if you share this opinion, you've never tried to deal with concurrency. Clojure's preference for immutable data structures isn't _easier_ than the usual acceptance of side-effects; but it is _simpler._ Making me think before I do an operation for side-effects in effect makes me think hard about many cases where I have an opportunity to complect my code. 

I've heard the argument that Python's bondage-and-discipline approach to programmer freedom is comparable, but I call shenanigans. It's too much to go into here, but I think another day I'll go into everything that's wrong with "The Zen of Python."

Anyhow... I thought these preliminary thoughts on what simplicity really means would be a good start for a blog entitled *Practical Elegance.*







