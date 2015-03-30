---
layout: post
status: publish
published: true
title: Funny Error in Entity Framework
author: Antony Koch
author_login: amkoch
author_email: ant@iamkoch.com
wordpress_id: 1
wordpress_url: http://localhost/~Ant/wordpress/?p=1
date: '2012-05-03 21:58:24 +0100'
date_gmt: '2012-05-03 21:58:24 +0100'
categories:
- ".Net"
tags:
- EntityFramework
- Linq-to-SQL
comments: []
---
I was receiving the error:

> The object cannot be deleted because it was not found in the ObjectStateManager

from the following code:
{% highlight c# %}
using (var dbContext = DbContextFactory.GetContext())
{
    var pendingQuoteRequest
        = dbContext
            .PendingQuoteRequests
            .FirstOrDefault(x => x.Id.Equals(quoteRequest.Id));
    if (pendingQuoteRequest != null)
    {
        dbContext
            .PendingQuoteRequests
            .Remove(pendingQuoteRequest);
        dbContext.Save();
    }
}
{% endhighlight %}
Oddly, I managed to fix it with the following code:
{% highlight c# %}
using (var dbContext = DbContextFactory.GetContext())
{
    var pendingQuoteRequest = dbContext.PendingQuoteRequests.Where(x => x.Id.Equals(quoteRequest.Id)).FirstOrDefault();
    if (pendingQuoteRequest != null)
    {
       dbContext.PendingQuoteRequests.Remove(pendingQuoteRequest);
       dbContext.Save();
    }
}
{% endhighlight %}
It seems that {% highlight c# %}FirstOrDefault{% endhighlight %} behaves differently to Where().FirstOrDefault() within Linq-to-SQL.
Weird one, huh?
