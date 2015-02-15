---
layout: post
title: "Keyword Arguments"
date: 2015-02-14 22:13:50 -0500
comments: true
categories: [code, how-to, flatiron, ruby, guide]
---

Keyword arguments were rolled out as part of the Ruby 2.0 release. And recently I've run into them as part of the 'Green Grocer' lab at flatiron. I was able to get the lab passing by deductive reasoning but I didn't fully grasp the concept. This blog post is my penance.

Let's start with a simple method `manipulate_string` that expects to receive two arguments; a String and then an Integer:

``` ruby
def manipulate_string(string, volume)
  if volume > 6
    puts string.upcase
  else
    puts string.downcase
  end
end

manipulate_string("let's jam", 8)
manipulate_string("bingo bango", 2)
# as expected:
#=> LET'S JAM
#=> bingo bango

# But, if we get a little bit wild:
manipulate_string("time to jam")
manipulate_string(2, "bingo bango")
#=> ArgumentError: wrong number of arguments (1 for 2)
#=> ArgumentError: comparison of String with 6 failed
```

So, the `manipulate_string` method does exactly what it's asked. But we know that computers don't like to make assumptions. And so we can't expect the ruby interpreter to make these kinds of decisions. 

This method, as written, lacks [robustness](https://en.wikipedia.org/wiki/Robustness_%28computer_science%29) in two obvious ways. For one, can only receive an exact amount of arguments. And two, arguments must also be given in the exact order. 

We can code around the first weakness pretty easily by assigning defaults to each argument:

``` ruby
def manipulate_string(string, volume=5)
  if volume > 6
    puts string.upcase
  else
    puts string.downcase
  end
end

manipulate_string("let's jam")
#=> let's jam
```
But it's a bit more difficult to protect against the second issue of passing arguments out of order...

``` ruby
def manipulate_string(string, volume)
  if string.is_a?(String)
    if volume > 6
      puts string.upcase
    else
      puts string.downcase
    end
  end
end

manipulate_string(2, "bingo bango")
manipulate_string("bingo bango", 2)
#=> bingo bango
#=> bingo bango
```

That got ugly very quickly. And this fix didn't really address the issue completely. Maybe, we could modify our method to accept a hash, with default values:

``` ruby
def manipulate_string(options = { string: "hello", volume: 5 })
  if options[:volume] > 6
    puts options[:string].upcase
  else
    puts options[:string].downcase
  end
end

manipulate_string(string: "Good Times", volume: 9)
manipulate_string(volume: 4, string: "Be Quiet")
#=> GOOD TIMES
#=> be quiet
```

The previous revision works a *bit* better. We can now accept arguments in any order. But what happens if we leave out one of the arguments:

``` ruby
manipulate_string(string: "Be Quiet")
#=> NoMethodError: undefined method `>' for nil:NilClass
```

You can see that we'll run into the same issue. We can fix this as well - but our method is going to get a bit more complicated:

``` ruby
def manipulate_string( options = {} )
  defaults = { string: "hello", volume: 5 }
  options = defaults.merge(options)

  if options[:volume] > 6
    puts options[:string].upcase
  else
    puts options[:string].downcase
  end
end

manipulate_string(string: "Good Times", volume: 9)
manipulate_string(volume: 4, string: "Be Quiet")
manipulate_string(string: "Be Quiet")
#=> GOOD TIMES
#=> be quiet
#=> be quiet
```

WAHOOO! We did it! Although something about the above method just doesn't *feel* very Ruby-like. You might be thinking - "when is he going to get to teh point?!" OK, here we go - by using **Keyword Arguments**, we can vastly improve the simplicity and readibility of our previous method without sacrificing any of the functionality. Let's take a look at an example:

``` ruby
def manipulate_string(string: "Nice to see you", volume: 7)
  if volume > 6
    puts string.upcase
  else
    puts string.downcase
  end
end
```

Notice the `key: value` structure as we define the arguments? We can call this new and improved method and pass missing and/or out-of-order arguments:

``` ruby
manipulate_string(volume: 4, string: "Be Quiet")
manipulate_string(string: "Good Times")
manipulate_string(volume: 3)
#=> be quiet
#=> GOOD TIMES
#=> nice to see you
```

Wonderful! Ruby can posit that you're passing in hash pairs for arguments. It also knows that you want to have defaults for those arguments, and it doesn't care what order you pass them into the method. That's what I call robust!

Closing thoughts
----------------

To sum it up, keyword arguments allow you to create dynamic methods that are able to accept arguments in a multitue of ways. I'll definitely keep this tool in my bag of tricks when coding methods going forward. Thanks for reading! Keep coding!

**Resources**

* Cooper Press - [6 Minute Guide to Keyword Arguments in Ruby 2.0](https://www.youtube.com/watch?v=u8Q6Of_mScI)
* Seiji Naganuma - [Keyword Arguments in Ruby](http://www.seijinaganuma.com/2015/02/keyword-arguments-in-ruby/)
