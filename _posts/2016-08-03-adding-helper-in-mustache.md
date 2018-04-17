---
layout: post
title:  "How to add helper in mustache"
tags:   [javascript, mustache]
categories: ["TIL"]
---
In my previous [post](http://borgs.cybrilla.com/tils/template-rendering-with-mustache/) I gave an brief overview about [mustache](https://github.com/janl/mustache.js) and how we can render templates with it.

Well one thing that mustache brands about itself is that it is a logicless way of rendering templates, so what if you want to dynamically change or let's just say format some data while rendering template e.g. you are rendering a table as a template and one of the column is price and let's say you want to display this price in multiple of thousands (5000 as 5K).

Mustache being logicless you can't directly do any arithmetic operations in a template, to do so mustache provides something called as `lambdas`. According to mustache's documentation we can pass callable objects(lambda or function) while rendering a template and if the value is a callable object, such as a function or lambda, the object will be invoked and passed the block of text. The text passed is the literal block, unrendered. {{tags}} will not have been expanded - the lambda should do that on its own. In this way we can implement filters(5000 to 5K) or caching.

Well that's just a lot of theoritical stuff let's see how we can put it to acutal use continuing with our example(table as a template), we will pass a function that formats price while rendering the template.

Considering our template as:
{% highlight javascript %}
  <script id="price-template" type="x-tmpl-mustache">
    Price: {{ "{{#formatPrice" }}}} {{"{{price" }}}} {{"{{/formatPrice" }}}}
  </script>
{% endhighlight %}
Here `formatPrice` is an callable object(a function) which is going to format the price for us we will pass this callable object while rendering template as:
{% highlight javascript %}
  var rendered_price = Mustache.render(price_template, {
    price: price[city],
    formatPrice: function() {
      return function(val, render) {
        return (parseInt(render(val)) / 1000).toString() + "K";
      }
    },
  });
{% endhighlight %}
So that's how we can use helpers in mustache for implementing filters to see a complete example please refer this [fiddle](https://jsfiddle.net/eurodo061/aj7175vu/).

## References:

* Mustache 5 lambda: [https://mustache.github.io/mustache.5.html](https://mustache.github.io/mustache.5.html)
