---
layout: post
title: Hey, ladiaria, you have been responsified!
description: "I've created a stylesheet that responsifies the website of a local newspaper."
modified: 2013-07-08
category: articles
tags: [lookma, responsive]
---

  All right, this is it. I'm tired of complaining about the lack of responsiveness of the
local newspapers I use to read online. It seems they didn't get how important is to deliver
their content to everybody, regardless user's abilities... and screen sizes! So I decided to
take the iniciative and responsify
<a href="http://ladiaria.com.uy" target="_blank">ladiaria's website</a>. And as a side effect 
start my own blog, one of my biggest pending issue.

I have responsified _only articles and sections_, both the kind of pages I access more frequently
from my mobile. Since I obviously wasn't able to rewrite the page structure (something I
would've like to do: they unfortunately serve HTML 4.01), I was constrained to overwrite the
styles only.

If the folks of ladiaria accept my suggestion, they should follow these instructions:

1. Download the <a href="https://raw.github.com/gusaaaaa/ladiaria-responsified/master/responsify.css" target="_blank">
   stylesheet</a> that responsifies the website.

2. Save it in the server's <code>media</code> directory.

3. Drop the following line in the head tag, after you load all the stylesheets:
   ```
   <link type="text/css" href="responsify.css" rel="stylesheet">
   ```

### Disclaimer note

Be warned that the <a href="https://raw.github.com/gusaaaaa/ladiaria-responsified/master/responsify.css" target="_blank">
stylesheet</a> I created is intended only for articles and sections, so just load it when rendering articles
and sections. I noticed that you change the body class depending on the page so another approach would be to prefix all
the style's selectors with ```body.article``` and ```body.section```. I leave it to your discretion.

<hr />

I hope the folks of ladiaria understand the importance of moving towards a responsive experience and accept
this proposal.
