---
layout: post
title: "Hackers Need Our Own Everything"
date: 2012-06-06 11:29
comments: true
categories: [apps, internet, hackers, trends, software]
---

When I conceived of this post, it was going to be about how damn awesome [Octopress](http://octopress.org) is. And it certainly is awesome; it powers this blog, and makes writing it a joy, whereas trying to use [Wordpress](http://wordpress.com), [Blogger](http://blogger.com), or even newer alternatives like [Tumblr](http://tumblr.com) or [Posterous](http://postero.us) was downright painful. But what I'm more interested in is the growing trend among apps, services, and even operating systems that has made projects like Octopress necessary.

### The Tragedy of Google

For such a long time, Google did search better than many of us ever dreamt _possible_ in the pre-Google days. But it wasn't just the intelligence of the search algorithms, or the massive cache and index behind Google search. Google made it possible to craft a finely-honed query from the front page, with excellent support for literal strings, boolean operators, required inclusion/exclusion, etc. And then came Google+.

Google's commitment to search had been on the decline for a while, it seems... the only new features search had acquired in years were fairly useless things like page previews and, briefly, Twitter integration. Because that's integral to search.

But when Google launched its abortion of a social network, usable search had to go. Not only did they kill one of the [most useful search operators](http://productforums.google.com/forum/#!topic/websearch/3oIWbew9xdE) (Boolean +), but they also started filtering search results based on social connections in Google+. While this doesn't _always_ end in having to re-search without "personal" results, I have a feeling that's only because I'm connected to so many developers on Google+. But if Google+ hadn't been such an abject failure, my mom might be on there, and we typically search about very different kinds of "cookies."  The situation with Google is so bad at this point, that I often get better results from [Duck Duck Go](http://duckduckgo.com/), which is sad, because it wraps the Bing search API. Seriously, Bing is giving me better results? If Google still had a free search API, it might not be so bad. But now we're stuck with a wrapper on Bing, and when Microsoft decides not to provide a free API for search, we're bascially screwed.

<!--more-->

### Blogging for Hackers

So, let's face it: unless you wanted to host your own blog, and either write your own engine, or tweak one into submission, keeping an attractive, maintainable, and useful blog was either an expensive or losing proposition. Sadly, this isn't a recent change like the other phenomena addressed in this post, but it's still an issue.

What's slightly alarming is the trend away from traditional blogging engines like Wordpress and Blogger, which, while not exactly hacker-friendly, were oriented toward content creation. The newer generation of blogging services are much more oriented toward the re-posting of content. While I'm okay in principle with re-posting (and I think "remix culture" is awesome), when your priority is saturation with "viral content" rather than the creation of OC, it makes it easy to ignore the creation of tools which lend themselves to the creation of content.

Octopress is awesome because it doesn't try to be everything to everybody. Billed as "A blogging framework for hackers," Octopress is basically a set of `rake` tasks and plugins for [Liquid](https://github.com/Shopify/liquid) and [Compass](http://compass-style.org/), all wrapped up with the tasty goodness of [Jekyll](https://github.com/mojombo/jekyll), the static site generator that powers [Github Pages](http://pages.github.com).

In a nutshell, this means I can use my favorite text editor (lately, either [Vim](http://www.vim.org/) or [Sublime Text 2](http://www.sublimetext.com/2), depending on my mood) to create my posts in Markdown, Textile, or Haml, and have Octopress generate pretty-styled HTML, CSS and JS, and deploy my blog to Github Pages (or Heroku) with a rake task. Even for non-programming power users, or anyone frustrated with Wordpress, really, Octopress is worth checking out. 

### Apple to Developers: "Go Fuck Yourselves"

Okay, slight hyperbole. But it feels that way sometimes. I've been using [TextMate](http://macromates.com/) on OS X for Ruby (and Perl, and C, and Clojure, you get the picture...) for such a long time now, that I'm _really_ loathe to change my workflow. Even though, conceptually, I prefer the idea of using Linux on all the things. But since Apple is now _blatantly_ [trying to turn my worsktation into a tablet](http://www.apple.com/macosx/mountain-lion/features.html), I'm forcing myself to use the [Lubuntu](http://lubuntu.org/) box sitting next to my iMac as much as possible. 

{% img float-right /images/post-img/mtlion1.png 400 %}

It's not just the "aesthetic" changes that chafe. I can deal with [annoying UI crap](http://unity.ubuntu.com/), especially when it's optional. But Apple is also changing the developer ecosystem, first with the Mac App Store, then with Gatekeeper, which will disallow installation of software not signed with an Apple developer account by default.

The whole allure of OS X was that it was a stable, supported, POSIX-compliant operating system that was enjoyable to use but afforded the user all of the power and flexibility of Unix. It looks liek those days are over, and the days of creating powerful tools for developers and designers to create whatever they could imagine are over. The Mac is turning into an overpowered tablet, suited for content consumption rather than creation.

Apple is not alone in its efforts to neuter the desktop. Not to be outdone in locking down the OS and polluting the developer ecosystem, Microsoft is scrambling to release Windows 8 so that Windows users can be as disoriented as possbile. Although there are [good](http://mobileopportunity.blogspot.com/2012/05/fear-and-loathing-and-windows-8.html) [arguments](http://pcunix.hubpages.com/hub/Why-Windows-8-might-Kill-Microsoft) that Windows 8 holds the threat of finally toppling the waning Microsoft hegemony, I'm actually jealous of Windows 8 in one way: Windows 8 includes an almost-workalike Windows 7 compatibility mode. I _wish_ Lion had a "act like Snow Leopard" mode. Although one of the articles I just cited laments the loss of the Start menu in Win7 mode, I don't think it's that much of a loss, if PowerShell is still included (or better yet, Cygwin). 

{% img float-left /images/post-img/win8-1.jpg 400 %}

I use Windows as little as possible, so I'm less annoyed about Windows 8 than I am Lion. But the trend is disturbing, and is even being echoed to a degree (a greatly diminished degree) in [GNOME 3](http://www.gnome.org/gnome-3/) and [Ubuntu Unity](http://unity.ubuntu.com/). But on Linux, at least, I have the option of using whatever window manager and desktop environment works best for me (or none at all). 

I realize that commercial operating system vendors need to target the widest possible user base. But the much-ballyhooed rise of the [developer-centric economy](http://www.forbes.com/sites/venkateshrao/2011/12/05/the-rise-of-developeronomics/) would _seem_ to suggest that pissing off developers is a _bad_ idea. Apple and Microsoft spent the better part of the 1980's and 1990's competing not only for market-share, but for developer mind-share. The movement toward locking us into proprietary toolchains and ecosystems (XCode for Apple, VisualStudio for Microsoft) looks like little more than a cynical attempt to chain down developers in a walled garden. Hopefully, we don't fall for it.

### For Us, By Us

It's been [The Year Of Linux On The Desktop](http://en.wikipedia.org/wiki/Desktop_Linux#Year_of_Desktop_Linux) since at _least_ 2000. I'm not going to be the next one to make grand proclamations (other than "total world domination _soon_"). But for me... right now, my primary development machines are a 27" iMac running Snow Leopard, and a 15" MacBook Pro, also running Snow Leopard. I won't be upgrading to Lion, and I'll miss the pretty Apple hardware. But when these are ready for replacement... let's just say I really hope [Project Sputnik](http://www.theverge.com/2012/5/7/3006266/dell-project-sputnik-ubuntu-xps-13-developers) is a huge success for Dell.

Although it's commercial software, targeted toward business users (and consumers) that pays the bills for most of us, I think it's important to remember that the people who make those tools are an important audience, too. I want to see more software of all kinds (web, desktop, and CLI) created by developers, for developers. Preferably open-source tools we can tweak and extend and continue to make better. I think that's my goal for this year, anyhow. I'm going to focus my efforts on projects that make it more fun to be a hacker, whether that's something like making blogging easier, creating build tools, or Linux desktop enhancements that are friendly to those of us who spend most of the day switching between an editor, a shell, and a web browser. I hope others have the same itch, and see the same need, and push back against the disturbing trend of hostility toward open systems and (by extension) the developers who use them.