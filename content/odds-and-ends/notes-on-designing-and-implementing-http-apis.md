---
title: "Some Notes on Designing and Implementing REST-ful HTTP API:s"
date: 2016-03-26T13:43:02+02:00
updated: 2016-03-26T13:43:02+02:00
draft: true
tags:
 - software-development
 - web-development
 - api
 - digital
doc: true
---

This document contains some notes on designing and implementing REST-ful HTTP API:s. I started
writing this document simply because I felt a need to document my own slightly confused ideas
about how to do REST-ful HTTP API:s. I hope it can be of value to other developers struggling with
the same issues.

Usually discussions about HTTP API:s are driven by arguments on what approach or technique
is considered most REST-ful. The REST architectural style is described by Roy Fielding in his 2000
dissertation but it leaves a whole number of practical implementation and technical issues open as
how to actually implement REST-style systems. There is no automatic recipe for for building REST-
ful systems with HTTP, or for implementing any other architectural style or set of design principles.
In the end we always have to think and invent!

The approach in this document has been to use the REST-architectural style together with the Unix
design philosophy as a basis for a set of practical design and implementation choices for HTTP
API:s that I believe are REST-ful but, equally important, pragmatic and simple.

This document is organized into a number of sections, each dealing with a particular aspect of
designing and implementing REST-ful HTTP API:s. Eventually I may try to work on a more
structured synthesis of all the notes and provide the reader with a complete and consistent set of
practices for building HTTP API:s. Until then you will have to do the synthesis in your own head.

