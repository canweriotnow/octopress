---
layout: post
title: "Static Is Beautiful"
date: 2012-07-04 23:21
comments: true
categories: [web, generators, ruby, blogging]
---

[My last post](/blog/2012/07/03/internet-culture-101/) was a bit off-topic, so I want to return to the core subject matter of this blog, elegance and simplicity in technology.

One trend that seems to be popping up again and again is the move away from over-featured and unmanageable content management systems (I'm looking at you, [Wordpress](http://wordpress.org/)), and toward static site generators. 

This blog, for instance, is generated from [Markdown](http://daringfireball.net/projects/markdown/) files by [Octopress](http://octopress.org/). More on Octopress later, but I want to survey the trend a bit.

This post was prompted by one of the auto-tweets by [@rubygems](https://twitter.com/rubygems), about yet another static site generation tool called [gumdrop](https://rubygems.org/gems/gumdrop). I've been playing with a few different static site generation tools, so first I'd like to survey a few examples, and then I'll talk about why I think they matter.

<!-- more -->

### Jekyll

[Jekyll](https://github.com/mojombo/jekyll) is kinda the all-father of the current crop of static site generators. Created by [Tom Preston-Werner](http://tom.preston-werner.com/) of [GitHub](https://github.com), it powers many, many [GitHub Pages](http://pages.github.com/) sites, and is pretty much pure awesomesauce. It's very bare bones, but that's what allows for such enormous flexibility. It's also what allows Jekyll to serve as the backbone of something like Octopress.

### Octopress

[Octopress](http://octopress.org) is my current favorite, as I use it all the time to power [this blog](http://decomplecting.org). Octopress wraps Jekyll with a bunch of templating goodness, which you can easily customize to your heart's content.

One of the best thngs about Octopress, however, is its plugin system. Not only does it come pre-loaded with some snazzy plugins for the [Liquid](https://github.com/Shopify/liquid) template language, but it makes it easy to extend with your own clever hacks.

Better yet, as it's a hacker-oriented blogging engine, it makes it dead simple to set up common widgets and services, from a GitHub repo listing to Google Analytics, just by editing `_config.yml`, the global configuration file.

Best of all, new post generation, testing, building, and deploying are all handled by `rake` tasks, and deployment via GitHub Pages, [Heroku](http://heroku.com), and `rsync` are easy as hell to configure.

### Middleman

[Middleman](http://middlemanapp.com/) is a newer static site generation tool, with all the sauce. You can template/style/script with Haml, Slim, Sass, Compass, CoffeeScript, and I'm sure others. It comes with [HTML5 Boilerplate](http://html5boilerplate.com/) baked in (if you're not using this, you probably should be), and it's built around [Sinatra](http://www.sinatrarb.com).

I haven't deployed Middleman anywhere yet, as the only static-content site I'm running right now is this blog, but it's definitely on the radar for the second I want to branch out from blogging with this domain (or any of my others).

### Gumdrop

I know way less about [gumdrop](https://github.com/darthapo/gumdrop) than about the other static site generators out there... but the [sites powered by gumdrop](https://github.com/darthapo/gumdrop/wiki/Sites-Using-Gumdrop) are nothing if not impressive. Gumdrop bills itself as "The sweet 'n simple cms/prototyping tool for creating static html websites and webapps."

I can't argue. The generation looks slick and simple, but also powerfully configurable, thanks to the awesomesauce of Ruby blocks.

I'll definitely be playing with this in my *copious* spare time.

## Why Static Site Generation Matters

It's pretty simple, actually. It all comes down to Wordpress. 

<blockquote class="twitter-tweet tw-align-center"><p>And there's only one thing worse in my eyes than PHP, and that's Wordpress PHP <a href="http://t.co/C40EfvOD" title="http://buff.ly/LkQIWH">buff.ly/LkQIWH</a></p>&mdash; Michael Robinson (@pagesofinterest) <a href="https://twitter.com/pagesofinterest/status/220254607849426946" data-datetime="2012-07-03T20:36:05+00:00">July 3, 2012</a></blockquote>
<script src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

We all *know* PHP is [a terrible excuse for a programming language](http://me.veekun.com/blog/2012/04/09/php-a-fractal-of-bad-design/), and also that the blogging platform wars, until recently, came down to only WordPress vs.  [Blogger](http://www.blogger.com). Of course, [Tumblr](http://tumblr.com) and [Postero.us](http://postero.us) have breathed new life into the blogging platform wars. But unless you wanted only the most basic features a hosted platform (everything but WordPress, honestly) provided, you'd need to settle on WordPress, because as an open-source platform, it had this ~~great~~ almost usable ecosystems of custom plugins. And somehow, the blogging community convinced ourselves we *needed* this plugin marketplace.

Now, don't get me wrong. As economies go, the WordPress plugin market has proved a lucrative environment for many freelance PHP developers I know. Mind you, because they were writing WordPress PHP 8-10 hours a day, their mental states ranged between suicidal and psychotic, but we all have our limits.

The need for a sane solution to this problem is, I think, what led to the development of blogging engines like [typo](http://fdv.github.com/typo/).

And, I think, the attempt to build a new, saner, databased-backed, comprehensive, blog-aware CMS system learned that a databased-backed, comprehensive, blog-aware CMS system is a whole bunch of [YAGNI](databased-backed, comprehensive, blog-aware CMS system) features rolled up in a big, painful bundle. 

Why not just generate your blog posts when you write them? Why not just use Javascript for whatever dynamic widgets you need? It's all HTML in the end, right?

Possibly, some of the impetus for this is the arguable feature of PHP that, unlike Ruby on Rails (at that time), PHP was dirt-cheap to deploy/host, whereas RoR required either a VPS or a pricey Engine Yard instance. This was, after all, before the days of free-ish [Heroku](http://heroku.com) instances for low-traffic apps. And, even then, what if your blog became insanely popular? It could get pricey pretty quickly, whereas you could have a medium-traffic WordPress blog on some PHP host for, what, US$3.00 a month? 

So economics and technology collide. We find ourselves searching for a simpler solution, using better tools and easier hosting. For static sites, you can have free hosting on GitHub Pages just by pushing a site to the your-username.github.com repo under your GitHub account. For that matter, you can host a static site (virtually) for free damn near anywhere you like.

So *why* were we spending all this time and effort building out complicated content management systems, just to spend unnecessary time and money on a blog?

Static site generators are the answer. Spend your coding time actually coding for web *applications,* not for (mostly) static content. Sure, the learning curve is higher to use Octopress vs. WordPress. But I think I've [addressed this issue](/blog/2012/06/06/hackers-need-our-own-everything/). 

Before you build another CMS, or decide to use WordPress because it's the "obvious choice," ask your self this: What are the features I *actually* need? Can these be met by `%w{Jekyll Octopress Middleman Gumdrop other-static-generator}`? Then do what makes sense. Needlessly complicating your online life is not a virtue.