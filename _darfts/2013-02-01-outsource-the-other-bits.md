---
layout: post
title: Outsource The Other Bits
author: Piers Warmers
---

If your not using dependency management for external code inclusion your doing it wrong. With the very robust and simple-to-use [Composer](http://getcomposer.org/), there's no reason to include code in any other way.

Before we get started, I'd strongly recommend reading Fabien Potencier fantastic book, [Create Your Own Framework](https://github.com/fabpot/Create-Your-Framework). This post is meant to be concise and exemplify a simple use case of including Symfony components via Composer, not elaborate on more extensive framework architecture.

It all starts with a `composer.json` file:

{% highlight yaml %}
{
    "require": {
        "symfony/http-foundation": "2.1.*",
        "symfony/http-kernel": "2.1.*",
        "symfony/routing": "2.1.*",
        "twig/twig": "1.*"
    }
}
{% endhighlight %}

Now we are able to use the Composer command line utility to do all the dependency management for us. Running the following commands will do the trick.

{% highlight bash %}
$ mkdir ~/Sites/ComposerTest
$ ~/Sites/ComposerTest
$ curl -s https://getcomposer.org/installer | php
$ php composer.phar install
$ ls
-rw-r--r-- composer.json
-rw-r--r-- composer.lock
-rwxr-xr-x composer.phar
drwxr-xr-x vendor
{% endhighlight %}

Composer locates the required packages and download them into a `vendor` directory under you project root. That's right, libraries and versions are project specific. What's more is that Composer provides you with a `composer.lock` file which details specific versions. This means that teams can synchronise versions states.

Get Things Rolling
------------------

To start off with, lets look at a really simple usage of Composer to familiarise ourselves with it's basic usage. Composer provides an autoloading utility so you can start using your new libraries with little effort. Lets create our script and see things in action, `app.php`:

{% highlight php %}
<?php

// app.php

require_once __DIR__.'/vendor/autoload.php';

use Symfony\Component\HttpFoundation\Request;

$request = Request::createFromGlobals();

printf(
    '%s %s',
    $request->query->get('message', 'Hi'),
    $request->query->get('name', 'Secret Squirrel')
);
{% endhighlight %}

… and to see it running quickly, try PHPs built-in server (PHP 5.4+) and point your browser to [http://localhost:8000/app.php/?message=Hi&name=Foo](http://localhost:8000/app.php/?message=Hi&name=Foo):

{% highlight bash %}
$ php -S localhost:8000
{% endhighlight %}

Simple right, but we can see a few important things. Firstly Composer has allowed for a very neat inclusion of an external library. Secondly we can see how a common web application requirement can be quickly filled by not getting tempted to write the code ourselves.

Adding Routing and Response
--------------------------

Routes are great but not the sort of thing you want to spend time building logic for. So lets use the Symfony Routing Component to provide a simple utility for defining and matching routes.

{% highlight php %}
<?php

// app.php

require_once __DIR__.'/vendor/autoload.php';

use Symfony\Component\HttpFoundation\Request,
    Symfony\Component\Routing\Route,
    Symfony\Component\Routing\RouteCollection,
    Symfony\Component\Routing\Matcher\UrlMatcher,
    Symfony\Component\Routing\RequestContext,
    Symfony\Component\HttpFoundation\Response,
    Symfony\Component\Routing\Exception\MethodNotAllowedException,
    Symfony\Component\Routing\Exception\ResourceNotFoundException;

$routes = new RouteCollection();

$routes->add('say', new Route('/say/{message}/{name}', array('message' => 'hello', 'name' => 'world')));
$routes->add('index', new Route('/'));

$context = new RequestContext();
$request = Request::createFromGlobals();
$context->fromRequest($request);

try {
    $matcher = new UrlMatcher($routes, $context);
    $attributes = $matcher->match($request->getPathInfo());
    if($attributes['_route'] == 'say') {
        $response = new Response(sprintf('%s %s', $attributes['message'], $attributes['name']));
    } else {
        $response = new Response('Welcome!');
    }
} catch (MethodNotAllowedException $e) {
    $response = new Response('Method Not Allowed', 405);
} catch (ResourceNotFoundException $e) {
    $response = new Response('Not Found', 404);
}

$response->send();
{% endhighlight %}

The Next Stage
--------------

{% highlight php %}
<?php

// app.php

require_once __DIR__.'/vendor/autoload.php';

use Symfony\Component\HttpFoundation\Request,
    Symfony\Component\Routing\Route,
    Symfony\Component\Routing\RouteCollection,
    Symfony\Component\Routing\Matcher\UrlMatcher,
    Symfony\Component\Routing\RequestContext,
    Symfony\Component\HttpFoundation\Response,
    Symfony\Component\HttpKernel\HttpKernel,
    Symfony\Component\HttpKernel\Controller\ControllerResolver,
    Symfony\Component\EventDispatcher\EventDispatcher,
    Symfony\Component\HttpKernel\Debug\ExceptionHandler,
    Symfony\Component\HttpKernel\EventListener\ExceptionListener,
    Symfony\Component\HttpKernel\EventListener\RouterListener;

new ControllerResolver();

$routes = new RouteCollection();

$routes->add(
    'say',
    new Route('/say/{message}/{name}',
        array(
            'message' => 'hello',
            'name' => 'world',
            '_controller' =>
                function(Request $request){
                    return new Response(sprintf('%s %s', $request->get('message'), $request->get('name')));
                }
        )
    )
);

$request = Request::createFromGlobals();

$dispatcher = new EventDispatcher();

$urlMatcher = new UrlMatcher($routes, new RequestContext());

$dispatcher->addSubscriber(new RouterListener($urlMatcher));

$exceptionHandler = function($exception) {
    $handler = new ExceptionHandler();
    return $handler->createResponse($exception);
};

$dispatcher->addSubscriber(new ExceptionListener($exceptionHandler));

$kernel = new HttpKernel($dispatcher, new ControllerResolver());
$kernel->handle($request)->send();

{% endhighlight %}

The Final Step
-------------

{% highlight php %}
<?php

// app.php

require_once __DIR__.'/vendor/autoload.php';

use Symfony\Component\HttpFoundation\Request,
    Symfony\Component\Routing\Route,
    Symfony\Component\Routing\RouteCollection,
    Symfony\Component\Routing\Matcher\UrlMatcher,
    Symfony\Component\Routing\RequestContext,
    Symfony\Component\HttpFoundation\Response,
    Symfony\Component\HttpKernel\HttpKernel,
    Symfony\Component\HttpKernel\Controller\ControllerResolver,
    Symfony\Component\EventDispatcher\EventDispatcher,
    Symfony\Component\HttpKernel\Debug\ExceptionHandler,
    Symfony\Component\HttpKernel\EventListener\ExceptionListener,
    Symfony\Component\HttpKernel\EventListener\RouterListener;

new ControllerResolver();

$routes = new RouteCollection();

$routes->add(
    'say',
    new Route('/say/{message}/{name}',
        array(
            'message' => 'hello',
            'name' => 'world',
            '_controller' =>
                function(Request $request){

                    Twig_Autoloader::register();
                    $loader = new Twig_Loader_Filesystem(__DIR__);
                    $twig = new Twig_Environment($loader);

                    return new Response(
                        $twig->render('index.html.twig', array(
                                'message' => $request->get('message'),
                                'name' => $request->get('name')
                            ))
                        );
                }
        )
    )
);

$request = Request::createFromGlobals();

$dispatcher = new EventDispatcher();

$urlMatcher = new UrlMatcher($routes, new RequestContext());

$dispatcher->addSubscriber(new RouterListener($urlMatcher));

$exceptionHandler = function($exception) {
    $handler = new ExceptionHandler();
    return $handler->createResponse($exception);
};

$dispatcher->addSubscriber(new ExceptionListener($exceptionHandler));

$kernel = new HttpKernel($dispatcher, new ControllerResolver());
$kernel->handle($request)->send();
{% endhighlight %}





{% highlight html %}
<html>
    <head>
        <title>A message for {{ "{{ name " }}}}</title>
    </head>
    <body>
        <h1>{{ "{{ message " }}}} {{ "{{ name " }}}}</h1>
    </body>
</html>
{% endhighlight %}



Ten Types Of Cool
-----------------

{% highlight html %}
<html>
<head>
    <title>{{ "{% block title '' %" }}}</title>
</head>
<body>
    {{ "{% block content '' %" }}}
</body>
</html>
{% endhighlight %}

{% highlight html %}
{{ "{% extends 'layout.html.twig' %" }}}

{{ "{% block title 'A message for ' ~ name %" }}}

{{ "{%  block content %" }}}

    <h1>{{ "{{ message " }}}} {{ "{{ name " }}}}</h1>

{{ "{%  endblock %" }}}
{% endhighlight %}