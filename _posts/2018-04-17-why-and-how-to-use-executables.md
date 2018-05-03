---
layout: post
title:  "Why Executables? and How to use Executables?"
tags:   [rails, ruby, sidekiq, executables]
categories: ["Blog"]
---

### Why Executables?

Executables is built to solve following problems:

1) Do you often login to your prod server to manually execute some code?

2) Do you have dependency on a particular dev(the one with PROD access) in your team to get things done?

3) Do you hate writing redundant code just to make an POC to be executable via a web interface?

If you face above problems then executables might be the solution for you, with the help of executables you can expose your jobs/workers/anything that accepts JSON datatypes (numbers, strings, boolean, array, hash) and can execute them via a web interface keep reading to know how you can achieve this.

### How to use Executables?

Using executables is as easy and simple like any other gem. In order to get started with executables you can follow the Getting Started guide [here](https://github.com/rohitcy/executables#getting-started). Once you are done with the setup mentioned in getting started guide you can access your executables by navigating to the mounted url like as follows.

<br>

![Executable Dashboard]({{ "/assets/images/executables-dashboard.png" | absolute_url }})

<br>


As mentioned in the screenshot in order to execute a particular executable you can click on it and you will be redirected to a screen like following, here you will be able to see the executable methods available and arguments it takes, you can provide respective arguments and as per your need you can run the executable inline or async.

<br>

![Executable execute page]({{ "/assets/images/executables-execute.png" | absolute_url }})

<br>

That's all their to executables as of now, feel free to shoot out any questions/doubts you've in the comments below and as always you can create a new issue [here](https://github.com/rohitcy/executables/issues) if you're facing any problems with executables.



