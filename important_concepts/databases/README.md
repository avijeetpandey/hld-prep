# Database management system

## What is RDBMS ?
RDBMS stands for relation database management system which basically stores data in the form of rows and columns and data across multiple tables are linked via Primary and Foreign keys , preventing storing duplicate data. 
- These systems are ACID compliant
- Have a structured way of accessing / ingesting data ( SQL )
- But as they are designed to scale vertically , often when tables are biggers complex joins slows down the DB

## Types of database languages
There are 5 types of database languages present and they are 
- DDL ( data definition language ) [CREATE, ALTER , DROP]
- DML ( data manipulation language ) [INSERT, UPDATE, DELETE]
- DQL ( data query language ) [SELECT]
- DCL ( data control language ) [GRANT , REVOKE ]
- TCL (transaction control language ) [COMMIT, ROLLBACK, SAVEPOINT]

## ACID Properties
- Atomic - the whole operation either succeeds or fails
- Consitent - data should be in consisten form
- Isolation - one transaction does not know about the other transactions
- Durable - data should persist

## Keys in DBMS
- Primary key
- Foriegn key
- Candiate key ( potential primary key )
- Composite key ( combination of multi primary keys )

## SQL commands and its types

## Nested queries in SQL

## What is a JOIN and types of JOINS

## Tier2 and Tier 3 architectures

## Types of locks in DB

# SQL Related concepts

## Constraints in SQL

## Foreign Key

## Primary Key

## What is a cursor?

## Alias in SQL

## OLTP

## OLAP

## What is a collation

## Bin logs in DB

## Replicas

## How to prevent dead locks in databases transactions?

## Elasticsearch and its scaling

## Sharding