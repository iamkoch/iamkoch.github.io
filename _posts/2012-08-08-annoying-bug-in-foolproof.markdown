---
layout: post
status: publish
published: true
title: Bug in mvcfoolproof.unobtrusive.js when using RegExMatch
author: Antony Koch
author_login: amkoch
author_email: ant@iamkoch.com
wordpress_id: 93
wordpress_url: http://iamkoch.com/?p=93
date: '2012-08-08 15:43:02 +0100'
date_gmt: '2012-08-08 15:43:02 +0100'
categories:
- ".Net"
- MVC
- JavaScript
tags:
- unobtrusive
- foolproof
comments: []
---
Found this annoying bug today when using MVC Foolproof's unobtrusive JS with the following DataAnnotation
{% highlight c# %}
[RequiredIf(&quot;BusinessType&quot;, Operator.RegExMatch, &quot;[1,2,4]&quot;, ErrorMessage = &quot;Your company number is required&quot;)]
{% endhighlight %}
The code seems to parse the regex as an int if the original value for comparison is one, causing it to become NaN and consequently failing the regex.
To fix it, add the following at line 3:
{% highlight javascript %}
 var pattern = value2;
{% endhighlight %}
Then modify lines 53 and 54 to the following:
{% highlight javascript %}
case &quot;RegExMatch&quot;: return (new RegExp(pattern)).test(value1); break;
case &quot;NotRegExMatch&quot;: return !(new RegExp(pattern)).test(value1); break;
{% endhighlight %}
