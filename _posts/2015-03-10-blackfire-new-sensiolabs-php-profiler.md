---
layout: post
title: Blackfire, PHP Profiling by SensioLabs 
author: Piers Warmers
---

[Blackfire](https://blackfire.io) is a new service by [SensioLabs](http://sensiolabs.com/). It's a web based utility to help benchmark your PHP 
applications. I've just sat down to give it a try. I'm blown away!

Installation was very simple via a Brew Keg (`blackfireio/homebrew-blackfire`) and I tested it with a [Symfony Framework](http://symfony.com/)
application using one of my custom commands.

The standard interface tracks a single test batch:

[![Blackfire](/images/2015-02/blackfire.png)](/images/2015-02/blackfire.png)

You have 10 slots to store test batches. This allows you to compare your benchmarks from one iteration
to another, as shown below:

[![Blackfire](/images/2015-02/blackfire-comparison.png)](/images/2015-02/blackfire-comparison.png)

Hat's off to the interface people - that's some sweet work.

A incredible addition to the toolkit.

Also, take a look at this simple [toggle for XDebug](http://tech.enekochan.com/en/2015/03/06/disable-xdebug-temporary-while-using-blackfireio/).
