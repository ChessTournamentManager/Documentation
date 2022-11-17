<h1> Database Research </h1>

<h2> Table of Contents </h2>

- [Introduction](#introduction)
- [My Requirements](#my-requirements)
  - [The database needs to be fast](#the-database-needs-to-be-fast)
  - [The database should be NoSQL](#the-database-should-be-nosql)
- [Database Options](#database-options)
  - [MongoDB](#mongodb)
  - [Redis](#redis)
- [Final Choice](#final-choice)
- [Next Steps](#next-steps)

## Introduction

For this project, I need to choose a suitable database for all of my services. Since all of my services work very similar, I only want to choose one type of database. I will then use multiple instances of that database type for my services.


## My Requirements

### The database needs to be fast

I want my website to be as responsive as possible. It would be a shame if I used a slow database while using such a fast module bundler like Vite. The database must also be able to scale well, in case many people use the website. This is not that much as a requirement though. It is more important that the database is fast than it is scalable.

### The database should be NoSQL

There are multiple reasons why I don't want to use a database with SQL. First of all, SQL databases are generally slower than NoSQL databases, especially for key-value storage (https://www.cs.rochester.edu/courses/261/fall2017/termpaper/submissions/06/Paper.pdf). Furthermore, it is easier to do scaling when using NoSQL databases. When scaling with SQL databases, you have to migrate to a more expensive server (verticle scaling). When scaling with NoSQL databases, you can just add more cheaper servers (horizontal scaling) (https://www.mongodb.com/nosql-explained/nosql-vs-sql, https://www.geeksforgeeks.org/sql-vs-nosql-which-one-is-better-to-use/). Lastly, I want to use NoSQL, because I have never used a NoSQL database in an individual project before and I would like to gain more experience by using it in this project.


## Database Options

### MongoDB


### Redis


###


###



## Final Choice


## Next Steps

