---
layout: post
title: Dynamo DB
published: true
---

## Purpose
Notes for the Dynamo DB session acloud.guru

### Breif History of Data Storage
- Basic intention of Data Storage is share intentions, ideas and facts
- Should be able to store them and retrive them
- Velocity of reads and writes dependent on usecases and influences decision
- Internet changed the information volumes and brought urgent need to scale up reads and writes

### RDBMS Fundamentals
- Relation Databasae Management System (RDBMS) consists of the following:
	- Server Side: Physical Server -> Operating System -> RDBMS System(Oracle, SQL Server, My Sql etc.,)
    - Client Side: Physical Server -> Operating System -> Proprietery Client or Applications using Drivers like JDBC or ODBC
    - Languege of communication -> Structured Query Languege (SQL)
- RDBMS building blocks:
 	- Tables 
    	- is a collection of rows with defined columns 
    	- can have relationship defined between them (One to One, One to Many, Many to Many)
    	- can have constraints defined on them (Constraints: Primary Key/Forigen Key etc.,)
    	- can have search patterns defined on them (Index)
    	- have to be modeled before usage (Model = Schema)
        - every row has the same schema, no exception
        - every column has a predefined types
    - Keys
        - Candidate Key: any column that uniquely defines the row
        - Primary Key: any designated Candidate Key
        - Composite Key: group of keys that if used together would act as a candidate key
        - Foreign Key: defines relationships between tables.
    - SQL
        - Data Defination Language (DDL)
        - Data Manipulation Language (DML)
        - **Data Control Language (DCL)** More should be learnt on this
    - JOIN
        - can be used to get information from multiple tables
        - _**gives the flexibility to ask questions that were never considered while modelling**_
        - leverages the formal relationship which was provided while modelling to join data accross tables
        - for many to many relationships a bridge table with composite key has to be used
        - if there is no formal relationships then a costly table join will occur
    - Architectural Parts of RDBMS Server
        - Query Parser: 
            - Takes a query from client and breaks the same in logical blocks
            - Builts a sequence tree
        - Query Optimizer: 
            - Takes Sequence tree and builds a optimized execution plan
        - Relational Engine:
            - Executes the execution plan and delegates the data opertions to storage engine
        - Storage Engine:
            - Reads data
            - Writes data
            - Caches data
            - Organizes the data in a way that it can be efficiently retrieved
        - Data by itself can be CPU cache/RAM/HDD/SDD
    - Patterns to scale RDBMS
        - Increase the RAM/CPU
        - Change the Magentic HD to SSD
        - Implement the Write Master/Read Slave(s) architecture
            - This would increase the read performance not the write
            - We might be giving up slighty on the consistency as the data replication might have latency
        - Implement Sharding
            - Rows in the tables would be sharded across the cluster on the basis of some hashing algorithm
            - Choises around the hashing algorithm and the columns invovled determines if there is fair distribuition of work across the cluster
            - Makes the join across tables might become very expensive if the data doesnot recide in the same shard
            - If this is required the choise RDBMS vs non RDBMS (NO-SQL) should be seriously thought upon
