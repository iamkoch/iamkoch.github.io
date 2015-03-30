---
layout: post
status: publish
published: true
title: Agile Dev Practices - Day 1, Morning 1
author:
  display_name: Antony Koch
  login: amkoch
  email: ant@iamkoch.com
  url: ''
author_login: amkoch
author_email: ant@iamkoch.com
wordpress_id: 243
wordpress_url: http://iamkoch.com/?p=243
date: '2013-03-05 12:25:12 +0000'
date_gmt: '2013-03-05 12:25:12 +0000'
categories:
- Agile
- Testing
- Agile Dev Practices
tags:
- exploratory testing
- testing
comments: []
---
So this morning, with a rather weary head from drinking some excellent beer last night, I headed down for the first couple of sessions. I didn't quite make the first keynote as it was time at what seemed to be an ungodly hour - 9.15.

I did, however, manage to drag my sorry ass out of bed and get to Sergej Mudruk's "Agile Test Automation at XING Mobile Team" which I found quite interesting. The talk was in an area I don't have a great deal of experience in, but it was a high-level overview of how XING develop their apps for both Android and iOS, and how they test them. They preferred to test on devices for Android which I'm not surprised by, but the cool part is they have cameras pointing at the devices so you can RDP into a machine and watch the tests running live on the device. Cool huh? They tested their iOS devices in the simulator as 'the iOS simulator is a lot more stable'. Again, no surprises there :)

Talk two was Meike Mertsch and Markus Gärtner's  "Exploratory Testing - for devs, testers and you". This one tickled my fancy yesterday, even more so having hung out with Markus a bit last night whilst surrounded by beer. There were some good slides and some good points raised, as well as highlighting the testing triangle with Unit Tests at the bottom, integration tests in the middle and UI tests at the top. The guys placed manual testing in a dirty cloud above said pyramid, but a couple of good soundbites were that automation is there for the things you are going to do hundreds or thousands of times, and manual testing is there to allow you to get to know the system, and ideally find out those parts of the system that you didn't know you didn't know about. Another line that really hit home for me was if you (as a dev, tester, whoever) get frustrated using your system's interface then you're getting a window into what your system might be like for your users. I've never really made that connection before but now it's been said it seems so obvious. The guys talked about session-based test management, adhering to a test charter:

1. Explore &lt;target&gt;
2. With &lt;resources&gt;
3. To discover &lt;information&gt;

Where:

4. &lt;target&gt; - feature, area of system
5. &lt;resources&gt; - tools, data sets, techniques
6. &lt;information&gt; - lays down your mission. 

What are we interested in? Why are we doing this? Secuity, performance, reliability

This then lead into talking about the importance of heuristics when testing, which were summed up into HICCUPSF

- History
- Image
- Comparable Products
- Claims
- User Expectations
- Purpose
- Product
- Standards and Statutes
- Familiar Problems

These were a small section taken from the Heuristic Testing Cheat Sheet which looks like a goldmine of info for a starter-for-ten when you're testing something.
There's lots more I could, and probably should, write, but I have to head back down for the rest of the day's talks and workshops...
