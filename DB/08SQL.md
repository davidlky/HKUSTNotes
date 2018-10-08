## Lecture 8, SQL
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
  - What happens on delete?
    - By default: disallow deletion
    - `cascade` - also delete all tuple that refers to the deleted entity (the referencer rows gets deleted)
    - `set default` gives it a default value
    - `set null`
  - What happens when a primary key id gets changed? Rejected
    - can specify on update action (to propagate, use `cascade`)
      - Oracle does **not** support this

  - `check` clause
    - add constraint for an attribute that can contain an *arbitrary predicate*
      - similar to a `where` clause
    - Checked during an update


### Views
- gives you a way to hide data from users
- `create view <name> as <query expression>`
- `drop view` to drop a view
- You can specify access to views
- some DB allow view to be stored and kept up to date if the relations change -> **Materialized Views**
- You can query them like a table
- insertion must add null to the ones that are non-existent
  - need to update original relations accordingly
- View is only updatable if *all* of the conditions are satisfied
  - `from` only has 1 relation
  - `select` only contains attribute name (no aggregate, distinct etc.)
  - any not listed can be set to `null` (cannot have `not null`)
  - does not have `group by` or `having`

`delete`
- delete 0 or more tuples
- only done if no constraints violated
- `where` can be as complex as `select` statements

`insert`
- must match order of relation
  - you can specify attributes
- insert from select statement is a thing

`having`
- can only use attributes(columns) that already exists in the relations
- 


### Exercises
- Exercise 1
```sql
select distinct title from Book natural join Author where lastName == 'Piper';
```

- Exercise 2
```sql
select lastName, firstName 
from (
  select authorId, lastName, firstName from Author natural join Book where subject='Art'
  intersect
  select authorId, lastName, firstName from Author natural join Book where subject='Business'
);

or

select lastName, firstName from 
  Author natural join Book 
  where 
    subject='Art' 
    and authorId in (
      select authorId, lastName, firstName from Author natural join Book where subject='Business'
    );
```
- Exercise 4
```sql
select lastName, firstName 
  from Author 
  natural join Book
  group by aid, lastName, firstName 
  having count(distinct subject) = 3

  can also do set! 
```
- Exercise 5
```sql
select cid, lastName, count (*) as numOrder 
  from Customer 
  natural join BookOrder 
  group by cid, lastName 
  having count(oid) > 10
```
- Exercise 6
```sql
with tmp (cid, totalQuantity) as 
  (select cid, sum(quantity) as totalQuantity from OrderDetails
    left join BookOrder 
    on OrderDetails.oid = BookOrder.cid 
    group by cid)
select cid, lastName, totalQuantity 
  from Customer 
  left join tmp
  on tmp.cid = Customer.cid 
  where totalQuantity = 
    (select max(totalQuantity) from tmp)
```