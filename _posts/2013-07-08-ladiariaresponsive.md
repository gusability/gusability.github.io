---
layout: post
title: Hey, ladiaria, you have been responsified!
description: "I've created a stylesheet that responsifies the website of a local newspaper."
images:
  before: /images/2013-07-08-ladiariaresponsive/before.png
  after: /images/2013-07-08-ladiariaresponsive/after.png
modified: 2013-07-08
category: articles
tags: [lookma, responsive]
---

  All right, this is it. I'm tired of complaining about the lack of responsiveness of the
local newspapers I use to read online. It seems they didn't get how important is to deliver
their content to everybody, regardless user's abilities... and screen sizes! So I decided to
take the iniciative and responsify
<a href="http://ladiaria.com.uy" target="_blank">ladiaria's website</a>. And as a side effect
I started my own blog, one of my biggest pending issues.

<figure class="half">
  <img src="{{ page.images.before }}">
  <img src="{{ page.images.after }}">
  <figcaption>Before and after responsifying the site</figcaption>
</figure>

To start working on, I had do download a couple of sample pages and assets to make the
website look nice locally. That allowed me to start playing with the website styles until I
came up with a minimum viable responsive experience.

I responsified _only articles and sections_, both the kind of pages I access more frequently
from my mobile. Since I obviously wasn't able to rewrite the page structure, I was constrained
to create a stylesheet that overwrites the previous styles when the screen size is narrower than 758px.

### Instructions

If the folks of ladiaria accept my suggestion, they should follow these instructions.

1. Download the <a href="https://raw.github.com/gusaaaaa/ladiaria-responsified/master/responsify.css" target="_blank">
   stylesheet</a> that responsifies the website.
2. Save it in the server's <code>media</code> directory.
3. Drop the following line in the head tag, after linking all the stylesheets:
{% highlight html %}
   <link type="text/css" href="responsify.css" rel="stylesheet">
{% endhighlight %}

### Disclaimer note

Be warned that the
<a href="https://raw.github.com/gusaaaaa/ladiaria-responsified/master/responsify.css" target="_blank">
CSS</a> I created is intended only for articles and sections, so it should be linked only when
rendering those type of pages. I noticed that the class of the ```<body>``` element changes depending
on the page type so another approach would be to prefix all the style's selectors with
```body.article``` and ```body.section```.

<hr />

I hope the folks of ladiaria and other local newspapers understand the importance of moving towards a
responsive experience and accept this proposal.
