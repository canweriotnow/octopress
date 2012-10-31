---
layout: post
title: "Feedback Loops"
date: 2012-10-31 14:12
comments: true
categories: [coding, blogging, psychology]
---

Sadly, I haven't added a blog post in roughly 2.5 months. I've had ideas for posts, but when it came time to set pen to page (or fingers to keyboard, as teh case may be) I just haven't had it in me. I really enjoy writing this blog, too. I wasn't quite sure what was going on, until I read one of the most insightful blog posts I've ever seen: [Be Nice To Programmers](http://edu.mkrecny.com/thoughts/be-nice-to-programmers).

The tl;dr is a dialogue between a programmer and a guy who wishes he had the chops because he thinks coding is the neatest job in the world. The programmer tells him he thinks coding is making him miserable because the the development/debug process is the ultimate negative feedback loop. 

{% blockquote [http://edu.mkrecny.com/thoughts/be-nice-to-programmers] %}
 My workflow is something like this.

write some code
run the code
get an error message
find the error and back to step 1
Hour by hour, day after day, I do this. Always searching for what's wrong with what I'm creating, rarely thinking about what's good about it. It's a negative reinforcement feedback loop.
{% endblockquote %}

{% pullquote %}
I definitely get the sentiment. But I think of this as the inner loop in the red-green-refactor cycle, so to speak. Yeah, coding (_especially_ doing proper TDD) is going to make you hate the world (and possibly feel like an idiot) sometimes. But overall... I was in a job interview a few weeks ago, and was asked why I love being a programmer. I didn't even have to think about my response: {" The main reason to become a programmer is that the position of 'God' is unavailable. Your _job_ is to create universes where the fundamental laws of nature, so to speak, are completely under your creative control. "} Ultimately, that's the takeaway: programming is _awesome._ But a job is still a job, and I think that's where some of the negative feedback loop comes in.
{% endpullquote %}

My last post was just before a huge project I'd both originated and put a large amount of my time and effort into over the course of 15-18 months was shelved. It was ready to ship, but corporate politics being what it is (i.e., something I'd schedule a root canal to avoid, _especially_ where I work), I tried to just move on and not lose sleep over it. Still, it rankled.

<!-- more -->

I haven't pushed a single new commit to any of my projects on Github. I haven't written a blog post. I have an engineering pad with a bunch of scribbled, inchoate notes for things I want to do, but can't seem to move on anything. 

My own theory is that we (hackers) are especially sensitive to feedback loops. I could go [on and on](http://decomplecting.org/blog/2012/05/22/passion/), and even cite [more](http://www.codinghorror.com/blog/2006/07/separating-programming-sheep-from-non-programming-goats.html) [notable](http://www.bricklin.com/wontprogram.htm) [bloggers](http://www.codinghorror.com/blog/2010/02/the-nonprogramming-programmer.html) than myself, on my theory of what could be referred to as "programmer exceptionalism." That's not to say we (programmers who can actually build working (and hopefully, elegant) systems) are in any way _better_ than non-programmers (or the [Java Schools](http://www.joelonsoftware.com/articles/ThePerilsofJavaSchools.html) crowd); it's just that the preponderance of anecdotal evidence (not to mention some [proper research](http://www.eis.mdx.ac.uk/research/PhDArea/saeed/paper1.pdf)) suggests that _programmers are not normal._ 

"Sensitivity to feedback loops" could also be a symptom of the intuition many of us experience when faced with an implementation that just _feels_ wrong. We can, through due diligence, prove that this is the case eventually; but what is it that drives us to find exploits, or benchmark competing implementations? It's that little voice in the back of your head whispering, "This is wrong. And also, stupid."

My main focus in my day-to-day programming life right now is dealing with interfaces for yet another vendor product that is very wrong, and very, very stupid. So when I come home, I just want to play [Guild Wars 2](http://guildwars2.com) and not really think about coding. Which makes me even sadder, because I love hacking on side projects. 

And it's not that I haven't had some fun and some successes in the meantime. I wrote a pretty cool framework in Clojure for generating and emailing reports from various datasources. The core of it is going to be open source, as soon as I get around to that. But the grind... the grind, man. The grind.

I don't know what the solution is. We can't all be working on innovative, game-changing products all the time. And sometimes things will get shelved the day you expect them to ship. I do know there needs to be a way to _love_ this shit without going crazy or making oneself miserable. 

So, interwebs... suggestions? 