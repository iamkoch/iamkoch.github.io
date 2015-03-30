---
layout: post
status: publish
published: true
title: NServiceBus.Testing and NCrunch
author: Antony Koch
author_login: amkoch
author_email: ant@iamkoch.com
wordpress_id: 85
wordpress_url: http://iamkoch.com/?p=85
date: '2012-07-25 12:10:41 +0100'
date_gmt: '2012-07-25 12:10:41 +0100'
categories:
- ".Net"
- Unit Testing
tags:
- NServiceBus
- NCrunch
comments: []
---
I encountered an issue with NCrunch whereby the NServiceBus unit testing framework was blowing up, even though the ReSharper Test runner did not.
The error given was:
{% highlight c# %}
System.ArgumentException : The handler object created does not implement IMessageHandler&lt;T&gt;.
Parameter name: handlerCreationCallback
{% endhighlight %}
After some googling, I found the cause of the error to be a bug in NServiceBus. The fix involves prefixing the NServiceBus.Testing initializer:
{% highlight c# %}
Test.Initialize();
{% endhighlight %}
To look like the following, fixing the new line to match your namespacing rules and ensuring the final '!StartsWith("!NserviceBus")' line is left in
{% highlight c# %}
 // this is a workaround for a bug surrounding Test.Initialize() in NServiceBus
 // see https://github.com/NServiceBus/NServiceBus/issues/443 for info
 MessageConventionExtensions.IsMessageTypeAction =
        t =&gt; t.Namespace != null
             &amp;&amp; (t.Namespace.Contains(&quot;Events&quot;) || t.Namespace.Contains(&quot;Commands&quot;))
             &amp;&amp; !t.Namespace.StartsWith(&quot;NServiceBus&quot;);
 Test.Initialize();
{% endhighlight %}
And NCrunch will then work as expected.
