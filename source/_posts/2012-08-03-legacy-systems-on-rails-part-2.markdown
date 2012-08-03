---
layout: post
title: "Legacy Systems on Rails (Part 2)"
date: 2012-08-03 11:38
comments: true
categories: [ruby, rails, legacy systems, databases]
---

This will be a quick one. I just wanted to give an example of how Ruby's open classes can be a lifesaver when a vendor makes bizarre choices, which you then have to deal with.

### Into the mouth of madness

So let's imagine you're a software engineer (actually, to make a decision this crazy, you'd probably have to have a title like Señor Software Architect, or possibly VP of Development). You need to store precise date values for an OLTP system in the database. Although you know that Oracle's TIMESTAMP datatype will store a time right down to sub-millisecond precision, that's just too easy. Or, at least, too sane.

Then you remember the [Julian day](http://en.wikipedia.org/wiki/Julian_day) system. Perfect! You can just use floats to reperesent the time, with the Julian day number as the integral part, and the time of day represented as the fractional part! Even better, you decide to make up your own offset instead of using a standard Day of Calendar Reform, _and_ to store the local time instead of UTC.

If you have ever considered something like this, step away from the computer. I'm revoking your programmer license. Leaving aside the general inaccuracy of floats (you wouldn't use a float to represent money, why the hell would it be a good idea for time?), there are _existing datatypes_ for this! Moving on...

### Monkey-patching to the rescue!

Since datetimes are represented as floating-point values internally, we'll need to have a way of converting between those and normal datetime types. So I'll start by introducing a few monkey-patches in an intializer, so they get loaded before anything else.

{% codeblock date_fixes.rb lang:ruby %}

# We need two values because the offset is from midnight instead of noon, 
# so the standard methods for handling Julian day values get confused.

SG1 = 2415019
SG2 = 2415018.5

class ::Float
  
  def vendor_to_dt
    date = DateTime.jd(self + SG1)
  end
  
  def to_date
    self.vendor_to_dt.to_date
  end
  
  def to_time
    t = self.vendor_to_dt
    Time.zone.local(t.year, t.month, t.day, t.hour, t.minute, t.second)
  end
end


class ::DateTime
  def to_vendor
    time = self.ajd.to_f - SG2
  end
end

class ::Time
  def to_vendor
    self.to_datetime.to_vendor
  end
end

class ::Date
  def to_vendor
    self.to_datetime.to_vendor
  end
end


{% endcodeblock %}


