---
layout: post
title: PHP7 and Symfony Performance
author: Piers Warmers
---

I missed the talk but these slides – [PHP by Rasmus Lerdorf](http://talks.php.net/oz15#/perf2014) – inspired me to 
take a look for myself. 


So I thought I'd run a very quick test to see how a fresh Symfony Framework 2.6.4 install performed on in comparison 
testing against PHP 5.6.6-dev vs PHP 7.0.0-dev.

I'm using a [Rasmus' Vagrant configuration](https://github.com/rlerdorf/php7dev) and Apache Benchmark to 
target the demonstration "Hello World" script shipped with Symfony – and enabled on production.
 
## The Results

I ran 600 hits with a concurrency of 100 and found that the mean for each was:

PHP 5.6.6-dev = 220.55 req/sec  
PHP 7.0.0-dev = 341.77 req/sec

That's a pretty impressive performance boost.

I'd love to see a [Blackfire](https://blackfire.io/) probe compatible with PHP7 to see where the performance gains are.