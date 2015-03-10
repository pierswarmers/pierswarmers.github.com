---
layout: post
title: PHP / Symfony Checker
author: Piers Warmers
---

Before I commit changes to my PHP / Symfony projects, I like to pre-check it against a few utilities to ensure
quality and consistency. This little script to automates the steps:
 
1. A PHP compilation check.
2. A syntax cleanup - [Sensio Labs](http://cs.sensiolabs.org/)
3. Run my unit tests - [PHPUnit](https://phpunit.de) - with code coverage as an option.
4. Then optionally commit and push changes - only if the above steps passed.

It's simple and I can modify it easily from one project to another. I thought I'd both share it and ask for any tips on
improvements.

## Here it is: check.sh

You can run it via something like:

`./check.sh`  
or  
`./check.sh -g -b -p -m "Fixed the stuff and things."`

<script src="https://gist.github.com/pierswarmers/0c0c5f80d31daa94a461.js"></script>
