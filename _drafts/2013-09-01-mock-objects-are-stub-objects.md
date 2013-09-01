---
layout: post
title: "Mock objects are stub objects"
description: ""
category:
tags: []
---
{% include JB/setup %}

based on for instance: http://confreaks.com/videos/659-rubyconf2011-why-you-don-t-get-mock-objects

I think the whole mock objects aren't stub objects is confusing, at least in ruby. I think rspec solves this nicely with calling them all doubles now. The interesting thing is whether a method is an expectation or a stub, why not talk about method level instead of class/object level?
