---
layout: post
title: Bookmarklet that unhides file names in GitHub
description: "A handy bookmarklet that shows hidden filenames in GitHub"
images:
  before: /images/2014-02-18-github-show-full-filenames/before.png
  after: /images/2014-02-18-github-show-full-filenames/after.png
modified: 2014-02-18
category: articles
tags: [bookmarklet, javascript]
---

Drag and drop the following button link to your bookmarks:

<a class="btn" href="javascript:(function()%7Bvar%20nodes%20%3D%20document.getElementsByClassName(%22info%22)%3B%20for%20(var%20info%20in%20nodes)%20%7B%20if%20(nodes%5Binfo%5D.children%20%3D%3D%20null%20%7C%7C%20nodes%5Binfo%5D.children.length%20!%3D%202)%20break%3B%20nodes%5Binfo%5D.children%5B1%5D.className%20%3D%20nodes%5Binfo%5D.children%5B1%5D.className.replace(%27css-truncate%20css-truncate-target%27%2C%20%27%27)%3B%20%7D%3B%7D)()">GH unhide</a>

Before:

<figure>
  <img src="{{ page.images.before }}">
</figure>

After:

<figure>
  <img src="{{ page.images.after }}">
</figure>

Try it out in this commit: <a href="https://github.com/rails/rails/commit/6d87cd028b32570973450424db164e5405a0ee13">https://github.com/rails/rails/commit/6d87cd028b32570973450424db164e5405a0ee13</a>.
