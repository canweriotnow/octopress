---
layout: post
title: "PAM Authentication Beyond The Desktop"
date: 2013-03-08 20:11
comments: true
categories: [Ruby, PAM, Linux, authentication, Clojure]
---

The Linux [PAM](http://www.linux-pam.org/) (Pluggable Authentication Modules) architecture is one of the most wonderful (and most overlooked) features of the OS. Typically we only consider PAM as handling our console (or xdm/gdm etc. logins) on Linux, but it's useful for so much more.

### Web Authentication

At work, we needed an authentication solution that allowed users to sign in with their ActiveDirectory credentials. Although the "official" solution was to use [SiteMinder](http://www.ca.com/us/secure-single-sign-on.aspx) for web authentication against AD, we were working on a mobile application, and at the time the SiteMinder auth page was ugly, and had no mobile-optimized login page. The latter problem has since been rectified; now it has both an ugly desktop login and an ugly mobile login. In addition, we were using nginx, and SiteMinder was really only supported under IIS and Apache (and at the time, the latter was via Shibboleth. Ugh.), so without official SiteMinder support, or an nginx Shib plug-in, we were in a bit of a bind.

Around the same time, I was playing with Likewise Open (now known as [PowerBroker Identity Services - Open Edition](http://www.powerbrokeropen.org/)) to bind my Linux workstation into AD. So it occurred to me: if a normal Linux PAM login can be authenticated against ActiveDirectory, why not a PAM login from a web application?

I know, I know, my first though should have been LDAP, right? For some unknown reason, LDAP was verboten at the time. The policy has since (apparently) been reversed, but such is the ebb and flow of corporate politics. And so, in the grand tradition of one of the mothers of modern computer science (and one of my daughter's namesakes):

{% blockquote Rear Admiral Dr. Grace Murray Hopper %}
 If it's a good idea, go ahead and do it. It is much easier to apologize than it is to get permission.
{% endblockquote %}

<!--more-->

My first obstacle was to figure out how to do this from Ruby. [Authlogic](https://github.com/binarylogic/authlogic) is a decent authentication framework (Sure, Devise is newer, but there's nothing wrong with Authlogic). There's an [authlogic_pam](https://github.com/jhu-idcs/authlogic_pam) plugin (link is to my updated version, original seems to be abandoned), so the main issue was updating the long-abandoned rpam gem to tie into PAM. So I created [rpam-ruby19](https://github.com/canweriotnow/rpam-ruby19) to have a C extension compatible with Ruby ~>1.9.2. Once the server (all of our production servers are [Debian 6 "Squeeze"](http://www.debian.org/releases/stable/)) was tied into AD, it was relatively trivial to create a login that used Authlogic to hit PAM (and thusly ActiveDirectory) for user authentication.

### But now everyone has a server login?

No, not at all. Likewise/PBIS has a setting to change the login shell for _only_ AD users; we simply changed their shell to `/bin/true`. Problem solved.

### And that forgiveness/permission thing?

While we were in beta, we informally ran the auth scheme by the people directly responsible for such things. They actually thought it was pretty cool and innovative. Which just reinforces my dedication to the timeless wisdom of Dr. Hopper.

### And so...

Since we implemented this auth scheme for our mobile app, we've continued to go with it; it's simple, elegant, and shields us from capturing (even hashed) credentials. We have two(-ish) new products launching this year using the same auth scheme. And we're still quite satisfied with the results.

### Caveats

Over the past couple of months, I've been researching an [issue submitted on Github](https://github.com/canweriotnow/rpam-ruby19/issues/5) documenting a problem authenticating local users other than the euid running the process. You can get the details from the link, but this is how PAM (or at least shadow passwords) are supposed to work. This isn't for authenticating local system accounts (at least not if you're using shadow passwords properly); you should only auth external accounts (LDAP, ActiveDirectory, maybe NIS+) through PAM for non-system-login applications.

### Future

Since this has worked out so well with our Rails apps, I'm now working on a Clojure equivalent. There's a PAM integration library for Java called JPam, which I've started wrapping in a library called [clj-pam](https://clojars.org/clj-pam), available from Clojars. If you'd like to help, the source repo is located [here on Github](https://github.com/canweriotnow/clj-pam).

PAM is wonderfully extensible. It's also very configurable, and is worth leveraging whenever possible. Dig deeper. Linux has so many great little pieces we tend to overlook.