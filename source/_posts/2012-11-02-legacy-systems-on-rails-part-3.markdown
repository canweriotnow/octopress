---
layout: post
title: "Legacy Systems on Rails (Part 3)"
date: 2012-11-02 13:25
comments: true
categories: [ruby, rails, legacy systems]
---

It's been a while since my last post in this series (if you missed them, here are parts [one](http://decomplecting.org/blog/2012/08/02/legacy-systems-on-rails-part-1/) and [two](http://decomplecting.org/blog/2012/08/03/legacy-systems-on-rails-part-2/)) but I wanted to return to the topic of building out Rails applications on top of legacy systems.

### Abstraction is your friend

I think if there's a common theme in these posts, it's abstraction. Primarily, using Ruby and Rails to abstract away the crazy implementation details of a system that's been accumulating cruft for over twenty years. I'm going to start referring to this system as "Bubba" for the sake of convenience (and since I don't have permission from the vendor to say what it actually is).

I mentioned in Part One that most of the access to the backend system going forward is occurring via a REST API wrapping the Oracle database that serve's as Bubba's back-end. Today I wanted to look at how the user-facing portions are constructed.

<!-- more -->

The customer-facing applications that integrate with Bubba via the API just send JSON back and forth at the model level. But our in-house developed applications are somewhat freed from tight integration with Bubba in that they handle persistence for their own data independently. So in addition to the Oracle DB, we also maintain a Postgres database that handles things like user sessions, application preferences, etc. I once complained about the inability to add tables to Bubba, but now I'm glad we were "forced" to add a separate database, one which we control and can write proper unit tests for our models (I think Part 4 will probably be about testing against legacy systems. It won't be pretty). 

Bubba is quickly becoming one component of _our_ systems, rather than _the_ system that we're just extending in various ways. 

One thing you'll find really quickly if you're trying to use a JSON API as your persistence mechanism is that ActiveResource is pretty inadequate if you were expecting an ActiveRecord-like API to use. I highly recommend the [reactive_resource](https://github.com/justinweiss/reactive_resource) gem by Justin Weiss as a substitute. 

Reactive Resource (among other things) adds read support for associations, including generating nested paths for child associations. So, for instance, the `Customer` object I described in Part 1 `has_many :cards`. ReactiveResource allows you to build models like this:

``` ruby
class Customer < ReactiveResource::Base

  has_many :cards

end

```

Reactive Resource will know to generate the URI `/customers/42/cards/123456` from `Customer.find(42).cards.first`.

### Encapsulation matters, too

Before I went this route, I tried the old "Rails can handle multiple databases just fine" theory. And while that's true in principle, in practice it often blows up in your face. First of all, you have to be very, very careful combining data from multiple sources - an ActiveRecord::Relation object when confronted with another object that quacks like a Relation will often try doing things like implicit joins - whcih obviously won't work across separate databases.

The other reason this approach was full of fail is Oracle. Oracle syntax is incredibly nitpicky about its non-standard quirks. I often found that attempting to do something as simple as an inner join on the Postgres DB, using a class that _knew_ to use the postgres adapter, syntax from the oracle_enhanced adapter would leak in. This _may_ be an implementation bug due to some hack in the oracle_enhanced adapter (maybe one day I'll ask Raimonds about it), but just knowing that that was possible convinced me that was not the right path. Having an API for interaction with Bubba, whose sole responsibility is interaction with Bubba, is much cleaner and easier to maintain.

### Don't be Lando

There's also one very, very good reason for quarantining vendor systems behind a REST interface. From time to time, the vendor is going to come along and ~~randomly change shit~~ release an upgrade.

![Imgur](http://i.imgur.com/qE6ko.png)

Maintaining a custom application dependent on a database schema beyond your control... let's just say you're gonna have a bad time. But wait, what's that? Gang of Four to the rescue!

{% blockquote  Gang of Four, Design Patterns %}
Program to an 'interface', not an 'implementation'.
{% endblockquote %}

Wrapping the system in an API for which _you_ control the public interface means you can account for schema changes in one place, rather than in multiple dependent applications, while keeping the public interface consistent. This also goes a long way in keeping your code DRY. And with a bit of metaprogramming magic like I described in part one, you can often spare yourself from having to push a new version if the schema changes are minor.

So, this post was a little light on code, but I did want to explain some of the reasoning behind this approach to legacy systems integration using Rails. 

#### Note

I'd like to thank the folks at the [Ruby5 podcast](http://ruby5.envylabs.com) for [covering this series in Episode #295](http://ruby5.envylabs.com/episodes/299-episode-295-august-7th-2012/stories/2616-legacy-systems-on-rails). If you missed that episode, please give it a listen... the commentary is pretty great, even if they did question my sanity a bit.