---
layout: post
title:  "Send POST data without a HTML form"
date:   2016-07-20 14:30:00 +0530
author: rohit
tags:   [javascript]
---
Recently while working on one of the projects I encountered a situation where I had to post some nested-data to a controller method and this data wasn't associated with any model hence rails `fields_for` was of no help.

So to acheive it I created a `params json` by fetching the values from DOM and then posted this data by building a form using a JS function as mentioned below.

{% highlight javascript %}
  post: function(path, params) {
    params["authenticity_token"] = $('meta[name=csrf-token]').attr('content');
    method = "post";
    var form = document.createElement("form");
    form.setAttribute("method", method);
    form.setAttribute("action", path);
    for(var key in params) {
        if(params.hasOwnProperty(key)) {
            var hiddenField = document.createElement("input");
            hiddenField.setAttribute("type", "hidden");
            hiddenField.setAttribute("name", key);
            hiddenField.setAttribute("value", params[key]);
            form.appendChild(hiddenField);
         }
    }
    document.body.appendChild(form);
    form.submit();
  }
{% endhighlight %}

As we know rails raises `ActionController::InvalidAuthenticityToken` error if authenticity_token is missing from params
`params["authenticity_token"] = $('meta[name=csrf-token]').attr('content');` in our function takes care of that.
