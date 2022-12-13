<h1> Database Research </h1>

<h2> Table of Contents </h2>

- [Introduction](#introduction)
- [My Requirements](#my-requirements)
  - [The database needs to be fast](#the-database-needs-to-be-fast)
  - [The database should be NoSQL](#the-database-should-be-nosql)
- [Database Options](#database-options)
  - [Redis](#redis)
  - [MongoDB](#mongodb)
  - [Cassandra](#cassandra)
  - [Scylla](#scylla)
- [Implementation](#implementation)
  - [Redis Implementation](#redis-implementation)
  - [MongoDB Implementation](#mongodb-implementation)
  - [Scylla Implementation](#scylla-implementation)
- [Benchmarking](#benchmarking)
  - [Redis Benchmark](#redis-benchmark)
  - [MongoDB Benchmark](#mongodb-benchmark)
- [Conclusion](#conclusion)
- [Next Steps](#next-steps)

# Introduction

For this project, I need to choose a suitable database for all of my services. Since all of my services work very similar, I only want to choose one type of database. I will then use multiple instances of that database type for my services.


# My Requirements

## The database needs to be fast

I want my website to be as responsive as possible. It would be a shame if I used a slow database while using such a fast module bundler like Vite. The database must also be able to scale well, in case many people use the website. This is not that much as a requirement though. It is more important that the database is fast than it is scalable.

## The database should be NoSQL

There are multiple reasons why I don't want to use a database with SQL. First of all, SQL databases are generally slower than NoSQL databases. According to a Rochester study, key-value storage databases are especially fast (https://www.cs.rochester.edu/courses/261/fall2017/termpaper/submissions/06/Paper.pdf). Furthermore, it is easier to do scaling when using NoSQL databases. When scaling with SQL databases, you have to migrate to a more expensive server (verticle scaling). When scaling with NoSQL databases, you can just add more cheaper servers (horizontal scaling) (https://www.mongodb.com/nosql-explained/nosql-vs-sql, https://www.geeksforgeeks.org/sql-vs-nosql-which-one-is-better-to-use/). Lastly, I want to use NoSQL, because I have never used a NoSQL database in an individual project before and I would like to gain more experience by using it in this project.


# Database Options

For my database options, I decided it would be good to pick different types of NoSQL databases, to test the theory that key-value databases are the fastest. I have also picked popular databases of each type, which are said to be very fast.

## Redis

**What type of database is Redis?**

Redis is a type of database known as a key-value database. In a key-value database, data is stored and retrieved using a unique key that identifies the particular item of data. The data (value) associated with a key can be any type of data, such as strings, integers, lists, dates, UUID's and more. Key-value databases are typically very fast and scalable, making them well-suited for applications that require quick access to large amounts of data.

[![Redis data types](../Images/redis_data_types.png)](../Images/redis_data_types.png)

*Data types in Redis*

**In what scenarios is Redis often used?**

Redis is a good option for applications which need to handle lots of small continuous reads and writes. It is more often used as a cache, but can also be used as a data store. It can also store data in-memory, which allows these actions to be done faster. It is also ideal for applications that don’t require frequent updates or need to support complex queries.

Redis is often used for the following use-cases:

- Caching
- Chatting, messaging, and queues
- Gaming leaderboards
- Session store
- Rich media streaming
- Geospatial
- Machine Learning
- Real-time analytics

For more information about these use-cases, go to [this page](https://aws.amazon.com/redis/#Popular_Redis_Use_Cases)

**How popular is Redis?**



**Which large companies use Redis?**



**How fast is Redis?**



**(What is the website of Redis?)**



## MongoDB

**What type of database is MongoDB?**



**In what scenarios is MongoDB often used?**



**How popular is MongoDB?**



**Which large companies use MongoDB?**



**How fast is MongoDB?**



**(What is the website of MongoDB?)**




## Cassandra


**What type of database is Apache Cassandra?**



**In what scenarios is Cassandra often used?**



**How popular is Cassandra?**



**Which large companies use Cassandra?**



**How fast is Cassandra?**



**(What is the website of Cassandra?)**




## Scylla

**What type of database is Scylla?**



**In what scenarios is Scylla often used?**



**How popular is Scylla?**



**Which large companies use Scylla?**



**How fast is Scylla?**



**(What is the website of Scylla?)**






# Implementation


## Redis Implementation



## MongoDB Implementation



## Scylla Implementation



# Benchmarking


## Redis Benchmark


## MongoDB Benchmark



# Conclusion



# Next Steps

