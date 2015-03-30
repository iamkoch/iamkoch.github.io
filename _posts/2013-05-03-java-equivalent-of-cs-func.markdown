---
layout: post
status: publish
published: true
title: Java equivalent of C#'s Func
author: Antony Koch
author_login: amkoch
author_email: ant@iamkoch.com
wordpress_id: 253
wordpress_url: http://iamkoch.com/?p=253
date: '2013-05-03 23:07:24 +0100'
date_gmt: '2013-05-03 23:07:24 +0100'
categories:
- ".Net"
- Java
tags: []
comments: []
---
If you're wondering how to translate a .Net Func&lt;T, T1&gt; (up to the 16th item) into comparable java code, then here's how. First, the C#
{% highlight c# %}
public class Car {
  // ID
  public string ModelId { get; set; }
}
public class Account {
  // ID
  public int Id { get; set; }
}
// some code
public void AddIdsToList&lt;T&gt;(Collection&lt;T&gt; collection, List&lt;string&gt; ids, Func&lt;T, string&gt; extractId) {
  foreach (T item in collection) {
    ids.add(extractId.Invoke(item));
  }
}
public List&lt;string&gt; CollectIdentifiers() {
  var car = new Car { ModelId = &quot;Fiesta&quot; };
  var account = new Account { Id = 45 };
  var ids = new List&lt;string&gt;();
  AddIdsToList(new Collection&lt;Car&gt;(car), ids, x =&gt; x.ModelId);
  AddIdsToList(new Collection&lt;Account&gt;(account), ids, x =&gt; x.Id.ToString());
}
{% endhighlight %}
And now, the same in Java using inner classes
{% highlight java %}
public class Car {
  private String modelId;
  public Car(String modelId) {
    this.modelId = modelId;
  }
  public String getModelId() {
    return this.modelId;
  }
}
public class Account {
  private int id;
  public Account(int id) {
    this.id = id;
  }
  // ID
  public int getId() {
    return this.id;
  }
}
interface GetTheIdFunc&lt;T&gt; {
  String getTheId(T item);
}
// some code
public &lt;T&gt; void AddIdsToList(Collection&lt;T&gt; collection, List&lt;string&gt; ids, GetTheIdFunc&lt;T&gt; extractId) {
 for (T item : collection) {
   ids.add(extractId.getTheId(item));
 }
}
public List&lt;string&gt; CollectIdentifiers() {
  Car car = new Car(&quot;Fiesta&quot;);
  Account account = new Account(45);
  List&lt;string&gt; ids = new ArrayList&lt;string&gt;();
  AddIdsToList(new ArrayList&lt;Car&gt;(car), ids, new GetTheIdFunc&lt;Car&gt;() {
    public String getTheId(Car item) {
      return item.getModelId();
    }
  });
 AddIdsToList(new ArrayList&lt;Account&gt;(account), ids, new GetTheIdFunc&lt;Account&gt;() {
    public String getTheId(Account item) {
      return item.getId().toString();
    }
  });
}
{% endhighlight %}
Quite different but conceptually pretty clean and logical really when you consider that an interface offers a contract. Not as flexible on the fly as C#, but not a lot of extra code. Where these internal interface types should rest package-wise is an interesting one though. Any thoughts?
