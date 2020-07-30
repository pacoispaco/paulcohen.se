---
title: "Database Psychosis"
date: 2011-03-19T10:02:58+02:00
updated: 2020-04-24T07:40:58+02:00
draft: true
---

Most applications have the need to have data persistent between application sessions. Persistence means that data is saved and can be read at a later time, even if the power to the device running the application is turned off in between application restarts. The only way to achieve this is to store data to some sort of file system on a non-volatile storage, usually in the form of a hard disk. This is a fundamental technique of software systems; use the underlying file system, which actually manages the use of the hard disks, to persistently store and read data to and from files.

When talking about software systems with non-programmers it is common to use the rather vague term database when talking about persistent data. This is understandable, since non-programmers shouldn’t have to know all the details of making data persistent. Also the term database is a easier name to use than a persistent data storage mechanism.

However, surprisingly, many developers are not aware of the simple technique of making data persistent by using the file system. Instead they assume a database means a fully fledged transactional ACID database system. Even worse, many developers equate a fully fledged transactional ACID database system with a relational database system. And in the most pathological cases they equate this with Microsoft SQL server. I call this phenomenon, database psychosis.

Strangely enough, some programmers seem even unable to understand that all database systems eventually rely on the underlying file system.

The principles of the Unix philosophy as as expressed by Eric S. Raymond lists among others the following principles:

* Rule of Simplicity: Design for simplicity; add complexity only where you must.
* Rule of Parsimony: Write a big program only when it is clear by demonstration that nothing else will do.

The latter rule could be rephrased for database “situations” as:

* Rule 1 of database Parsimony: Use a database system only when it is clear by demonstration that just using a file or set of files won’t do.
* Rule 2 of database Parsimony: Use a database system with a dedicated database server only when it is clear by demonstration that an embedded database system won’t do.
* Rule 3a of database Parsimony: Use a relational database system only when it is clear by demonstration that a key/value database system won’t do.
* Rule 3b of database Parsimony: Use an object or document database system only when it is clear by demonstration that a key/value database system won’t do.
* Rule 4 of database Parsimony: Use Microsoft SQL Server only when it is clear by demonstration that no other relational database system will do.
