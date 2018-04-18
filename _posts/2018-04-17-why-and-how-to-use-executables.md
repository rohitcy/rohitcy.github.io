---
layout: post
title:  "Why Executables? and How to use Executables?"
tags:   [rails, ruby, sidekiq, executables]
categories: ["Blog"]
---

### Why Executables?

If you have ever worked on a application which depends on lots of third party apis then you might know that most of the apis don't work as expected.

Such was the case in one of the projects I was working on. It falls under Fintech domain and being a fintech application, it requires a user's details to be shared with different third parties for compliance and regulatory reasons and this is handelled by lots of background jobs.

Most of the times this background jobs won't run properly due to various causes
like some third party is down or sometimes just because life as we know is not so perfect. In order to solve this first we started executing this executables from rails console of our prod server. But this led to more problems like dependency on a particular team member since everybody doesn't have production access, and as the number of job failures increased it became time consuming as well. In order to solve this new problem we came up with a quick solution, we started exposing this jobs on our application's admin panel so that our operations team can run them as per need, it worked in short run as a quick fix.

But as we know quick fixes are not always good in a long run and leads to more problems. It happens so we ended up adding multiple routes and controller actions whenever we needed a new executable to be exposed on our admin panel. This became a problem which demanded proper solution and so it happens I came across sidekiq's web module which is nothing but a Rack app which can be mounted with your rails application and it facilitates job monitoring. This led me to a question that if I can monitor jobs via a web interface why can't I execute them as well via a web interface, and thus I created executables.

### How to use Executables?

Using executables is as easy and simple like any other gem. In order to get started with executables you can follow the Getting Started guide [here](https://github.com/rohitcy/executables#getting-started). Once you are done with the setup mentioned in getting started guide you can access your executables by navigating to the mounted url like as follows.

<br>

![Executable Dashboard]({{ "/assets/images/executables-dashboard.png" | absolute_url }})

<br>


As mentioned in the screenshot in order to execute a particular executable you can click on it and you will be redirected to a screen like following, here you will be able to see the executable methods available and arguments it takes, you can provide respective arguments and click on execute and you're all set.

<br>

![Executable execute page]({{ "/assets/images/executables-execute.png" | absolute_url }})

<br>

That's all their to executables as of now, feel free to shoot out any questions/doubts you've in the comments below and as always you can create a new issue [here](https://github.com/rohitcy/executables/issues) if you're facing any problems with executables.



