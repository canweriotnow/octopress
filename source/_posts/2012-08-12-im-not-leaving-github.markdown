---
layout: post
title: "I'm not leaving Github yet, but..."
date: 2012-08-12 02:09
comments: true
categories: [github, open source, coding, git]
---

So [this blog post](http://bytbox.net/blog/2012/08/leaving-github.html) started making the rounds, and (at least in my little corner of the interwebs) has been quite a hot topic. 

You should go read it now, if you haven't already, but if I had to give the tl;dr version: Github's a great piece of software, but both its tooling and culture have made it something both other than, yet dependent on, Git. This is a Bad Thing, detrimental to Git, and to the open source community in general.

I can't say I disagree with any of the issues raised in the post. My personal conclusion is a bit different, but I can't fault the choice to leave, either. But I'd like to address why I agree that Github isn't a universal good, as well as why I'm not jumping ship right this moment.

### Hegemony

Just because it's one of those words ex-philosophy majors bandy about, I made this reference in one Twitter thread just a few minutes ago:

<blockquote class="twitter-tweet tw-align-center" data-in-reply-to="234526337556168704"><p><a href="https://twitter.com/steveklabnik"><s>@</s><b>steveklabnik</b></a> Github hegemony "forcing" new people to use git = pro. Everything's been downhill since the mac gui. Especially the culture.</p>&mdash; jason lewis (@canweriotnow) <a href="https://twitter.com/canweriotnow/status/234530318751784961" data-datetime="2012-08-12T06:02:40+00:00">August 12, 2012</a></blockquote>
<script src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

And [hegemony](http://en.wikipedia.org/wiki/Hegemony) is really quite an apt term for the thrall Github tends to hold over most of the Git ecosystem nowadays. At one point, I thought this was a really, really, good thing, even including the increasing tendency of some hackers to be prickly toward contributing to any project not hosted on Github. 

At that point, it wasn't completely sure whether Git or Mercurial would come out ahead in DVCS natural selection (please don't mention Bazaar). Since Git is _so_ much nicer to use, and _so_ technically superior, I was rooting for any competitive edge it could get to promote adoption. Yeah, people still use svn, I know. People also still use FORTRAN. It happens. But, I digress...

So, yeah. The fact that Github's ascendancy was helping Git to crush Hg, and at the same time, to get people to finally ditch Subversion, made me love them all the more, even beyond the free hosting for open source projects, the easy code browsing, and the features they kept adding all the time, making Github a really, really, nice web interface for Git.

Until it stopped being one.

### Change We Don't Need

See, when I referred to hegemony back there, that's wasn't as accurate as I first thought. If you look at what hegemony really means (this might require reading Gramsci, Adorno, or Althusser, sorry), you see that I really just meant popularity/ascendancy. Github didn't achieve hegemony until it started overtaking its host.

Github started as a really great way to do three or so things:

1. Host projects (git repos)
2. Communicate about them
3. Coordinate development (sort of)

So, there wasn't a whole lot of coordination until Github Issues was added, but that was a pretty ealry-stage feature, so we'll leave that in there.

Project hosting is sort of a core thing, as is the communication stuff, although that's gone through several iterations as well.

The real genius of Github, though, was the idea of *social* coding. That shiny "Fork" button, that throbbing "Hardcore Forking Action" animation... really, just some chrome on a `git clone` action, but it was *cool.* Almost sexy, even.

And then we wanted everything to be that slick and clicky. Sclicky.

Or, someone decided we should want that. And the default response to a feature request in the open source world went from "Where's your patch?" to "Where's your pull request?"



