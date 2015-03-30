---
layout: post
status: publish
published: true
title: How to get libcore sources for HttpUrlConnectionImpl.java and other classes
  missing from the base android SDKs
author: Antony Koch
author_login: amkoch
author_email: ant@iamkoch.com
wordpress_id: 296
wordpress_url: http://iamkoch.com/?p=296
date: '2013-11-11 10:40:44 +0000'
date_gmt: '2013-11-11 10:40:44 +0000'
categories:
- Java
- Android
tags:
- android
- java
- sdk
comments: []
---
I'm doing some work that requires the usage of the libcore library, specifically using the class HttpUrlConnectionImpl.java or so my trusty IntelliJ debugger tells me.

Unfortunately, these sources aren't shipped with the standard sources that come with your android sdk in the sources directory, and you have to do some work to get them up and running.
Here's the steps I took to allow me to step into the classes and see what's going on.

First, you need to pull down the libcore sources from google into a location on your computer:

{% highlight bash %}
[bash]git clone https://android.googlesource.com/platform/libcore[/bash]
{% endhighlight %}

Now visit the libcore site and find the tag representing the version of the android OS you're using (or the one your IDE is bound to source-wise. Mine was android-4.1.2_r1 which I found by clicking on "more" at the bottom of the tag list. This presented me with the list of tags
From here, I copied the name of my tag, and in terminal, after checking out the source, I executed

{% highlight bash %}
cd libcore
git checkout -b tags/android-4.1.2_r1 android-4.1.2_r1
{% endhighlight %}

This checkout out the tag I required into a new branch on my machine. Then, in finder, I located the folder ./luni/src/main/java and copied the libcore folder into my &lt;sdk&gt;/sources/android-16 folder and hey presto, I could now step through the source!
