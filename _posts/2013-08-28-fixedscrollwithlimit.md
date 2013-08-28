---
layout: post
title: Fixed float with vertical limit
description: "Easy way to create a fixed float with a vertical limit"
images:
  scheme: /images/2013-08-28-fixedscrollwithlimit/scheme.png
modified: 2013-08-28
category: articles
tags: [javascript]
---

When you need to fix a float constraining its vertical movement to a particular area, using
CSS' ```position: fixed``` won't work. That's because
<a href="http://tympanus.net/codrops/2013/07/17/troubleshooting-css/#article-position" target="_blank">fixed positioning</a>
removes the element from the flow and positions it relative to the viewport, so there's no
way of using CSS to limit its vertical movement.

There's an out-of-the-box JQuery plugin called <a href="https://github.com/bigspotteddog/ScrollToFixed" target="_blank">
ScrollToFixed</a> that does the job, but if you just want to patch your page with a quick
solution here you have an alternative.

It's 90% based on <a href="http://jqueryfordesigners.com/fixed-floating-elements/" target="_blank">this post</a>
with the difference that it stops floating the element when reaching a particular vertical
position. <a href="http://jsfiddle.net/2BZ2a/" target="_blank">Demo here</a>.

<figure>
  <img src="{{ page.images.scheme }}">
</figure>

### Markup and CSS

In this case we have a two-column layout and we want to fixed-float the aside column
but without trespassing the footer's upper bound. To see the trick you probably need
to add more content to main and footer sections.

{% highlight html %}
<section>
  <main>
    Main content
  </main>
  <aside id="fixedfloat_wrapper">
    <div id="fixedfloat">
      What I want to float
    </div>
  </aside>
</section>
<footer>
  No trespassing
</footer>
{% endhighlight %}

{% highlight css %}
section main {
    float: left;
    width: 60%;
}
section aside {
    float: right;
    width: 40%;
}
#fixedfloat {
    width: 100%;
}
footer {
    clear: both;
}
{% endhighlight %}

### Javascript

{% highlight javascript %}
var $wrapper = $('#fixedfloat_wrapper'),
    $fixedfloat = $('#fixedfloat'),
    $limit = $('footer'),
    top = $wrapper.offset().top - parseFloat($wrapper.css('margin-top').replace(/auto/, 0));

$wrapper.css('position', 'relative');
$fixedfloat.css('position', 'absolute');

$(window).scroll(function (event) {
    // what the y position of the scroll is
    var y = $(this).scrollTop();
    // whether that's below the form
    if (y < top) {
        $fixedfloat.css('top', '');
    } else if (y >= top && y + $fixedfloat.height() + parseFloat($fixedfloat.css('margin-top')) <= $limit.offset().top - parseFloat($limit.css('margin-top'))) {
        $fixedfloat.css('top', y - top + 'px');
    }
});
{% endhighlight %}

You can add margin to the top of the fixedfloat element and it will work fine.

As you may have noticed, it uses absolute positioning modifying the ```top``` property
when the vertical scroll is greater than the wrapper's top offset. An improvement would
be using fixed positioning instead and stopping (```position: absolute``` and freezing
the element's ```top``` property) the movement when reaching the footer.
Contributions are always welcome.
