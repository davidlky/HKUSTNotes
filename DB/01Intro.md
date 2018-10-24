## Intro

Database: collection of related data
- represent part of ral world, have inherent meaning
- specific purpose

DBMS: Database Management System
- defining, storing, manipulating, sharing, protecting
- convenient and efficient

OG: File Processing
- redundancy, hard to access, no data isolation, integrity issues, security and concurrency issues

Database Processing
- Integrate org data
- Separate Meta Data
- Support Multiple View
- Controls Definition and Access *Centrally*

Levels of Abstraction
- separation of application program from data they access
- DBMS provides various level so you don't have to care about how data is stored and indexed and etc.
- View level (different access levels) -> Logical level (DB model) -> Physical Level

Schema -> overall design of a database
- changes infrequently
- schema at each level
- instance -> actual content at point in time

Data Independence
- modify a schema def in one level without affecting another level

Data Models
- Data Structure Types => properties, relationships and semantics
- Integrity Constraints => constraints
- Operations => RIUD (CRUD)

- logical organization and restrictions

Entity Relationship Model
- entities and relationships in between them

Relational Model
- tables (rows and columns)

DDL -> data definition language
- access/manipulate data
- procedural
  - specifies what and how to get data
-  non-procedural
  - only what data is needed
  - **SQL** Structured Query Language

Query Processing
- translate nonprocedural queries and updates into efficient disk-level ops
  - DDL interpreter
  - DML compiler
  - Query evaluation engine

Storage Management
- interface between low-level data and app program + queries within system
- auth/integrity, transaction, file and buffer management

Transaction Management
- transaction: collection of operations that perform a single logical function in DB app
- Transaction Management Component
  - ensure consistency state despite failures
- concurrency-control
  - ensure consistency through concurrency


