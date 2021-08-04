---
title: "Do not force users to change passwords"
date: 2010-10-23T11:36:24+02:00
updated: 2021-08-01T16:09:24+02:00
tags:
 - passwords
 - digital
 - sysadmin
 - infosec
draft: false
---

This post is the first in a series which I call “The flat earth posts”. In each post I discuss a commonly held truth which is a) untrue, b) hinders progress and c) causes unecessary work.

Many organizations force their users to change their passwords every 3 months or according to some other regular schedule. This policy is based on old established security policy "wisdom" that has been around for a long time and which is seldom questioned. The argument is that changing passwords improves security.

In fact, forcing users to change passwords on a regular schedule degrades security and causes dissatisfaction in your organization. Here are some of the effects of this policy:

* Users start writing down passwords (bad for security).
* Users loose time and get locked out of accounts (bad for productivity).
* Users get irritated (bad for motivation).
* Users phone the IT support help desk to recover accounts they’ve been locked out from (increased help desk work).

The only time it is appropriate to force users to change their passwords is when you know or think their accounts have been compromised.

I wrote this original post back in 2010. In 2017 NIST (the U.S. National Institute of Standards and Technology) at last updated their [publication on Digital Identity Guidelines](https://pages.nist.gov/800-63-3/sp800-63b.html) to recommend _**against forcing users to periodically change their passwords**_.

> Verifiers SHOULD NOT require memorized secrets to be changed arbitrarily (e.g., periodically). However, verifiers SHALL force a change if there is evidence of compromise of the authenticator.

Also, since I wrote this post in 2010, two-factor authentication has become much more common in many applications and business settings, which solves many of the other drawbacks with password based authentication. Furthermore there now exist good password managers, for keeping track of your passwords, which reduce the need for writing down your passwords. Yes, thats what normal people end up doing, and even more so when they are forced to change their password. Today I use [KeepassX](https://www.keepassx.org) on my Linux machine and [Keepass2Android](https://play.google.com/store/apps/details?id=keepass2android.keepass2android) on my Android phone and tablet, to keep track of passwords and various PIN codes.

References:

* [NIST Special Publication 800-63B, Digital Identity Guidelines - Authentication and Lifecycle Management](https://pages.nist.gov/800-63-3/sp800-63b.html).
* [Security Myths and Passwords](https://www.cerias.purdue.edu/site/blog/post/password-change-myths/).
* [The Security of Modern Password Expiration: An Algorithmic Framework and Empirical Analysis](http://www.cs.unc.edu/~fabian/papers/PasswordExpire.pdf).
* [Why do we annoy our users](https://www.sicpers.info/2010/03/why-do-we-annoy-our-users/)?
* [So Long, And No Thanks for the Externalities: The Rational Rejection of Security Advice by Users](https://www.nspw.org/papers/2009/nspw2009-herley.pdf).
* [How forcing Password Changes Actually Weakens Security](https://helgeklein.com/blog/how-forcing-password-changes-actually-weakens-security/).
* [Are Users Right in Rejecting Security Advice](https://www.techrepublic.com/blog/it-security/are-users-right-in-rejecting-security-advice/)?
* [Password Expiration Considered Harmfull](https://cryptosmith.com/password-sanity/exp-harmful/).
