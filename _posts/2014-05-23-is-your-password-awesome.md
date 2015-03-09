---
layout: post
title: Understanding awesome passwords
author: Piers Warmers
---

![Passwords Can Be Tough](/images/2014-05/passwords.png)

Everyone knows that long random passwords are best, but how random, how long and what about practicality?

## A bad password

Let's start with an example of a **bad** password: “G3org3.1984”.

There are many methods hackers use to exploit systems. One of which is the "brute-force attack", a technique which attempts to discover a users password by trying one variation after another. Each failure triggering another attempt with a new password. You might be thinking, **"my password is awesome, that would take forever"**. Is it, is it really that awesome?

## A closer look at "brute-force"

Brute force attacks are not actually carried out by a person. Instead a computer is given the task — even if it takes days, months or longer. The time it takes is linked to the strength of your password.

Lets look at a password example: “J@ck.1984”. A mathematical perspective uses a term “key space” to determine it’s strength. The “key space” for that password would be 85<sup>9</sup> (depending on the characters used [^1]). That is to say that it would take 85<sup>9</sup> or less[^2] attempts to crack it.

**85<sup>9</sup> = 231,616,950,000,000,000... is a huge number!**

## “J@ck.1984” is a BAD password

Here's why. 85<sup>9</sup> is a big number, but we're being naive to assume a hacker is going to simply try random character combinations. We're dealing with people. Creatures of habit that love to give things meaning and have limited memory. A dangerous combination which hackers use to optimise their efforts.

Think of the complexity reduction if you focus on passwords built on simple proposition:

`password = "<word or name>.<year between 1940 and 2014>”`

Complexity reduction may be further reduced if the persons email address "jack.beanstalk@example.com" was known.

## An  Acronym Solves All

A good password is built on four simple steps:

| **C** | Character Rich | Use uppercase, lowercase, numbers and special characters |
| **U** | Unique         | A fresh password for each credential                     |
| **R** | Random         | Avoids words, names and dates                            |
| **L** | Long           | 15 characters or more                                    

"C.U.R.L",  a recipe for awesome passwords.

## Great, but we live in the real world?

No one is expecting you to memorise dozens of long, complicated codes. If you haven't already -- now might be time to move to a dedicated password management program like [RoboForm](http://www.roboform.com/), or [1Password](https://agilebits.com/onepassword).

At the very least, keep the "C.U.R.L" principles in mind when creating your next password. Your credentials are yours and yours alone.

## Further Reading and References

- [Keeping Secrets: Good Password Practice](http://go.eset.com/us/resources/white-papers/EsetWP-KeepingSecrets20090814.pdf)
- [A birthday present every eleven wallets?](http://www.jbonneau.com/doc/BPA12-FC-banking_pin_security.pdf)
- [Choosing a smart password](http://gmailblog.blogspot.com.au/2009/10/choosing-smart-password.html)
- [10,000 Top Passwords](https://xato.net/passwords/more-top-worst-passwords/#more-269)

[^1]: 85 being the number of uppercase, lowercase and special characters, 9 being the length of password.
[^2]: On average it takes half the “key space” to solve.

