---
layout: post
status: publish
published: true
title: NCrunch and StyleCop
author: Antony Koch
author_login: amkoch
author_email: ant@iamkoch.com
wordpress_id: 106
wordpress_url: http://iamkoch.com/?p=106
date: '2012-08-19 19:34:53 +0100'
date_gmt: '2012-08-19 19:34:53 +0100'
categories:
- ".Net"
- Unit Testing
tags:
- NCrunch
comments: []
---
I ran into some problems last week once we changed all our projects to target StyleCop, namely that for some reason NCrunch wouldn't pick up my Settings.StyleCop file.
The fix was to go into the NCrunch configuration for the solution and add a route to the file in the 'additional files to include' section. 
The routes use some nice Ant-style (sadly not named after me) relative paths, however as my Settings.StyleCop file was in the root directory sitting next to the .sln file I merely had to add "Settings.StyleCop" as a path, hit recompile and hey presto - my NCrunch build went green again.
