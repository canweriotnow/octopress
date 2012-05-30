---
layout: post
title: "Hypermedia APIs: The New Wild West?"
date: 2012-05-30 13:26
comments: true
categories: [coding, web, API]
---

Two of the best presentations at RailsConf this year, **Designing Hypermedia APIs** by [Steve Klabnik](http://steveklabnik.com/) and **Rails: The Next Five Years** by [Yehuda Katz](http://yehudakatz.com/) were related to the topic of hypermedia APIs. The video of Steve's talk isn't up on Confreaks yet, but the slides are [here](http://steveklabnik.github.com/hypermedia-presentation/#1). I'll embed Yehuda's talk right here:

<iframe width="560" height="315" src="http://www.youtube-nocookie.com/embed/UlMpIHH1K5s" frameborder="0" allowfullscreen></iframe>

The two big takeaways from these talks (for me, at least): 

1. We've come a long way in designing in implementing APIs. But now we're to the "hard part": Going from REST to true hypermedia.
2. Rails is really, really good at creating de facto standards via "convention over configuration." But we don't go far enough, and that's where we shoot ourselves in the foot (think ActiveResource).

### Why don't you REST for a while?

I know, it's stressful figuring this stuff out.  Rails going all RESTful was a big help when it came to creating uniform interfaces for our applications. HTML, XML, JSON... you could have it your way, right away. But going from RESTful resources to true hypermedia APIs is an even bigger leap forward than the move to REST, and that transition also needs to be planned and implemented carefully and correctly.

`as_json` will only get you so far. Yes, it will represent the resource in a way that is eminently consumable by a client application, whether that's Javascript in the browser, a mobile app, or curl. But your client still needs to know _far_ too much about the structure of the resources on your server. That's tight coupling, which we all know is evil. It's even evilly-tight from a REST standpoint; if the client has to know _anything_ about server-side resources, you're breaking the encapsulation layer between resources and the representation of those resources, which is what REST is all about, right?

So what is to be done?

<!-- more -->

### HATEOAS

Yeah, there it is. **Hypermedia As The Engine Of Application State.** That last layer of REST that we'd rather not think about, much less try to implement. 

We know better, but we do all sorts of crazy things in order _not_ to do it right. One of the most common sins (I'm guilty myself) is embedding nested resources inside of the requested resource. 

What's wrong with embedding, for instance, comments in the JSON representation of an article?

If nothing else, when I request an article, I'm requesting a specific representation of a specific resource. I don't necessarily *want* all of its child resources or other associations. I should *know* about them, but not forced to accept them.

Furthermore, 

I really like the example Steve used of implementing a `links` array in the returned object:

```json Sample response http://steveklabnik.github.com/hypermedia-presentation/#47

request("http://w3clove.com/api/", 
  "application/vnd.w3clove.validation+json")
# =>
{
  "links":[
  {"rel":"website-form", "href":"..."},
  {"rel":"sitemap-form", "href":"..."}
  ]
}

```

What's especially interesting here is the Content-type: `application/vnd.w3clove.validation+json`. That was another big takeaway: I was unaware of the `vnd` prefix for defining your own content-types, rather than waiting (and waiting, and waiting...) for the W3C to define a standard. 

{% img float-right http://imgs.xkcd.com/comics/standards.png %}

Please don't take that as encouragement to go create 2^10 new content-types all willy nilly. Use something that exists, preferably an accepted standard, unless there *really, really* isn't an acceptable standard for your use case.

In that scenario, there's nothing wrong with defining a content-type that meets your needs, provided you thoroughly spec it and adhere to the spec.

### as_json is not the answer

I want to go a little further into why links > nested resources.

Let's say you have an `Article` class, which `has_many :comments` and `has_and_belongs_to_many :tags` You might think it's a good idea to do this:

```ruby article.rb

class Article < ActiveRecord::Base

  has_many :comments
  has_and_belongs_to_many :tags
  belongs_to :user
  
  def as_json(options={})
    options[:include] = {:comments => [], :tags => []}
    options[:except] = :user_id
    return super(options)
  end

end

```

It's not necessarily terrible, but it's not optimal. Normally you might get back:

```json

{
  article: {
    title: "First Post!",
    body: "Chillwave fixie food truck vinyl. Squid cred +1, cardigan sustainable before they sold out wayfarers twee synth. Retro cliche 3 wolf moon banh mi, put a bird on it hella american apparel sriracha ennui artisan beard. Small batch four loko cardigan, umami stumptown keffiyeh cray street art etsy. Whatever high life synth godard 3 wolf moon, brunch PBR hella banh mi gluten-free vegan next level mustache stumptown lo-fi. Ethnic photo booth pork belly wayfarers, cardigan blog etsy portland mumblecore single-origin coffee post-ironic shoreditch. +1 typewriter sriracha authentic artisan master cleanse, bushwick freegan keytar."
    comments: [
      {
        id: 1,
        body: "Dude!"
      }
    ],
    tags: [
      {
        id:3,
        name: "hipster-crap"
      }
    ]
  }
}

```

This might be okay until you end up with hundreds of long-winded comments about where to find the best kefir in Portland. And what if your client wants to follow the tags to find similar articles? Sure, they can assume you're following rails conventions for URIs and try to get "http://example.org/tags/3", but there's no guarantee that's what you're doing, and it's expecting too much of the client. What if you want to find more by the same author? you've decided in advance your clients don't need to see the user_id.

Worse, you're now eager-loading all of your associations, which, while preferable to a risk of n+1 queries, does mean you're banging on your database harder.

There's another added benefit: if *all* a resource needs to know about its associations is where to find them, you've just loosened the coupling between those classes. It's a Good Thing.

It occurred to me that there's an (imperfect) metaphor for this: pass-by-value vs. pass-by-reference. Rather than copying the value from the server to the client, you pass a reference where the value can be retrieved. Yes, I know this is closer to C pointers ("pass-by-value where the value is a reference") than than true pass-by-reference. Anyhow.

### Tradeoffs

There are definitely some potential latency-induced pitfalls here. By leaving the task of requesting the appropriate representations of the appropriate resources to the client, we're buying decoupling and a reduction in unnecessary database activity at the potential cost of *many* more HTTP requests. 

This might be true. But it just highlights a need that already existed: we really, really need to optimize HTTP. We need to use [keep-alive and pipelining](http://www.igvita.com/2011/10/04/optimizing-http-keep-alive-and-pipelining/), and we need to understand [TCP slow-start](http://www.igvita.com/2011/10/20/faster-web-vs-tcp-slow-start/). Among other things.

### The Wild West

Now, back to the title line. Hypermedia API design is kinda chaotic right now, with all sorts of possible solutions, from the clever and innovative to the completely brain-damaged.

One thing Rails has been pretty good at is pushing the envelope, gaining wide adoption of good ideas, and giving the other web frameworks something to aspire to/catch up with. We've seen this with MVC, REST, and now the asset pipeline. It is, to a large degree, the convention-over-configuration principle that drives this phenomenon, and in Yehuda's talk, he laments the state of ActiveResource, which is pretty useless for the most part, and (correctly, I think) blames the fact that we don't have a good convention for resource serialization, which ActiveResource could consume intelligently.

There are plenty of good options out there already; the [roar](https://github.com/apotonick/roar) gem recently got support for the [JSON-HAL](http://stateless.co/hal_specification.html) content-type, which I think is a great approach to HATEOAS, although not perfect.

The [draper](https://github.com/jcasimir/draper) has HATEOAS helpers listed as a TODO, and that'll be great. If you need decorators, you should definitely be using draper. If you don't think you need decorators, you're probably wrong.

Ultimately, however, I think for Rails applications to implement true hypermedia APIs in a consistent fashion, something needs to make it into Rails core that's better than the current serialization methods in `ActiveRecord::Base`. So I'm **really, really** happy about `ActiveModel::Serializers`. I think it points to the Right Thing. Please try it out, and use it in your apps. It's not in Rails core yet, but if we all start using it, there's a better chance of it being included in Rails 4. And that would be really, really cool. Better yet, you can fork and contribute to it (yeah, it's on my list to do... someday).

The "wild west" can be exciting, but it's not where most of us want to live. Building sane infrastructure allows us to work at higher levels of abstraction, and that's where the *real* fun and excitement lives, right?