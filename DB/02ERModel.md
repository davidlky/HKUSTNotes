## Entity-Relationship Model
- Logical Level design - structure of database
- 3 basic concepts
  - entities
  - attributes
  - relationships

LMAO: Entity (type) has a bunch of entities instances (entity set)
- entity: Employee
  - entity instance: David, Jeff, etc.
  - ^all in the entity set
  - (wtf)

Entity has attributes, each having values

![image](DB/images/1.png)

![image](DB/images/2.png)

Generalization
- bottom up, super class at the top
- can also be top down (attribute defined)
- discriminator: attribute of enumeration type (property that is being abstracted)
  - determined by predicate (the discriminator attribute)

Inheritance
- reduce redundancy, promote reuse, simply modification
- no more than 2-3 levels

Can have multiple inheritance

Relationship(type) -> description of a set of relationship with common properties
- instances of relationship (John does E-commerce, etc.)

Unary and Binary degree of entity type (ignore ternary)

Role Name useful for Unary Relationships!!

### Part 2

Constraint: logical restriction -> true or false
  - expect to be always true, enforcable
- add more meaning

Constraint: Domain
- restricts an attribute to only have certain values

Constraint: Key
- if can uniquely identify an entity instance, then it is a key
- candidate key: minimal set of attribute that help uniquely identify instance
- one candidate key -> primary key
  - enforced by DBMS
  - if candidate key is a set -> composite key

Strong Entity: has a primary key

Weak Entity: does not have a primary key (associated with a strong entity - identifying entity)
- discriminator helping to differentiate (along with the identifying relationship)


Surrogate Key - new attribute added to be the primary key of entity
- invisible to user
- make weak entity strong

Coverage
- Disjointness:
  - overlapping (o) -> super-class can relate to more than one subclass
  - disjoint (d) -> one or the other but not both
- Completeness
  - partial (single line) the super class can exist on its own (non-abstract class)
  - total (double line) the super class is abstract.

![img](DB/images/3.png)
- if min-card = 0 -> partial participation, > 0 -> total
- max-card -> cardinality constraint: 1->1, 1->n, n->1, n->m

Exclusion
- one or the other but not both! (linked by a --(+)--)

Choosing between entity and attribute:
- entity: severy properties can be associated
- attribute -> concept has no property of interest
- relationship: not a distinct application, no interest

Note: if the same relationship instance need to appear 2 times -> switch to Entity instead of relationship