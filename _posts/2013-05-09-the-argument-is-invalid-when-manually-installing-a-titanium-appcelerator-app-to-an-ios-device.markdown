---
layout: post
status: publish
published: true
title: "'The Argument is Invalid' - When manually installing a Titanium Appcelerator
  app to an iOS device"
author:
  display_name: Antony Koch
  login: amkoch
  email: ant@iamkoch.com
  url: ''
author_login: amkoch
author_email: ant@iamkoch.com
wordpress_id: 267
wordpress_url: http://iamkoch.com/?p=267
date: '2013-05-09 13:27:24 +0100'
date_gmt: '2013-05-09 13:27:24 +0100'
categories:
- iOS
tags:
- titanium
- appcelerator
comments: []
---
<p>Been getting this for a while with a lot of irritation!</p>
<p>It all worked fine on the iOS simulator, but failed when trying to install the app.</p>
<p>A bit of googling lead me to an article saying that the JS minification process can leak into some of the critical iOS files. I re-ran the 'install to iOS device' wizard, unticked the box and hey presto it works. Bit of a weird one that.<a href="http://iamkoch.com/wp-content/uploads/2013/05/TitaniumBuildWindow.png"><img class="alignnone size-full wp-image-268" alt="Titanium Build Window" src="http://iamkoch.com/wp-content/uploads/2013/05/TitaniumBuildWindow.png" width="523" height="519" /></a></p>
