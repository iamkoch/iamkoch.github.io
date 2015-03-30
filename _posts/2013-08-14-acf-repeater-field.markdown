---
layout: post
status: publish
published: true
title: ACF Repeater Field
author:
  display_name: Antony Koch
  login: amkoch
  email: ant@iamkoch.com
  url: ''
author_login: amkoch
author_email: ant@iamkoch.com
wordpress_id: 272
wordpress_url: http://iamkoch.com/?p=272
date: '2013-08-14 07:26:26 +0100'
date_gmt: '2013-08-14 07:26:26 +0100'
categories:
- PHP
- Wordpress
tags:
- wor
comments: []
---
The docs for this don't seem to be working at the moment and the examples I've seen after a quick google seem to avoid the API in favour or just treating the repeater as an array.
I thought I'd document the correct usage here in case people questioned the other blogs on the net.
{% highlight php %}
&lt;?php
  if ( get_field('item_images') ):
    while( has_sub_field('item_images') ): ?&gt;
      &lt;div class=&quot;work-image&quot;&gt;
        &lt;?php echo wp_get_attachment_image(get_sub_field('item_image'), 'full') ?&gt;
      &lt;/div&gt; &lt;?php
    endwhile;
  endif;
?&gt;
{% endhighlight %}
