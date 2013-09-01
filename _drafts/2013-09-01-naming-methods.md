---
layout: post
title: "Naming methods"
description: ""
category:
tags: []
---
{% include JB/setup %}

I actually used the following convention for a long time:

command method: verb
query method: noun
This of course breaks down in object oriented programming, where you already have a noun, so there I switched to using adjectives for methods on objects. I actually didn't realize that this isn't very ruby-ish, and have to consider that ;)

I don't really buy the sound-more-like-natural-language argument, because to me, this sounds more natural ('give me sentence, normalized). I think it's rather personal, and what you're used to. I do like how this really indicates what method modifies state in some way, and what method returns a result. And though I think ! could have indicated that as well, it doesn't. It indicates 'dangerous' operations, which could be a modification, and could be something else. And it is used rather inconsistently, for instance ActiveModel#save and Enumerable#keep_if doe have side_effects.

I'll try to be a bit more aware of ruby core classes to see whether this style conflicts with ruby or doesn't. Really liking this discussion :)



Hmm, I'm not sure whether it really is a pattern (just browsing around the core classes a bit, but at least numeric classes like Float don't seem to follow it), but you would suggest:

Command method: verb
Transformation method: verb
query method: noun
It sounds sane, though to me it's less obvious than what I proposed before. It is an interesting pattern I didn't notice before. (I think numeric classes might very well be an exception, since mathematical operations have names which are typically well established. On the other hand, I consider the same to be true for the functional methods on enumerator, which I wouldn't expect to follow the noun/verb logic, since I now them from functional languages)

Reply





----- from exercism:

This post will be about naming methods. First a dump of what I said on this before on exercism/parley:

I like to name methods which return something for what they return, and methods which do something for what they do. I also strongly believe you should seperate methods which are commands from methods which are queries. Therefore the normalized. If you would do something like @words = @words.downcase, I would call it normalize.

You're right, the command/query distinction isn't totally obvious here. I wouldn't call it a query though, because you cannot just set an expectation for it to be called in your tests. You need the result as well. So I do think it's more of a query. In the end, if you retrieve an object from the database, you put in an id, and get out a user. It's no different than putting in a string, and getting out a normalized string.
However, this is always difficult in ruby/coffeescript, because methods always return something, so there are no pure commands as such. But can you implement this method without a return on the end? I think not, so I would say it's a query.

