---
layout: post
title: "DateTime Conversions in Clojure"
date: 2013-02-03 14:18
comments: true
categories: [datetime clojure]
---

In dealing with integrating data from disparate incomaptible systems (which I do to a degree that would drive some men mad), one of the most frequent irritations is dealing with datetime conversions.

A while ago, I [wrote a post about Bubba](http://decomplecting.org/blog/2012/08/03/legacy-systems-on-rails-part-2/) (not its real name), a legacy/vendor-supplied system in which the original developers (may they suffer eternal torment) decided to store all datetimes as floating-point values using a bastardized form of the Julian Day system with fractional day part. In that post, I showed a solution used in a Ruby on Rails web app, but now I'm writing data integration services for multiple systems, and needed something a bit more robust, so I'm writing it in Clojure. 

I'll start off with the dependencies:


{% codeblock lang:clojure %}

(ns project.util.date
  (:require [clj-time.core :as tm]
            [clj-time.local :as loc]
            [clj-time.format :as fmt]
            [clojure.math.numeric-tower :as math])
  (:use clj-time.coerce)
  (:import [oracle.sql TIMESTAMP]
           [java.sql Timestamp]))
{% endcodeblock %}

I'm using the fantastic [clj-time](https://github.com/seancorfield/clj-time) library by Sean Corfield. It's basically a wrapper around the [Joda Time](http://joda-time.sourceforge.net/) Java library, allowing us to use its powerful datetime handling in idiomatic Clojure.

So, for the actual code. First, the Bubba dates need to be converted to and from a floating point value to a normal Date object.

<!-- more -->

{% codeblock lang:clojure %}

;; Bubba DateTime conversions

;; Set day of calendar reform for TS julian dates.
;; And yes, it uses local time, not UTC. Because FML.
(def docr
  "It's the day of Calendar Reform for bubba"
  (loc/to-local-date-time (tm/date-time 1899 12 30)))


(defn fractional-part 
  "Get the fractional Julian day part from a DateTime"
  [dt]
  (let [
    hour-part (tm/hour dt)
    min-part  (tm/minute dt)
    sec-part  (tm/sec dt)
    seconds (+ (* hour-part 60 60) (* min-part 60) sec-part)]
    (float (/ seconds 86400))))

(defn to-bubbadt 
  "Converts a DateTime to a bubba Julian date"
  [dt]
  (let [offset docr]
    (+ 
      (tm/in-days
        (tm/interval offset dt))
      (fractional-part dt))))

(defn current-bubbadt 
  "Get the current local time as a bubba Julian date"
  []
  (to-bubbadt (loc/local-now)))

(defn from-bubbadt [bubbadt]
  (let [day-part (math/floor bubbadt)
        frac-part (- bubbadt day-part)
        docr docr]
    (tm/plus docr (tm/days day-part) (tm/secs (math/round (* 86400 frac-part))))))

{% endcodeblock %}

Okay, that's probably a lot to take in, but basically it performs the calculations to convert the floating-point dates to Date objects and back again. But there's still a catch. In some of the views I've built for reporting, I'm pre-converting those dates to Oracle SQL TIMESTAMP types, and depending on the context, sometimes those floats come back as Doubles, and sometimes as BigDecimals. 

Clojure's got me covered, with multimethods.

{% codeblock lang:clojure %}

;; Use a multimethod for our date coercion b/c the input type might be variable.
(defmulti bubba-date-coerce class)

(defmethod bubba-date-coerce Double [f]
  (from-bubbadt f))

(defmethod bubba-date-coerce BigDecimal [f]
  (from-bubbadt f))

(defmethod bubba-date-coerce oracle.sql.TIMESTAMP [ts]
  (from-date (.toDate ts)))

(defmethod bubba-date-coerce :default [d]
  (identity d))

 {% endcodeblock %}

 Much like generics in Common Lisp (well, CLOS anyhow) `defmulti` takes a dispatch function as an argument, in this case `class`, which returns the class of the argument passed to the multimethod. Methods can then be defined to handle each type of possile argument, with a `:default` method for unmatched cases. Multimethods can be used with any dispatch function you like, but `class` is a common use case, and handy as hell here.

 As I mentioned, the point of this is to get data in and out of multiple systems, and they all have their own idiosyncracies.

 For instance, there's, uhh, let's call it Joe's Directory, or JD, which stores all of its dates and datetimes as strings, with inconsistant formatting across the board. 

 Luckily, clj-time has awesome parsers:

 {% codeblock lang:clojure %}

 ;; General (jd DateTime conversions)

(def jd-parser 
  (fmt/formatter (tm/default-time-zone) "MM/dd/YYYY" "YYYYMMddHHmmssZ" "YYYY-MM-dd HH:mm:ss"))

(defn jdparse [date-string]
  (fmt/parse jd-parser date-string))



{% endcodeblock %}

Easy as pie. Where it gets truly beautiful, however, is when mixed in with [Korma](http://sqlkorma.com/) for SQL abstraction. Korma entities have two special macros for data conversion: `prepare`, which applies a function to data before storing it in the database, and `transform` which applies a function when reading from the database.

Since Korma returns query results as a vector of hashmaps, it's as simple as updating a hashmap:

{% codeblock lang:clojure %}

(defn jd-date-transform [rec]
  "Converts date strings to DateTime instances"
  (let [ent rec
        date-fields [:DOB :empstartdate :modifytimestamp :createtimestamp]]
    (reduce #(update-in % [%2] jdparse) ent date-fields)))

{% endcodeblock %}

That's the first version of the transform fn I wrote for JD, but there's two problems. First, the fields to apply are hard-coded in the `let` form. More importantly, however, is the condition where I do a `select` and don't return those fields; `update-in` will add the field with a value of `nil`.

So we need a higher-order function, and a bit of help from `clojure.set`

{% codeblock lang:clojure %}

(defn generic-transform
  "Transform function for queries. Arguments are a function to apply (f),
   the entity to be transformed, and the fields on which to apply the transformation."
  [f ent fields]
  (let [update-fn f
        ent ent 
        fields (vec (st/intersection (set (keys ent)) (set fields)))]
    (reduce #(update-in % [%2] update-fn) ent fields)))

{% endcodeblock %}

Finding the set intersection of the fields we normally want to transform, and the fields returned, ensures we don't get extra fields with values of `nil`.

And look, I resisted the temptation to use a macro where a function would suffice! Do I get points for good Lisp behavior?

Then it's as simple of using a lambda that applies this function inside our korma entity declaration:

{% codeblock lang:clojure %}

(defentity customers
  "Korma entity for the CUSTOMER table. Transforms Bubba datetimes to DateTime objects."
  (database envdb)
  (table :customer)
  (transform #(generic-transform dt/bubba-date-coerce % [:active_start_date 
                                                       :active_end_date 
                                                       :lastmod_datetime 
                                                       :birthdate 
                                                       :opendatetime])))

{% endcodeblock %}



So that's how I'm normalizing datetimes in this particular project. I'm really enjoying writing code like this: building short, composable functions and refactoring by decomplecting them into shorter, more composable functions. 

I find refactoring easier to reason about in Clojure than any other language I've worked in. Thinking in terms of simple, composable functions (particularly having the facility of higher-order functions and macros) also makes it very straightforward to decouple interface and implementation.

I'll state for the record I'm fairly new to Clojure, so it wouldn't surprise me if this code looks pretty amateurish to more experienced Clojurians. If anyone has any suggestions for improving it, I'd welcome the advice.