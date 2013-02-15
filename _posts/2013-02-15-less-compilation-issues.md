---
layout: post
title: LESS Compilation Issues
author: Piers Warmers
---

I love [LESS](http://lesscss.org/) and I love [Assetic Filters in Symfony](http://symfony.com/doc/2.0/cookbook/assetic/asset_management.html). But a pretty painful bug while compiling [Bootstrap](http:twitter.github.com) LESS libraries nearly did my head in.

For the record, the issues were with [Node.js LESS](https://github.com/cloudhead/less.js) module. When compiling the Twitter Bootstraps mixins.ls I could see variables being lost with `NaN` being printed.

The solution? Installing lessphp did the trick `composer.json`:

{% highlight json %}
"require": {
    "leafo/lessphp": "dev-master"
}
{% endhighlight %}

Then in your `config.yml`:

{% highlight yaml %}
lessphp:
    file: %kernel.root_dir%/../vendor/leafo/lessphp/lessc.inc.php
    apply_to: "\.less$"
{% endhighlight %}