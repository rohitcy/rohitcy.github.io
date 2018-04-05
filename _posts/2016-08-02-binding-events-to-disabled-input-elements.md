---
layout: post
title:  "Binding mouse events to disabled input elements"
date:   2016-08-02 16:00:00 +0530
author: rohit
tags:   [javascript]
---
Do you know, you can't bind mouse events to a input element once it is disabled?

Recently I came across a situation where I had to show a tooltip on `mouseover` of a disabled button, specifying the reason why it is disabled. For that I tried binding `onmouseover` event to the button and failed in doing so, after a bit of searching I came to know that we cannot bind any mouse events to a disabled element as shown in below embedded fiddle.

<iframe width="100%" height="300" src="//jsfiddle.net/eurodo061/vv6fuLc8/embedded/js,html,css,result/dark/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

To solve this problem I came up with two approaches.

1. Wrapping the input element inside a parent element: We can wrap our disabled input element inside a parent element and bind events on the parent element as shown in below embedded fiddle.

    <iframe width="100%" height="300" src="//jsfiddle.net/eurodo061/vab20c9h/embedded/js,html,css,result/dark/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

2. Making the element look like a disabled one through css by doing so we will be able to bind mouse events to the element as shown in below embedded fiddle.

    <iframe width="100%" height="300" src="//jsfiddle.net/eurodo061/nz25348t/embedded/js,html,css,result/dark/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

So by using any of the above mentioned approaches we can bind mouse events to a disabled element.
