---
layout: post
status: publish
published: true
title: How to stop IE defaulting to Quirks / Compatibility mode
author: Antony Koch
author_login: amkoch
author_email: ant@iamkoch.com
wordpress_id: 108
wordpress_url: http://iamkoch.com/?p=108
date: '2012-10-01 12:29:31 +0100'
date_gmt: '2012-10-01 12:29:31 +0100'
categories:
- HTML
tags:
- IE7
- IE8
- IE9
comments: []
---
This is a real arse ache and something worth having yet another blog post out there.
I was experiencing some issues with a site defaulting to "Quirks Mode' meaning it just plain didn't work.
It took some choice googling but I eventually found the answer to be a simple one-liner in the <head> element the HTML.
{% highlight html %}
<meta http-equiv="X-UA-Compatible" content="IE=edge">
{% endhighlight %}
Include this and all of a sudden, if you've done it right, it'll look 'normal' in IE.
