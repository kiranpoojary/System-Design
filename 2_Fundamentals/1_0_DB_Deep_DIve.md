# 1. What are Databases?

Databases as a persistent storage solution can support various types of structured data. They store, update, and retrieve information.

Databases are expected to be durable. Different Database Solutions have trade-offs involved as discussed.

1. Is DB a server? Yes but separated from normal server
2. Is DB a File Sys? No: file is unstructure but DB  structured
3. Can DB in Memory? yes it can be in cache

# 2. Storage and Retrieval

We look at the intricate relationship between hardware and software in the context of database storage.

The focus is on how data is stored in tables with specific data types, leveraging indexes and algorithms internally.

We look at how SQL queries are run, breaking down components such as FROM, WHERE, GROUP BY, HAVING, ORDER BY, and LIMIT.


## How data stored in DB

1. Magnetic Tape
2. Solid State Disk

## How data stores in DB(Algo)

1. RDB: B+ Tree are used
2. pages
3. Hash Table
4. Pointer

## How Data Red in DB

HashTable+B+ Tree= Index

Query execution order: 

Query optimizer


# 3. NoSQL database

NoSQL databases encompass various types of data storage requirements.

Key-value stores have risen in popularity due to their off-the-shelf solutions, like fault tolerance, sharding, etc...

We also touch on the concept of database consistency, highlighting its dependence on the application's nature.

Databases are generally considered a single source of truth for data-related operations, with an expectation of consistent data.

Database Management System (DBMS) manages configurations, lead replicas, and system coordination, serving as a vital component in the overall database infrastructure.

Can't be queries using SQL queries

# 4. Types of Databases:

## Graph DB

1. stores data internaly as node and edges
2. graph queries

## Timeseries DB

1. store data that part of time series
2. metric data
3. monitoring data

## Object DB

store complex data objects.


# 5. What database should you choose?

he right database for your project depends your app needs, what you're comfy with, and the pros and cons of each choice.

For example, Postgres is solid but isn't built for write heavy workloads, while Cassandra is great for fault tolerance but needs tweaking for consistency.

Think of a database as a tool that handles data, letting you focus on your app's important parts.
