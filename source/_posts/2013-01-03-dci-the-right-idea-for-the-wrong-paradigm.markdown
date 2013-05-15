---
layout: post
title: "DCI: The Right Idea for The Wrong Paradigm"
date: 2013-01-03 01:10
comments: true
categories: [DCI, OOP, FP, Ruby, Lisp, Clojure, Design Patterns]
---

I've been following with great interest the recent debate over DCI vs. Concerns vs. Whatever in Ruby. The best take I've seen, however, is Tony Arcieri's recent post, ["DCI" in Ruby Is Compeltely Broken](http://tonyarcieri.com/dci-in-ruby-is-completely-broken). 

Reading his post, it ocurred to me that what Rubyists are trying to do with `object.extend(Module)` is precisely what Lisp hackers have been doing for years with macros, but it's an ugly hack when applied in the wrong paradigm (or, at least, the wrong language).

Now, I was initially a big fan _conceptually_ of DCI. It seemed intuitive, even familiar. And it helped that it was the brainchild of Trygve Reenskaug, the erstwhile inventor of MVC, possibly one of the most useful OOP patterns ever devised. 

But the more familiar it seemed, the more difficult it seemed to implement properly, much less efficiently, even in the purest of modern OO languages, i.e., Ruby. 

It wasn't until I tried to forget everything I knew about OOP that its familiarity became clear: this novel appropach to object-oriented design is embedded in the most natural thing in the world in the oldest of functional programming languages, Lisp.

Enter the macro. In Clojure, providing context to a function is straightforward using a macro, for instance, a database query (n.b., most of this is straight example code from [wikibooks.org](http://en.wikibooks.org)).

```clojure Set up JDBC connection http://en.wikibooks.org/wiki/Clojure_Programming/Examples/JDBC_Examples#PostgreSQL
(use 'clojure.java.jdbc)
 
(let [db-host "localhost"
      db-port 5432
      db-name "a_database"]
 
  (def db {:classname "org.postgresql.Driver" ; must be in classpath
           :subprotocol "postgresql"
           :subname (str "//" db-host ":" db-port "/" db-name)
           ; Any additional keys are passed to the driver
           ; as driver-specific properties.
           :user "a_user"
           :password "secret"}))
```
This provides the context for the `with-connection` macro:

```clojure SELECT Statement http://en.wikibooks.org/wiki/Clojure_Programming/Examples/JDBC_Examples#SELECT

(with-connection db 
   (with-query-results rs ["select * from blogs"] 
     ; rs will be a sequence of maps, 
     ; one for each record in the result set. 
     (dorun (map #(println (:title %)) rs))))
```

I'm using the simplest of (admittedly cribbed) examples here for the sake of demonstration, but right away here, we've got the D and C of DCI - Data and Context. As for interaction... we could easily conceive of a `with-role` macro which determines the interaction of the database connection and the actual application of the `with-connection` macro, whether it invokes a SELECT, CREATE, UPDATE, or DELETE statement. 

In a Lisp, this level of composition is completely _natural,_ is my point. In a language like Ruby (which despite having much of the Lisp nature, is OO to its core), and especially in a framework like Rails, with its cargo-cult Design Pattern-worshipping user base (I'm going to take some shit for that one, but accept that I'm exaggerating and flame with that in mind), is it any surprise that a pattern that makes _total sense_ in an FP context is going to be a hot controversy in an OOP context?

I agree with Tony's post that "DCI" in Rails is totally broken. But that's because, IMHO, DCI isn't the best pattern for OOP. Yeah, Ruby has _lots_ of functional features, but maybe we need to rethink how we're doing this DCI stuff (or Concerns, or whatever), on the basis that messing with inheritance and the class hierarchy is the _wrong thing,_ and perhaps we should be creatively exploring the use of blocks and lambdas and Ruby's other functional constructs. 

I'm not offering any solutions here, but I'm hoping I can contribute to the conversation. Step away from the mixins, away from the class hierarchy, away from the object model. Maybe take another read of Design Patterns and see if DCI is another hot YAGNI thing. I don't know yet. I just know it reminds me of how things are AWESOME in a whole other paradigm that doesn't necessarily apply to your Rails app.

As a caveat, I should say that I haven't really tried to use this DCI mojo in a production application, although I have played with different ideas about it Just For Fun&copy;. If you think I'm wrong, or have the whole thing arse-about-face, I'd be happy to discuss it in the comments.