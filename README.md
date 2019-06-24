# Bootcamp - Server Team
Notes for a Server Team Bootcamp (Cassandra and lua OpenResty)

## Cassandra
### Install

### Tables - Logical Model

The fundamental object in Cassandra is the Table. It is roughly a souped up key-value store that holds entities that must conform to a schema. This schema is defined by a list of columns and their data types. Typical types are here null-able versions of: text, number, boolean, datetime, as well as Collection types thereof: Maps, List, Set.

The value is the entity itself: the full set of columns and their values. We alternatively call this a `row`.

The key is a subset of columns.

The fundamental restriction Cassandra places on this key is: you can only SELECT having first specified the precise value of the a fixed subset of the key called the `Partition Key`. All other SELECTs are deemed full-table scans and are usually forbidden by default.

Furthermore, reads are optimized for getting all the values for a single fixed partition key, or a single-partition read. In consequence, there is no optimization for selecting from multiple partitions in a single query.

#### Partition Keys

Logically, the table is one big collection but it should really be thought of as mini collections partitioned (yes, that's why this word is used) by the entries in the partition key.

#### Clustering Keys

#### The Only Way is Denormalization

There is no way of doing JOINs in Cassandra. Another way of putting it is there is no way of enforcing normalization using foreign key constraints like in SQL. To normalize data roughly means to be able to track all references between tables and ensure changes in one table is propagated to all refrences. Data in Cassandra is thus said to be `denormalized`. 

The upside is Cassandra's performance profile. The downside(?) is you have to deside applications from the ground up to account for denormalization.

#### Queries
##### INSERT and UPDATE
##### Conditional INSERT and UPDATE
##### SELECT
##### DELETE

#### Full Table Scans

### Nodes - Physical Model
#### Consistency
#### Any vs Quorum vs All
#### CAP Theorem
Roughly speaking, the CAP Theorem says that if you have a network partition, you cannot guarantee the system to be both fully available and fully consistent by the time the partition is finished. Intuitively this makes sense: you'll have to spend a nonzero amount of downtime to ensure access only when fully consistent.

This means you'll always have to consider balancing high availability and high consistency.
A single SQL database that serializes queries will always be highly consistent, but the thing could crash. On the other hand, a network of 1000 identical machines that allow read from any machine will have high availability but inconsistent values on reads from two different machines, even on the same timestamp.

#### ACID (SQL) vs BASE (NoSQL)
#### Columnar DBs and the Way Data is Laid Out

### What DELETE Actually Does: Tombstones and Compaction
DELETE (and setting TTL) does not immediately delete a row from a table. It simply marks it with a tombstone. Reads will skip the value. Periodically rows marked with a tombstone will be truly deleted from storage automatically. This process is called compaction.

Note that most tables have a tombstone limit. Once the limit is reached, Cassandra refuses any new queries on the table, and you have to wait until compaction. This is done to roughly ensure performance range for reads and prevent running out of memory. That is why best practice is not to delete too much, or to do a "soft" or fake delete by manually marking rows as "deleted". In the second case Cassandra's compaction is never invoked of course.

### Batch INSERT/SELECT - it's not what you think
#### Guarantees
Batch INSERT/SELECT ensure atomicity, but only single partition batches ensure isolation as well.
#### The lifecycle of a SELECT

## Git and Version Control
### Always Be Committing (ABC)
### Clone/Pull/Push
### Branches and Commit Numbers
### Pull Requests - The way any work gets done
### Revert
### Reset

## Lua 5.1
### Install (LuaRocks)
### REPL
### Variables
### Strings
#### Formatting and String Interpolation
#### Find and Replace
### Tables
#### Array = Table with 1
#### Iteration
### Functions
#### Higher Order Functions
### Penlight - The "Stdlib"
#### List
##### .map/.filter
##### List Comprehensions
#### Map
#### Set
#### Copy vs Deepcopy
### Busted and Testing
#### assert.are.equal
#### assert.are.same
### Step-through Debug using Mobdebug + Lua Plugin for IntelliJ

### Modules
#### Modules of Static Functions
#### "require"

### Object Oriented Programming
#### Hacky metatable stuff
#### Penlight's OOP
#### Ducktyping: "behaves like a"
#### Inheritance: "is a"
#### Composition: "has a"
#### Dependency Injection
#### Testing and OOP
##### Mocks and Stubs

#### Exercises
With teammates, do all the exercises in this [pdf](http://elementsofprogramminginterviews.com/sample/epilight_python_new.pdf) using Lua 5.1.

## Docker and OpenResty
### Install
### Postman/Curl
### newman - Automated Postman
### nginx.conf
### sites-available/default
### lua file structure
### "require"
### logger
### Fake StatsD

## Nginx
### Worker Model
### How a Worker handles multiple requests as non-blocking
Recall that the Nginx worker runs in a single thread and does not fork any new thread. So concurrency would be entirely due to context switches. OpenResty knows to swap to a new task when it hits a specific call to lua-socket. Upon doing so (usually this is a call to an external database or API), it knows it has to wait and it switches. Once the socket gets a response back to OpenResty it'll know to switch back. 

### lua code cache and Worker-local cache
nginx.conf has a setting boolean lua code cache. Basically when OpenResty starts, it runs all the modules. If lua code cache is on, it caches each environment after each of the modules have run. So if at module top-level you have a table holding something, it'll stay there in the environment when actual module methods are called. It can even be changed! You can see how this is a way to implement a simple worker-local cache.

Exercise: Implement a cached table in a module that lazily expires every minute.
Exercise: Implement a cache with Google Guava's Cache's semantics

## HTTP Requests
### HTTP Verbs
### JSON
### Response Codes
### Kinda RESTful API

## Authentication - Tokens, Tenant Credentials and Client Credentials
### HTTP Manager and the HTTP Context
### JWT (token format)
### Tenant vs Client Credentials

## OpenResty + Cassandra
### Lua-Cassandra
### Data Access Layer Pattern
### Timing Queries

Despite what your teammates may think about the cost of table creation, iteration and string/number arithmetic, time spent in handling an http request is overwhelmingly dominated by network calls to storage, by several orders of magnitude (look up standard estimate).

## Prometheus - Time Series for your monitoring
### Time Series
### Tags
### Queries
### Fake StatsD = Prometheus
#### Counters
#### Gauges

### Grafana
#### Make a chart

## Kibana - Search Engine for your logs
#### Note your VPC
#### Find your error logs

## Kafka
### Topics

## OpenResty + Kafka

## Creating Value
### Metrics

## Design Problems
### kinda RESTful APIs
### bit.ly
### Instagram
### Your own App (1 week)
