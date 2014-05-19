---
layout: post
title:  "Hybrid SQL and NoSQL models with PostgreSQL - Part 1: An introduction"
date: "2014-05-17"
---

In this series I'm going to be covering the use of [PostgreSQL][pg] as a hybrid between a 
traditional SQL relational model and a document-based [NoSQL][nosql] model. First I'll cover 
the database side of things, and then I'll go into how I implemented data access from an 
application written in C#.

But first, some context. <!-- More -->Recently I've had the opportunity to work on a project where some parts where relational in nature, while 
others were nothing more than an object graph. Other teams in the company had already realized this, so
newer developments are being made against a document database. In my case though, my project 
was already stored in a relational database, and some of the complexity in the code was 
caused by trying to please the relational model and the [ORM][orm] in use. If we could only store 
these documents exactly as they were, then a lot of our maintenance problems would go away.

Enter PostgreSQL. In version 9.3 they introduced a [JSON][json] datatype for columns. Internally 
the JSON blob is stored as text in the database, but it has some basic 
validation checking to ensure that the data is actually a valid JSON object. But it doesn't 
stop there. You can also do [a couple of interesting things][json_ops] with JSON such as filtering by a 
value, indexing on a value, and even flattening into a row so that you can perform joins with 
your other tables. In our case we only required storing and filtering the JSON object, so that's 
mostly what I'm going to cover in this series.  

I'll be updating this post with links to the other parts as they become available.

{% include hybrid-model-series-links.html %}

[pg]: http://www.postgresql.org/about/
[nosql]: http://en.wikipedia.org/wiki/Nosql#Document_store
[orm]: http://en.wikipedia.org/wiki/Object-relational_mapping
[json]: http://en.wikipedia.org/wiki/JSON
[json_ops]: http://www.postgresql.org/docs/9.3/static/functions-json.html
