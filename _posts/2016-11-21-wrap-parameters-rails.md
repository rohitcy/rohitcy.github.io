---
layout: post
title:  "Wrap parameters in Rails"
tags:   [rails, actioncontroller]
categories: ["TIL"]
---
`ActionController::ParamsWrapper` in Rails is responsible for wrapping the parameters hash into a nested hash.

Recently while building a rest api for one of the applications I ran into an strange problem.

While making a `POST` request with some JSON params, I observed that the request params were getting duplicated in an unusual manner for eg. when I made following request to a controller named `transactions` with following params:

{% highlight json %}
  {
    "amount": 10000,
    "operator": "vodafone"
  }
{% endhighlight %}

Here's what I was getting in my controller as request params:
{% highlight ruby %}
  {
    "amount" => 10000,
    "operator" => 'vodafone',
    "transactions" =>  {
      "amount" => 10000,
      "operator" => 'vodafone',
    }
  }
{% endhighlight %}

As we can see above the same params are getting duplicated, after searching a little while for what could be the reason for this, I got introduced to Rails's [ActionController::ParamsWrapper](http://api.rubyonrails.org/classes/ActionController/ParamsWrapper.html) module.

Well in brief what this module does is that it wraps the parameters hash into a nested hash, which in turn allows us to submit requests without having to specify any root elements. Rails has it because it provides us an advantage as it wraps the parameters in a nested hash using the `controller-name` as key by default (we can change this as well). So let's say if we `enable` ParamsWrapper for :json format then we don't need to send JSON parameters like:

{% highlight json %}
  {
    fruit: {
      "name": "apple",
      "price": 200
    }
  }
{% endhighlight %}

instead we can just send them as:

{% highlight json %}
  {
    "name": "apple",
    "price": 200
  }
{% endhighlight %}

This functionality is enabled in wrap_parameters initializer of your app(`config/initializers/wrap_parameters.rb`) and can be customized. Below is how `wrap_parameters` is initialized by default when we create a new Rails app.

{% highlight ruby %}
ActiveSupport.on_load(:action_controller) do
  wrap_parameters format: [:json] if respond_to?(:wrap_parameters)
end
{% endhighlight %}

Rails has params wrapping on by default for `json`, but if we don't want our params to be wrapped we can either remove `json` from the  `format` array which will turn off params wrapping for the whole application altogether. In case you want to do this for a specific controller, `transactions_controller` in our example, it can be done by calling `wrap_parameters false` in our controller.

References:

*  Customizing ParamsWrapper: [ActionController::ParamsWrapper](http://api.rubyonrails.org/classes/ActionController/ParamsWrapper.html)
