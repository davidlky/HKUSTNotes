## Lecture 5, SQL
SQL is the most common relational query language

Based on set and relational algebra

`select * from relation where...`

does not remove duplicate by default
- (use `distinct`)
- `all` does nothing lmao

`where` clauses must be already defined in the from relations

`not between a AND b`

`from A, B` -> attribute must be specified, cartesian product

`A natural join B` -> will check duplicate attribute name if they equal

`union all, intersect all, minus(except) all`
- remove duplicates
- `(select *) minus (select *)`

Oracle: rename relation without `as` in `from`
- correlation name, alias

`like` -> string matching
- `%` any substring
- `_` single character
- `like '20\%%' escape '\'` -> specify escape character, all string starting with `20%`
- 2 single quote to include a single quote

![image](/DB/images/6.PNG)

`order by` default `asc`

Nested Subquery
- `where clause` -> must return appropriate value -> single or set of values
- relation can also return null
- `in, not in`
- `column > some` -> at least one
- `column > all` -> all
- `where exists` suquery can use the larger schema
  - returns if the subquery is not empty
- `where unique` return if the subquery has no duplicate


Aggregation
- apply the where first, then the aggregate function
- can specify group by
- attribute in select clause must also appear in group by, group by attributes do not need to be in the select clause
  - if there's aggregation in the select clause it is fine

will first perform join then group by then aggregation

Having
- allow conditions on groups
- refers to group after the formation, must involve aggregate function of attributes in select or group by clause

- where -> group -> having

`having count(*) > 1`

`from (select ....)` -> the middle from relation is a derived relation
- oracle does not allow for derived to be reused, hence using `with` can work
- `with Table (columns...) as (select...)`

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

```sql
create table (
  ...
  primary key (attr1, attr2),
  foreign key (attr) references Table on delete ____ on update _____,
  check (______)
)
```

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


```sql 
update Account
set balance= case
  when balance<=10000 then balance*1.05
  else balance*1.06
end;
```


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