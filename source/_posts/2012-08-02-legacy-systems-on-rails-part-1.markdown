---
layout: post
title: "Legacy Systems on Rails (Part 1)"
date: 2012-08-02 14:48
comments: true
categories: [ruby, rails, legacy systems, databases]
---

Much of my job consists of providing customized or novel interfaces for a complex legacy system which, although still maintained by the vendor (who shall remain nameless), does not currently (nor do I ever expect it to) meet many of our institutional needs. 

Since I spend a lot of time on this, I figured it would be a good topic for a series of posts, hence the "Part 1" in the title. Hopefully I'll actually follow through on it.

The first thing I did was to replace a few aging Perl CGI scripts with a Rails app, which was interesting. The notion that Rails is far easier to use for greenfield projects than for legacy systems is probably accurate, but it's not universally true.

This back-end is an Oracle database with over 450 tables and a hodgepodge of different strategies for how relationships should be modeled. I'm pretty sure it was my second or third day on the job that I was asked to implement a feature (in the old Perl codebase) that should have been straightforward given the relationships between two particular entities, but ended up requiring six inner joins and two left outer joins, IIRC. Just to give you an idea of what I'm dealing with.

Anyhow, the first time around, I wrote an ActiveRecord model for each table, did my `has_many`'s and `belongs_to`'s, et cetera. Some were easier than others. There were a _lot_ of conditions hashes in some of those associations.

When the project scope started to grow beyond a single web app, and I started designing a REST API for the system, I had the opportunity to scratch some of the itches that had been bugging me about the original implementation from the very beginning.

<!--more-->

### When Good Patterns Go Bad

The first thing I needed to do was to solve an issue with the EAV tables. EAV (Entity-Attribute-Value) is an okay model for sparse data. Somehow, the designers of this system decided to use it for custom fields where **every** entity has **every** attribute. When a custom field is added, a row is inserted in the definition table for the attribute. Then a row is inserted in the value table for **every single customer.** It's slow, to say the least. In the original (naive) implementation, this meant every time a new attribute definition was added, I added an association to the Customer class. And there are a *lot* of attributes.

I wan't about to make that mistake again.

### Metaprogramming to the rescue

First I started with the definition table:

{% codeblock FieldDef lang:ruby %}
class FieldDef < ActiveRecord::Base
  set_table_name 'custom_field_def'
  set_primary_key :custom_field_def_id

  has_many :field_values

  def symbol
    self.title.parameterize('_').to_sym
  end
end
{% endcodeblock %}

Pretty straightforward. The only extra thing is that `symbol` method, which returns a snake cased version of the 'title' attribute, suitable for using as a method name.

Next comes the field value table:

{% codeblock FieldValue lang:ruby %}
class FieldValue < ActiveRecord::Base
  set_table_name 'custom_field_value'
  set_primary_keys :cust_id, :custom_field_def_id

  belongs_to :customer, :foreign_kay => :cust_id
  belongs_to :field_def, :foreign_key => :custom_field_def_id
end
{% endcodeblock %}

Nothing out of the ordinary here (although I'd like to thank Dr. Nic and Charlie Savage for their work on [composite_primary_keys](https://github.com/drnic/composite_primary_keys), it's a lifesaver).

Of course, the goal here is eliminating the 40-odd lines of has_many and accepts_nested_attributes_for in the Customer class. This is where Ruby really shines:

{% codeblock Customer lang:ruby %}
class Customer < ActiveRecord::Base
  set_table_name 'customer'
  set_primary_key :cust_id

  # Here's where we dynamically generate associations at runtime

  FieldDef.find_each do |field|
    has_one field.symbol, :class_name => 'FieldValue', 
                          :foreign_key => :cust_id,
                          :conditions => proc {"customer_def_field_def_id = #{field.id}"}

    accepts_nested_attributes_for field.symbol
    delegate :field_value,  :to => field.symbol, :prefix => true
    delegate :field_value=, :to => field.symbol, :prefix => true

  end

  # snip

end
{% endcodeblock %}

This iterates over the rows of `custom_field_def`, generates an association for each entry, adds the `accepts_nested_attributes_for` declaration, and even delegates the getter and setters for the column we're really interested in (`"CUSTOM_FIELD_VALUE"."FIELD_VALUE"`).

I don't claim it's _the_ most elegant solution, but it's a lot better than in the previous iteration. It's important to remember that although Rails' opinionated nature makes it a little more awkward to deal with a legacy sytem than with a brand new project, Ruby gives you all the tools you could want to overcome whatever hurdles you might encounter.

 If you have any questions or suggestions for improvement, please let me know in the comments!