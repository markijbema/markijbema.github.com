---
layout: post
title: "Memoize all the things"
description: ""
category:
tags: []
---
{% include JB/setup %}

Today Henrik Nyh posted on his blog about [the dangers of memoization](http://thepugautomatic.com/2013/08/memoization-is-a-liability/). While I agree with the premise that there are dangers with memoization, I don't believe they are to blame on memoization. I added a comment, but I think my motivation for using memoization deserves a post of its own. But please read [Henrik's post](http://thepugautomatic.com/2013/08/memoization-is-a-liability/) first, as it makes an excellent point, and I think you should look at both sides of the issue.

## Why use memoization?

I will start out with a probably first version of the example Henrik used on his blog:

``` ruby
class Word
  def initialize(string)
    @string = string
  end

  def do_something
    letters = @string.chars

    10.times do |i|
      whatever(letters)
    end
  end
end
```

Since converting a string to characters probably has nothing to do with doing something, it is probably worthwhile to extract this to its own method. But now we run into a problem. Since the value of letters is used multiple times, we will calculate it multiple times if we don't memoize it:

``` ruby
  def do_something
    10.times do |i|
      whatever(letters)
    end
  end

  def letters
    @string.chars
  end
```

The alternative is to memoize it, and not calculate it multiple times:

``` ruby
  def letters
    @letters ||= @string.chars
  end
```

Either way we're going to break compatibility with the current implementation, so to me the sentiment of 'premature optimization', which was suggested in the comments doesn't hold.

## When use memoization?

I think you should only use memoization in immutable objects. Combining mutable objects with memoization opens up a world of pain. In my opinion, this is caused by the immutability though.

Lets look at what happens if you add a setter for string to our Word class? The memoized version of Word is broken: it will always return the result based on the first string. But the non-memoized version is broken as well: do_something suddenly isn't thread safe anymore.

To me, the latter feels more dangerous that former. Suddenly you have a program which only *sometimes* fail (in multiple ways), which your unit tests can (and probably will) miss, as opposed to a program which fails in a very predictable way.

## Is memoization dangerous?

I think in most cases memoization is perfectly safe. There are some pit-falls, and you should be aware of them

 * don't memoize values which can be falsey (as they won't memoize)
 * don't memoize in mutable classes (or be prepared to solve cache invalidation problems).
 * don't memoize methods with parameters (unless you're very sure you'll call it with the same parameters again)

But in most cases memoization solves more problems than it causes.

## Is mutability dangerous?

Yes
