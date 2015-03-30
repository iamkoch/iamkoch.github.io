---
layout: post
status: publish
published: true
title: Gotcha with IE8 and jQuery.wrap
author: Antony Koch
author_login: amkoch
author_email: ant@iamkoch.com
wordpress_id: 205
wordpress_url: http://iamkoch.com/?p=205
date: '2012-11-08 17:47:24 +0000'
date_gmt: '2012-11-08 17:47:24 +0000'
categories:
- JavaScript
tags:
- jquery
comments: []
---
I was just testing a site in IE8 using the amazing Browserstack and experienced an error within IE8 when trying to wrap some new elements around existing code.
# The Problem

Here's the code that was failing:

{% highlight javascript %}
$item.closest('a')
     .wrap($(&quot;&lt;div/&gt;&quot;, {class:&quot;item-holder&quot;}))
     .prepend($(&quot;&lt;strong/&gt;&quot;, {class:&quot;heading&quot;, text: $(item).attr('title')}))
     .prepend($(&quot;&lt;span/&gt;&quot;, {class:&quot;overlay&quot;}));
{% endhighlight %}

The error was occurring in the second line, spitting out an 'object doesn't support this property or method'.

# The Solution
It turns out that in IE8, you can't use an unescaped, unstringified word 'class' as I had been. Changing the class keywords to strings fixed it:

{% highlight javascript %}
$item.closest('a')
     .wrap($(&quot;&lt;div/&gt;&quot;, {&quot;class&quot;:&quot;item-holder&quot;}))
     .prepend($(&quot;&lt;strong/&gt;&quot;, {&quot;class&quot;:&quot;heading&quot;, text: $(item).attr('title')}))
     .prepend($(&quot;&lt;span/&gt;&quot;, {&quot;class&quot;:&quot;overlay&quot;}));
{% endhighlight %}
