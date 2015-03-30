---
layout: post
status: publish
published: true
title: How to load JSON content into the Sinatra params hash
author: Antony Koch
author_login: amkoch
author_email: ant@iamkoch.com
wordpress_id: 305
wordpress_url: http://iamkoch.com/?p=305
date: '2014-06-02 20:00:39 +0100'
date_gmt: '2014-06-02 20:00:39 +0100'
categories:
- Ruby
- Sinatra
tags: []
comments: []
---
Having trouble getting JSON content into the Sinatra params hash? Then read on...
I've been playing around with Sinatra a lot of late, including updating my Sinatra HTML5 Boilerplate to use Grunt - amongst other things, and in doing so started building a little backbone app by way of a proof of concept.
Part of Backbone's charm is to be able to provide a model a URL with which to save itself. Upon calling save() Backbone sends either the chosen attributes (passed into an array), or all the model's attributes if nothing is passed to the function call.
Sounds great, huh?
All was going rosily until I tried to use the params hash server-side, only to discover it was empty. This was odd, especially as I'm used to .Net's out-of-the-box model binding irrespective of content type. A bit of digging led me to discover this is by design, but can be handily circumvented with some sexy Rack middleware.
To get the JSON post content into Sinatra's params hash, first require the appropriate module/class combo:

{% highlight ruby %}
require 'rack/contrib'
{% endhighlight %}

Because I use a nice little bootup ruby file, I require this in there.
Once required, the dreadfully named PostBodyContentTypeParser must be loaded

{% highlight ruby %}
use ::Rack::PostBodyContentTypeParser
{% endhighlight %}

Once these two nifty lines are in place, your params hash will now be sexily filled with some lovely JSON content!
So, how does this work?

Pretty simply, actually. Digging into the source code, we can see the authors weren't too chuffed with the name either:

{% highlight ruby %}
# A Rack middleware for parsing POST/PUT body data when Content-Type is
 # not one of the standard supported types, like <tt>application/json</tt>.
 #
 # TODO: Find a better name.
 #
 class PostBodyContentTypeParser
{% endhighlight %}

The middleware then neatly hooks into Rack's call method (which is cheap to do per call and seems to be how all other middleware is loaded upon inspecting the stack):

{% highlight ruby %}
def call(env)
case env[CONTENT_TYPE]
when APPLICATION_JSON
env.update(FORM_HASH => JSON.parse(env[POST_BODY].read), FORM_INPUT => env[POST_BODY])
end
@app.call(env)
 end
{% endhighlight %}

Simple stuff - APPLICATION_JSON is a constant value of 'application/json', which when present as the request's Content-Type header parses the body and merges it with the form hash ready for loading into the params hash further down the line.
I love code like this. Rack is so well built that middleware like this involves a one-liner to hook in whatever you want to the low-level pipeline of your application.
