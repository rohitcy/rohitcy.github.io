---
layout: post
title:  "Template rendering with mustache"
date:   2016-07-12 13:00:00 +0530
author: rohit
tags:   [javascript, mustache]
---

In some widgets rich websites we are often faced with a situation where we need to update all the widgets on a page based on change of a particular attribute e.g consider a web page where you can select a city and based on the selected city you have to update four sections lets say hotels, atms, hospitals and parks in the city.

One way to approach it, will be making an ajax call on city change and then updating the four widgets from the response data.

Wouldn't it be nice if we can avoid this ajax calls and load all the data at once as some key value pair(ofcourse city being the key) and then onchange of city just render the widgets again with the new data.

Well you're in luck as [Mustache](https://github.com/janl/mustache.js) let's you do just that.

Continuing with our cities and hotel example let's see how we can approach it through Mustache, suppose that we need to render hotel and park of a selected city,

All you need to do is include a template like:
{% highlight javascript %}
  <script id="hotel-template" type="x-tmpl-mustache">
      Hotel: {{hotel}}
  </script>
{% endhighlight %}

Now on city change you can render your template using:

{% highlight javascript %}
var hotel_template = document.getElementById('hotel-template').innerHTML;
var rendered_hotel = Mustache.render(hotel_template, {hotel: hotel[city]});
{% endhighlight %}

And you can inject the rendered html and update hotel element like:

{% highlight javascript %}
document.getElementById('hotel').innerHTML = rendered_hotel;
{% endhighlight %}


To see a full-fledged example please refer [fiddle](https://jsfiddle.net/eurodo061/Lp1ch5vy/).
