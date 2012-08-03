---
layout: post
title: "Generational Impedance Mismatch"
date: 2012-08-03 15:48
comments: true
categories: [coding, customers, demographics]
---

One thing I've come to observe working in higher ed is that you can run into a lot of issues with what I want to term "generational impedance mismatch." It's what happens when your ostensible customers are about 40 years older than your target demographic.

When I started on an internal administrative application about two years ago, I threw in some error pages with lolcats on them because... well, error pages are boring. Those got yanked because the customer thought they were "unprofessional." Okay, sure. It's an administrative app, so maybe this isn't the best thing to throw up after a catastrophic failure:

{% img center /images/post-img/im-in-ur-serverz.jpeg %}

But the new crop of apps I'm writing don't target middle-aged administrators; they target students. Specifically, in addition to doing mundane things like reporting your a lost ID card or checking balances, there's a whole social gaming component. So far, I've been pretty successful at keeping things amusing (between the student focus group we assembled and the [JHU subreddit](http://reddit.com/r/jhu), my sense of humor is quickly vindicated), but the text is... kinda stodgy. 

I was discussing this with a co-worker, and we hit on what I think is a brilliant way of balancing conflicting stakeholder needs. The customer wants rather formal, business-like text that drily describes various functions of the application. On the other hand, students are going to be bored, and love easter eggs and humor. But we know how to deal with target demographics who speak different languages, don't we? Localization to the rescue!

<!--more-->

We can go from a default:

{% codeblock en.yml lang:yaml %}

en:
  hello: "Hi there!"

{% endcodeblock %}

to a specialized locale for old people:

{% codeblock en-old.yml lang:yaml %}

en-old:
  hello: "Why, good morrow, sir or madam."

{% endcodeblock %}

Since we track birthdates, it makes it really easy:

{% codeblock lang:ruby %}

class ApplicationController < ActionController::Base

  before_filter :localize_for_the_aged

  private

  def localize_for_the_aged
    I18n.default_locale = :en
    if current_user.try(:old?)
      I18n.locale = :"en-old"
    end
  end 
end

class User < ActiveRecord::Base

  def old?
    self.birthdate.nil? || self.birthdate < 40.years.ago
  end

end

{% endcodeblock %}

Simple! Now our middle-aged customer will see a formal greeting, while our teenage/twentysomething users won't think they've stumbled into Downton Abbey.

### Don't try this at work

Seriously, I hope you realize this was satire. Learn to talk to your customers, as painful as that might be, and convince them. Do A/B testing or have a focus group. Win over your users, and your customer will probably see the light of day. If not, you can always [whinge about it here](http://clientsfromhell.net).