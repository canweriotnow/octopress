---
layout: post
title: "job_interview"
date: 2012-05-09 13:14
comments: true
categories: 
---

So, I just wanted to plug a cute little project that [Micah Gates](https://twitter.com/#!/micahjgates) and I hacked together at [BohConf](http://railsconf.austinonrails.org/bohconf), the awesome un-conference and hackfest that runs parallel to [Railsconf](http://railsconf2012.com) each year.

It's called [job_interview](https://github.com/ruby-jokes/job_interview), and it's a Ruby gem to automate some of the tedium of programmer job interviews.

As an example, let's take [FizzBuzz](http://www.codinghorror.com/blog/2007/02/why-cant-programmers-program.html), a typical interview screening question intended to weed out the applicants who can't write code to save their lives. In Ruby, you might implement FizzBuzz like this:

``` ruby FizzBuzz https://github.com/ruby-jokes/job\_interview/blob/master/lib/job\_interview/fizz\_buzz.rb

def fizz_buzz(max)
  Array.new(max) do |i|
    j = i + 1
    val  = (j % 3 == 0 ? "Fizz" : "") +
    (j % 5 == 0 ? "Buzz" : "")
    val.empty? ?  j.to_s  : val
  end
end

```

But that's just tedious. With job\_interview, it's dead simple:

``` ruby job_interview FizzBuzz

require 'job_interview'
@answer = JobInterview::Answer.new
@answer.fizz_buzz(5)

 => [1, 2, "Fizz", 4, "Buzz"]

```

It also does Fibonacci sequences (recursive, iterative, and matrix strategies), a quine, the first _n_ primes, and, of course, "Hello, World!"

That wasn't enough, though.

It will also answer the bullshit personal questions that everyone lies about anyway!

``` ruby

include JobInterview::Questions

```

Q. Where do you see yourself in 5 years?

``` ruby

in_5_years

 => "I'd like to have made someone else rich with my re-contextualized non-volatile open architecture."

```

Q. Why do you want to work here?

``` ruby

why_here

 => "Your company has revolutionized seamless next generation interface."

```

Q. Does P = NP?

``` ruby

p_equals_np

 => "I doubt it, but it would make life easier for traveling salesmen."

```

...and many more.

We aim for 100% test coverage with RSpec, so we're confident that this is a robust solution for a range of job interview scenarios.

We did a lightning talk at RailsConf 2012, and you can [see the slides here](http://ruby-jokes.github.com/job_interview/pres.html).

Next time you face an interview for a programming job, work smarter, not harder. 

`gem install job_interview`
