---
layout: post
title: "Keyword Arguments"
date: 2015-02-14 22:13:50 -0500
comments: true
categories: [code, how-to, flatiron, ruby, guide]
---

Keyword arguments were rolled out as part of the Ruby 2.0 release. And recently I've run into them as part of the 'Green Grocer' lab at [Flatiron](http://flatironschool.com/). I worked my way through the lab but I didn't fully grasp what was going on. So through this blog post I hope to solidify the concept.

Let's start with a simple method `manipulate_string` that expects to receive two arguments; a String followed by an Integer:

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

So, the `manipulate_string` method does exactly what its asked. But knowing that computers don't make assumptions we can't expect the ruby interpreter to decide which argument is which. 

In other words, this method as written lacks [robustness](https://en.wikipedia.org/wiki/Robustness_%28computer_science%29) in two obvious ways. It can only respond to the exact amount of arguments expected and it's arguments must be given in the exact order as defined in the method. 

We can code around the first weakness pretty easily by assigning defaults to an argument. For example:

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
But it's a bit more difficult to protect against the second issue where we attempt to pass arguments out of order...

``` ruby
def manipulate_string(string, volume)
  if string.is_a?(String)
    if volume > 6
      puts string.upcase
    else
      puts string.downcase
    end
  else
    new_string = volume
    new_volume = string
    if new_volume > 6
      puts new_string.upcase
    else
      puts new_string.downcase
    end
  end
end

manipulate_string(2, "bingo bango")
manipulate_string("bingo bango", 2)
#=> bingo bango
#=> bingo bango
```

Our method is getting ugly very quickly. And the prior fix didn't really address the issue completely. Maybe we could modify our method to accept a hash with default values:

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

The previous revision works a *little bit* better in that we can now accept arguments in any order. But what happens if we leave out one of the arguments:

``` ruby
manipulate_string(string: "Be Quiet")
#=> NoMethodError: undefined method `>' for nil:NilClass
```

You can see that we run into the number of required arguments issue again. This is fixable but our method is going to get more complex:

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

WAHOOO! We did it! Although something about the above revision just doesn't *feel* very Ruby-like. You might be thinking - "when is he going to get to the point?!" OK, here we go - by using **Keyword Arguments**, we can vastly improve the simplicity and readibility of our previous method without sacrificing any of the functionality. Let's take a look at our example:

``` ruby
def manipulate_string(string: "Nice to see you", volume: 7)
  if volume > 6
    puts string.upcase
  else
    puts string.downcase
  end
end
```

Notice the `key: value` structure as we define the arguments? We can call this new and improved method without worrying about missing and/or out-of-order arguments:

``` ruby
manipulate_string(volume: 4, string: "Be Quiet")
manipulate_string(string: "Good Times")
manipulate_string(volume: 3)
#=> be quiet
#=> GOOD TIMES
#=> nice to see you
```

Wonderful! So Ruby can posit that you're passing in hash pairs for these arguments. It also knows that you want to have defaults, and it doesn't care what order you pass each argument into the method. Now that's what I call robust!

Closing Thoughts
----------------

To sum it up, keyword arguments allow you to create dynamic methods able to accept arguments in a multitude of ways. I'll be keeping this tool handy when coding methods going forward. Thanks for reading and keep coding!

**Resources**

* Cooper Press - [6 Minute Guide to Keyword Arguments in Ruby 2.0](https://www.youtube.com/watch?v=u8Q6Of_mScI)
* Seiji Naganuma - [Keyword Arguments in Ruby](http://www.seijinaganuma.com/2015/02/keyword-arguments-in-ruby/)
