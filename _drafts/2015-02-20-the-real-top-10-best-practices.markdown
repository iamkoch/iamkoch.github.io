---
layout: post
title:  "The real top 10 best C# practices"
date:   2015-02-20 19:42:43
categories: c# engineering development
comments: true
---

Having read [this post about the top 10 C# best practices](http://www.devbattles.com/en/sand/post-786-%5BC%5D+Top+10%2B+Best+Practices+for+Writing+Super+Readable+Code) today I felt compelled to write a response.

# Use Proper Naming Conventions

> Avoid adding prefixes or suffixes for your identifiers. Though in some guidelines, they use “m_” and in some other they use “_” as the prefix of variable declaration. I think it is not that much useful. But, it depends on your organizational coding practices. This point is contradictory based on various organizations and there is no strict guidance on it.

I agree with this one, though I loathe m_ or _ as a prefix as I don't feel it's necessary, especially with ReSharper's color code identifiers options. If you don't have this switched on, give it a go and once you have you'll never go back.

> Always use “I” as prefix for Interfaces. This is a common practice for declaring interfaces.

This is only a common practice in .Net, and many people in the industry whom I respect disagree with prefixing interfaces with an I. Consistency is key, though, and if you inheriting a codebase that doesn't prefix interfaces with an I then the pattern should be continued. Again, ReSharper's color identifiers will highlight interfaces a certain color, helping with clarity.

As a final point, I use I for my interfaces as it's the done thing in .Net