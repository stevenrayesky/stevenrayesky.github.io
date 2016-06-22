---
layout: post
title: Memoization 
---

Recently the concept of memoization came up, and somehow this concept had slipped by me while I was at NYCDA and crawling the web. So I took some time to get familiar with it. Let's start with the strict definition.

[Dictionary.com](http://www.dictionary.com/browse/memo-function) provided this definition (interestingly, it looks like "memoization" is not included in dictionaries yet):


> Memoization (Or "memoised function") A function that 
> remembers which arguments it has been called with and
> the result returned and, if called with the same 
> arguments again, returns the result from its memory 
> rather than recalculating it.

So memoization helps to eliminate making calls or computation of values that have already been called by storing them. This can be accomplished by creating a condition at the beginning of a call that asks "Hey, do I know this value already?" 

A simple example would be

```
def whats_my_name
 @my_name ||= set_name("Steven Rayesky")
end

def set_name(n)
puts "Setting name!"
 @my_name = n
end

whats_my_name
# => "Setting name!"
# => "Steven Rayesky"
whats_my_name
# => "Steven Rayesky"
```

The first function is checking to see if the variable `@my_name` exists. If it does, it simply returns that. If not, it calls the `set_name` function.

A simple example, but when used properly it can cut down on making multiple calls to a database or running the same function multiple times.

Gavin Miller gave a [great example](http://gavinmiller.io/2013/basics-of-ruby-memoization/) with the often used `current_user`.

Justin Weiss also has a good [blog post](http://www.justinweiss.com/articles/4-simple-memoization-patterns-in-ruby-and-one-gem/) with good examples as well.

This [article](http://www.rubyinside.com/what-rubys-double-pipe-or-equals-really-does-5488.html) by Peter Cooper is also interesting. He explains the commonly used operator `||=` for memoization.
