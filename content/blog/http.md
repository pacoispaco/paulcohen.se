---
title: "Some reflections on HTTP"
date: 2010-06-23T12:14:34+02:00
updated: 2020-04-23T11:59:34+02:00
draft: false
---

Since I wrote this back in 2010, the heated and confused REST/HTTP vs SOAP debate is over. Today, a REST-ful HTTP/JSON API is firmly established as the best-practice technology for web API:s. Of course, there are many legacy systems that provide API:s implemented with other technologies based on other design principles or simply because it seemed like a good idea at the time.

I still think these simple reflections on HTTP are relevant for understanding why REST-ful HTTP/JSON API:s have become so dominant today. And why we should continue developing these API:s.

> The Hypertext Transfer Protocol (HTTP) is an application-level protocol for distibuted, collaborative, hypermedia information systems. It is a generic, stateless, protocol which can be used for many tasks beyond its use for hypertext, such as name servers and distributed object management systems, through extension of its request methods, error codes and headers [47]. A feature of HTTP is the typing and negotiation of data representation, allowing systems to be built independently of the data being transferred. - IETF/RFC 2616: Hypertext Transfer Protocol.

Read that again. And again. And again. HTTP is an Application Layer protocol. It is _not_ a transport protocol. It’s for application-to-application communication. It's for applications that want to transfer data back and forth in a distributed setting.

The key properties of HTTP in my opinion are:

* Adaption to purpose. This means no unneccessary extra features. HTTP is for transferring hyperlinked resources between distributed applications. Maybe Hyperlinked Resource Transfer Protocol (HRTP) would have been a better name for the protocol!
* Statelessness. This means no session handles or enforced state based process paths to keep track of. This is good for implementing loosely coupled application-to-application logic.
* Resource oriented. This is instead of function or method oriented. This minimizes interface dependencies.
* Representation agnostic. This means that there are no constraints on resource formats. So we are free to use formats that are not based on XML. Hurray!
* Simplicity. Which is good and beautiful!

These key properties are natural consequences of the REST principles that where applied in the design of HTTP. Thank you Roy Fielding!

With HTTP you also get authentication, encryption and caching. We know it works. We know it scales. Up and down. You can do HTTP communication in all programming languages. There are many open source production stable HTTP servers that we easily can integrate our existing information systems with. We know we can do really cool things with HTTP with little effort and excellent performance.

All aspiring web service architects and programmers should ask themselves two fundamental questions:

1. How come the World Wide Web works so well without being recompiled every morning?
2. What software and life-cycle principles and properties are important for two applications that communicate with each other but are owned and developed by different organizations?
