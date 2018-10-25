## L4, Relational Model

Represent data as a collection of tables

Defined by set of relation schemas
- table show instances of relation schema

Tuple: ordered sequence (instance)

Relation Instance: relation, tme-varying finite set of tuples
- Degree: number of attributes
- Cardinality: number of tuples

Cartesian Product: relation is a subset of the cartesian product of domain of values
- every possible combination

Attribute values are atomic!! Multivalued/composite are not allowed

null: used for N/A, missing or not known data

Keys
- Superkey: set of attributes that can identify a unique tuple!
- mandatory candidate key for relational model
- not required for relational DBMS

- Candidate key: minimal set of attributes that is a superkey
- Primary key: one of the candidate key (at most one chosen)

Relational Attributes has Super keys has Candidate keys as Primary *key*

Entity integrity constraint: if X is primary key -> X cannot have null values (none of the attributes can have null value)

Referential integrity constraint: Foreign key can either equal to original primary key or just be null

### E-R to Relational
Referential Integrity Actions
- total participation: `on delete cascade`
- partial participation: `on delete set null`

Reducing Generalization/Specialization
1. Create subclass entity, have a K for super class, and acts as FK for subclasses, on delete cascade
2. Reduce only subclasses -> create schema with field from super class (total, disjoint only!)

Reduce composite/multi-valued
- Create a single attribute by concatenating components
- Create a separate attribute for each one
- Multivalued: create new schema with FK to orig class
    - `on delete cascade`

Reduce Strong/Weak Entities
- For weak, add a FK and a discriminator, `on delete cascade`

Relationships
- 1:1 trivial, 1:N use the PK of n side
- N:M, need to create union of primary key
- Can also just combine schema for 1:1 and 1:N

Reduce Exclusion
- add a `check` to make sure that only one of the 2 FK is set
- Or just make sure down stream have unique id

