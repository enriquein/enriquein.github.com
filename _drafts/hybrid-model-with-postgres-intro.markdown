---
layout: post
title:  "Hybrid SQL and NoSQL models with PostgreSQL - An introduction"
date: "2014-05-17"
---

In this series I'm going to be covering the use of PostgreSQL as a hybrid between a 
traditional SQL relational model and a document-based NoSQL model. Recently I've had 
the opportunity to work on a project where some parts where relational in nature, while 
others were nothing more than an object graph. Other teams had already realized this, so
newer developments are being made against a document database. In my case though, my project 
was already stored in a relational database, and some of the complexity in the code was 
caused by trying to please the relational model and the ORM in use. If we could only store 
this one document exactly as it is, then a lot of our maintenance problems would go away.

The data was originally stored in a SQL Server database. The first thought was to store this 
document in an xml field. However, this was going to present another set of challenges. Then 
I thought of storing it as json inside a VARCHAR(MAX) field. This would've been a "good enough" 
choice, except that we also needed to filter on some of the document's fields for some queries 
and for the analytics side. Just thinking of those substring and 'LIKE' queries makes me 
cringe. What we needed was something else.

Enter PostgreSQL. In version 9.3 they introduced a JSON datatype for columns. What in reality 
happens is that your JSON blob is stored as text in the database, but it has some basic 
validation checking to ensure that the data is actually a valid JSON object. But it doesn't 
stop there. You can also do a couple of interesting things with JSON such as filtering by a 
value, indexing on a value, and even flattening into a row so that you can perform joins with 
your other tables. In our case we only required storing and filtering the JSON object. So that's 
mostly what I'm going to cover in this series. First I'll cover the database side of things, and 
then I'll go into how I implemented data access from .Net. 

I'll be updating this post with links to the other parts as they become available.