---
layout: post
status: publish
published: true
title: Getting it right first time is not un-agile
author: Antony Koch
author_login: amkoch
author_email: ant@iamkoch.com
wordpress_id: 65
wordpress_url: http://localhost/~Ant/wordpress/?p=65
date: '2012-07-15 14:06:42 +0100'
date_gmt: '2012-07-15 14:06:42 +0100'
categories:
- Agile
tags: []
comments: []
---
While talking through some upcoming sprint candidates, I pushed a BA for more information because I wanted to 'get the code right first time'. The BA's response to this request was that he deemed it 'un-agile'.

I found that quite interesting and I wanted to talk about why coding things correctly first time has value and is agile, and that it's also not subject to the 'just enough' / 'just barely good enough' mantra that agile promotes.

# But Why?

Getting the code right first time is a statement borne out of numerous re-writes and refactors due to code having not been right first time. Did it work? Sure. Was it good enough? No. But why was that, and why is it so critical?

# The cost of refactoring

The cost of refactoring is obviously high. Writing something that works and then rewriting it again at some point incurs obvious costs in man hours, however it also costs something much more than that. A codebases 'quality' is such a fragile ecosystem that it takes very little for it to be broken. Bad code impinges on this ecosystem so much that in The Pragmatic Programmer it's posited that a bad piece of code is like a broken window in a building: it's an invitation to break more windows, an invitation to write more bad code. Once bad code is introduced, it can spread like wildfire - copied by those who don't understand it and turning hastily into an anti-pattern. Sealing these windows up - fixing bad code - is critical for the continued quality of the codebase. Taking a beat and writing something right first time is the first - and most critical - step towards this ethereal chalice we call quality.

# Raising the Bar
Just good enough may be alright in a conceptual sense, however in a practical sense we must raise the bar of what good enough really is. Good enough not only adheres to the agreed patterns and practices, it refines and improves them. It drives comment amongst developers and serves to benefit the overall quality of the codebase, and ultimately the quality of the application. These are things we all try to do, but only through an appropriate amount of thought do we draw the right conclusions. Making sure your code adheres to the principles of SOLID is a good start. A method should do one thing and one thing only, and it should do it bloody well. Business logic does not belong in the presentation layer, and presentation logic does not belong in the business logic layer. Is the domain simply a representation of state, modified by external code, or does the domain manipulate itself? Making sure everyone is on the same page, but also making sure everyone is striving for something a bit better that gives value to the rest of the team is critical. 

# The End Game
So is it un-agile to get the code right first time? I don't think so. The inherent benefits may simply be lost on those who aren't working on the code every day. Getting it right first time is not doing too much work, it is not doing more than the bare minimum. This is because our definition of the bare minimum is different to a few lines on a story card. The bare minimum for a developer involves a high standard. An eye on the future. Thinking about others in the team and how they will feel when they see your code. But most of all it's about taking pride in your work and mending those broken windows every time you see them. 

To close off this post I will ask you one question: if you're working on a closed source system - as a lot of us in the .Net world do - would you be proud if it were open sourced, or would you want to go back and fix up a few things first? 
