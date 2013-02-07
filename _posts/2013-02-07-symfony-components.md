---
layout: post
title: Symfony Components for Drupal
author: Piers Warmers
---

I've been lucky enough to be invited to give a talk at [DrupalCon Sydney](http://sydney2013.drupal.org) about Symfony Components. So here are the [slides](http://sydney2013.drupal.org/sites/default/files/slides/Symfony%20Components%20-%20A%20Travel%20Guide_7.pdf) and some extended examples for those interested.

<iframe width="420" height="315" src="http://www.youtube.com/embed/Tep1-oq6jrU" frameborder="0" allowfullscreen></iframe>

The following is an example which demonstrates how the Symfony HTTP Kernel, HTTP Foundation, Routing and Twig Components can be used to build a very simple application.

The commands noted in the discussion download, unpack and then run the example application.

**Please note:** these commands may need to be adjusted depending on your setup. Also PHP testing server is only available for PHP 5.4.

{% highlight bash %}

$ curl https://gist.github.com/pierswarmers/4712678/download > app.tar.gz | tar -zx
$ cd gist4712678-*
$ curl -s https://getcomposer.org/installer | php
$ php ./composer.phar install
$ php -S localhost:8000

{% endhighlight %}

Check it out: [http://localhost:8000/app.php/say/hello/DrupalCon](http://localhost:8000/app.php/say/hello/DrupalCon)

And the code for browsing pleasure…

<script src="https://gist.github.com/pierswarmers/4712678.js"></script>