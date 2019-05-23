# Bootcamp - Server Team
Notes for a Server Team Bootcamp (Cassandra and lua OpenResty)

## Cassandra
### Install

### Tables - Logical Model
#### Partition Keys

#### Clustering Keys

#### Queries
##### INSERT and UPDATE
##### SELECT
##### DELETE

#### Full Table Scans

### Nodes - Physical Model
#### Consistency
#### Any vs Quorum vs All
#### CAP Theorem
#### ACID (SQL) vs BASE (NoSQL)
#### Columnar DBs and the Way Data is Laid Out

### What DELETE Actually Does: Tombstones and Compaction

### Batch INSERT/SELECT - it's not what you think
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
### Step-through Debug

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
### lua code cache and Worker-local cache

## HTTP Requests
### HTTP Verbs
### JSON
### Response Codes
### Kinda RESTful API

## OpenResty + Cassandra
### Lua-Cassandra
### Data Access Layer Pattern
### Timing Queries

## Prometheus
### Time Series
### Tags
### Queries
### Fake StatsD = Prometheus
#### Counters
#### Gauges

### Grafana
#### Make a chart

### Kibana
#### Note your VPC
#### Find your error logs

### Kafka
#### Topics

### OpenResty + Kafka

## Creating Value
### Metrics

## Design Problems
### kinda RESTful APIs
### bit.ly
### Instagram
### Your own App (1 week)
