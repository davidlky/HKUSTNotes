## Lecture 7, SQL
### DDL
- Data Definition Language
- Allows for specifying
  - Schema
  - type of values
  - User defined types and domains
  - Integrity Constraints
  - Physical storage structure
  - Indices
  - Security + Auth

Creating Relations: use create table, need to specify **domain type**

`alter table` can be used to modify attributes (`add`, `drop`, `modify`)

`drop table` delete all info, data and schema

### Integrity Constraints
- These enforces valid values for attributes
- They *test* value and queries to makes ure the make sense
- Aside from basic type checking you can enforce more
- `check` will specify a predicate
- `primary key` also enforces as not null, `unique` allows for null

- can have many *candidate keys*, one of which is chosen as primary key

- Foreign key constraints
  - must be primary key of referenced relation
  - enforces *referential integrity*

- 