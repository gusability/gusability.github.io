---
layout: post
title: Pure CSS carousel using target pseudo-selector
description: "How to create a carousel without using Javascript"
modified: 2013-09-02
category: articles
tags: [css]
---

Given its potential, it's surprising that CSS' target pseudo-selector is not widely used to
achieve certain interaction effects without using Javascript. It is intended to select
elements whose id atribute matches the URL's
<a href="http://en.wikipedia.org/wiki/Fragment_identifier" target="_blank">fragment identifier</a>,
i.e. the text that comes after hash in the URL.

For example, to select the following headline when the fragment identifier is referencing
it,

{% highlight html %}
<h1 id="summary">Summary</h1>
{% endhighlight %}

you can use the target pseudo-selector like this:

{% highlight css %}
#summary:target {
  background-color: yellow;
}
{% endhighlight %}

Then, when the URL is like ```www.example.com/#summary```, the browser will jump
the scroll to the referenced headline changing its background color to yellow.

A more advanced use would be combining that feature with link elements that trigger
behavior inside the page. If it's possible to highlight an element clicking a
link, why wouldn't be possible to create something more sofisticated like
an <a href="http://developer.yahoo.com/ypatterns/navigation/accordion.html" target="_blank">
accordion menu</a>? (Jump to the last section to check out a variety of examples of
target pseudo-selector uses).

Here I present a pure CSS carousel using the target pseudo-element and I think the technique
could be easly extended to other use cases.

## Carousel implementation using CSS only

Basically, the idea is to store the state of the interaction (e.g. on/off, open/closed,
step1/step2/step3) in the URL's fragment identifier and trigger a particular behavior
when the state changes using a combination of dummy elements and the target pseudo-element.

<a href="http://jsfiddle.net/vYykU/" target="_blank">Demo here</a>.

### Markup

{% highlight html %}
<div id="carousel">
    <span class="state" id="goto_article1"></span>
    <span class="state" id="goto_article2"></span>
    <span class="state" id="goto_article3"></span>
    <section>
        <article id="article1">
            <h2>Article 1</h2>
            <a href="#goto_article2">Next</a>
        </article>
        <article id="article2">
            <h2>Article 2</h2>
            <a href="#goto_article1">Prev</a>
            <a href="#goto_article3">Next</a>
        </article>
        <article id="article3">
            <h2>Article 3</h2>
            <a href="#goto_article2">Prev</a>
        </article>
    </section>
</div>
{% endhighlight %}

### CSS

{% highlight css %}
body {
    margin: 0;
}

#carousel {
    width: 100%;
}

section {
    width: 300%;
    overflow: hidden;
    transition: margin 0.5s ease;
}

article {
    float: left;
    width: 33.333%; /* width := parent's width / 3 */
}

.state {
  display: none;
}

.state#goto_article2:target ~ section {
    margin-left: -100%;
}

.state#goto_article3:target ~ section {
    margin-left: -200%;
}
{% endhighlight %}

We have three states here, ```goto_article1```, ```goto_article2``` and ```goto_article3```.
The ```span.state``` dummy elements are identified with the names of these states to
capture the change. When the URL's fragment identifier changes, the ```section``` tag
sibling of the dummy elements is selected using the general sibling selector ```~```.

So if the state changes to ```goto_article2```, the section is shifted one-third to the
left allowing the second article to show up:

{% highlight css %}
.state#goto_article2:target ~ section {
    margin-left: -100%;
}
{% endhighlight %}

Analogously, if the state changes to ```goto_article3```, the section is shifted
two-thirds to the left allowing the third article to show up.

When the state changes to ```goto_article1``` or no state is selected (default), then
no shifting is applied to the section and the left margin comes back to zero.

Hiding the dummy elements is important to prevent the browser from actually jumping to
them:

{% highlight css %}
.state {
  display: none;
}
{% endhighlight %}

Target pseudo-element is
<a href="http://caniuse.com/#search=target" target="_blank">supported by most of
current browsers, including Internet Explorer 9.0 and beyond</a>. I tried this
example with Chrome and Safari and it works fine.

An alternative technique to trigger behavior using pure CSS is called
<a href="http://css-tricks.com/the-checkbox-hack/" target="_blank">the checkbox hack</a>,
but I prefer using links rather than labels. Moreover, using the target
technique the browser remembers the states so you can go back and forth in
history to trigger behavior.

## Other notable examples of the target pseudo-selector technique

- <a href="http://designmodo.com/css3-accordion-menu/" target="_blank">Accordion menu</a>
- <a href="http://snook.ca/archives/html_and_css/yellow-fade-technique-css-animations" target="_blank">Highlighting sections</a> (from <a href="http://css-tricks.com/on-target/" target="_blank">css-tricks</a>)
- <a href="http://hacks.mozilla.org/2012/02/a-simple-image-gallery-using-only-css-and-the-target-selector/" target="_blank">Image gallery</a>
- <a href="http://csscience.com/css3-tabs/" target="_blank">Tabs</a>
