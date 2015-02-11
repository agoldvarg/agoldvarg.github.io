---
layout: post
title: "All right stop. Enumerate and listen..."
date: 2015-02-10 20:48:31 -0500
comments: true
categories: [code, how-to, guide]
---

...Ruby's back with a brand new iteration.

<iframe src="//giphy.com/embed/ufXEskx0lCtxK?html5=true" width="480" height="270" frameBorder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>

You heard right, the [Enumerable](http://ruby-doc.org/core-2.2.0/Enumerable.html) mixin is all about **iteration**, **manipulation** (and a heavy helping of **consternation**).

Learning how to use Enumerable methods to manipulate data and objects has been one the most exciting revelations since starting to use Ruby. But to truly understand Enumerable, it helps to drill-down into what the methods are actually doing with the data inputs, how they yield in and out of passed blocks, and finally what kind of results they return.

Collect
----------

Within Enumerable, there are several methods that can be used to search through, or filter over a collection of elements. Let's look at `collect`.  The collect method returns a new array after it yields each element in the original collection into the passed block. Let's look at a simple example:

``` ruby
avi_says = ["Cool", "So yea", "Come on"]

excited_avi_says = avi_says.collect { |phrase| phrase + "!" }

#=> ["Cool!", "So yea!", "Come on!"]
```

So, what happened there? Well, we started with an array  called `avi_says`. We called the `.collect` method on the array which then passed each element into our block. The code in this block simply adds some much needed punctuation to each passed phrase (which all happen to be strings).  But what's *really* happening? Like I mentioned, we can build our very own version of the `collect` method.

``` ruby
def masochist_collect(array)
  result_array = []  # For locally storing our modified elements
  for iteration in 0...array.length # Looping 1 time less than our array size
    result_array << (yield array[iteration]) # Yielding each element to the block and saving the return
  end
result_array # Returning our modified array
end
```

When we use this sick and twisted collect method and pass it the exact same block, we get the same result that we achieved using the built in `collect` method!
```ruby
avi_says = ["Cool", "So yea", "Come on"]
masochist_collect(avi_says) { |phrase| phrase + "!" }

#=> ["Cool!", "So yea!", "Come on!"]
```
How cool is that?! Let's look at another method within the Enumerable class.

Include
-----------

The `include?` method takes a collection as input and iterates through each element comparing them with the passed argument. If any member of the collection matches the passed argument object, the method returns True, otherwise it returns false. The "?" on the end of the method indicates that true or false will be returned. Oh Ruby, you speak to me.

Let's review the standard behavior and then try to replicate it:

``` ruby
array = [103, "Albatros", :unitards, "Party", 28]

array.include?("Party")
#=> true

array.include?(50)
#=> false
```

Let's try to break this down (I'm taking a small liberty here, by passing in two distinct parameters):

``` ruby
def masochist_include?(array, object)
  result = false # Setting default result to false, unless we find what we're looking for
  for iteration in 0...array.size # Looping 1 time less than our array size
    if array[iteration] == object # Checking for object matches
      result = true # Setting our result if object is matched
    end
  end
  result # Returning the result
end
```

And when we call our method:

``` ruby
array = [103, "Albatros", :unitards, "Party", 28]

masochist_include?(array, :unitards)
#=> true

masochist_include?(array, "Loud Noises!")
#=> false
```

What a world! So by breaking down a couple of Ruby's built in Enumerable methods we get a better understanding of what's really going on under the hood.

<iframe src="//giphy.com/embed/u3zdWCHYqBRio?html5=true" width="480" height="478" frameBorder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>



