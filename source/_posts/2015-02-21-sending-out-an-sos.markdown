---
layout: post
title: "An introduction to Ruby's .send method"
date: 2015-02-21 12:32:30 -0500
comments: true
categories: [code, how-to, flatiron, ruby, guide]
---

.send
-----

Beards, you love them. Why? I'm going to tell you. But first, let's talk about Ruby's `.send` method. Let's look at a few simple examples:

``` ruby
def square
  self ** 2
end
9.send(:square)
"Profound String".send(:reverse) 
#=> 81
#=> "gnirtS dnuoforP"

2.send '+', 5
#=> 7
# 2 is the message recipient, + is the sender, or method, 
# and 5 is the argument. Equivalent to 2 + 7.

a = "upcase"
a.send(a)
#=> "UPCASE"
# Whooaaaaaa, metaaaaa
```

At first glance, send might not really seem that useful but it can come in handy when abstracting - one of our favorite things to do!  Let's say that we have a class named `Beard` that we want to instantiate and assign attributes to:

``` ruby
class Beard
  attr_accessor :name, :style
end

alex = {
  :name => "Alex's Beard",
  :style => "Wispy Wiggins"
}

Beard.new.tap do |b|
  b.name = alex[:name]
  b.style = alex[:style]
end

#=> #<Beard:0x007fca52f567d8 @name="Alex's Beard", @style="Wispy Wiggins">
```

So, the code above works by literally calling each attribute and assigning them individually. Literals present great opportunities for abstraction:

``` ruby
class Beard
  def assign_values(hash)
    hash.each_key do |attribute|
      self.send( "#{attribute}=" , hash[attribute] )
    end
  end
end

# In english...
# Take each key/or attribute (e.g. name, style)
# Interpolate the attribute to construct a method (e.g. `name=`)
# Assign the values (e.g. "Alex's Beard")
# All together:
#   alex[:name] = "Alex's Beard"
#   alex[:style] = "Wispy Wiggins"

Beard.new.tap { |a| a.assign_values(alex) }

#=> #<Beard:0x007f8af318a170 @name="Alex's Beard", @style="Wispy Wiggins">
```

Let's review what's going on right there. The assign_values method passes each key from the attribute hash to self. In this context, self represents an instance of the Beard class. More specifically, this particular each method builds setter methods by interpolating the attribute and appending "=" to the end. The actual value from `hash[attribute]` is passed in as an argument. Blargh, word soup! What does is all mean? It means one less piece of code to maintain given an expanding or changing set of attributes belonging to the class. Nice!

Ruby is kind.

Closing Thoughts
----------------
<iframe src="//giphy.com/embed/12eFpo8m9htKfu?html5=true" width="480" height="291" frameBorder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>










