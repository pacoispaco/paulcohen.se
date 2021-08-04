---
title: "Some Facts and Conclusions About REST and HTTP"
date: 2011-09-28T11:22:35+02:00
updated: 2020-04-24T07:51:35+02:00
tags:
 - software-development
 - web-development
draft: false
---

Fact 1: HTTP stands for Hypertext **Transfer** Protocol. It does not stand for Hypertext Transport Protocol.

Fact 2: HTTP is not a transport protocol in the sense of a computer or network communication protocol, despite it being used as such by SOAP. It is an **application-level protocol for distributed, collaborative, hypermedia information systems**.

Fact 3: HTTP is a **protocol**, i.e. a specification. It can be implemented in software.

Fact 4: REST is a set of **software architectural principles and constraints** for characterizing a certain class of systems; those that consist of distributed and independently developed and continuously evolving applications that need to collaborate.

Fact 5: HTTP is **based** on the REST principles and constraints.

Fact 6: HTTP is the foundation of **the largest and most rapidly evolving software system in the world**, that has also proven to be immensly scalable yet remained simple to use; namely the World Wide Web.

Conclusion 1: If you are in a situation where you need to implement an application or parts of a system that will consist of distributed and independently developed and continuously evolving applications that need to collaborate and must adress scalability, you will benefit hugely from applying REST principles and constraints in your design and implementation.

Conclusion 2: If you use HTTP as the foundation for your application, or parts of a system, you won’t have to invent and implement your own REST-based application-level protocol and you will also have an abundance of production stable HTTP software that can be used in your implementation.

Conclusion 3: If you respect the REST principles and constraints built into the HTTP protocol when implementing your application, or parts of the system, using HTTP you stand a very good chance of ending up with an application that works well in a distributed environment and that collaborates well with other applications that probably are being developed and evolving independently of your application.

Conclusion 4: REST and HTTP are good for you. Try to understand them.
