### Lecture 9, Functional Dependency
`X->Y`, X is determinant set, Y is dependent set
  - At most one value of Y for any X
  - eg. a supervisor can only have 1 specialization, but many supervisor can specialize at the same thing
  - If Y is a subset of X, then it is trivial
  - We care about non-trivial ones
    - given as constraints
  - Concept of a Key in a table
    - `primary key -> all attr.`
  - Whole tuple -> **SuperKey**
  - Minimal set that determines entire tuple is **candidate key**
    - multiple, choose one as primary key

- Reflexivity, Augmentation and Transitivity are sound and complete

- Attribute Set
  - X<sup>+</sup>
  - include itself, and what it can determine
  - Algo: Check one level at a time
  - Can be used to check for super key


Canonical Order
- no redundancy, every other set would be the same
- left side of each functional dependency is unique
- find and replace, use union rule or find extraneous ones

## Lecture 10, cont.

Prime Attribute - part of any candidate key

Normalization: reduce redundancy, should be lossless
- basically decomposition

Normal form does not mean good design!

Design guidelines:
1. Clear Semantics for Attributes
  - Design so its easy to define a attribute's meaning, should be related
  - Easy to explain schema = good!
2. Minimize Use of Null Values
  - If not relatable, there will be a bunch of null value, which should be avoided
3. Minimize Redundancy
4. Lossless Decomp
  - The common attribute between the decomposed relations must be a superkey for R<sub>1</sub> or R<sub>2</sub>
5. Preserve Functional Dependencies
  - if any gets lost, then things are harder to enforce



First Normal Form: all attributes are atomic
- no multi valued or composite attributes

Second Normal Form: non-prime attributes are fully functionally dependent on every candidate key.
- subset of candidate key cannot determine a non-prime attribute
- basically, the all FD of X -> A, has to have A be part of candidate keys (or X is not a proper subset)

Third Normal Form: every non-prime attribute of R is nontransitively dependent on every candidate key of R
- basically, the all FD of X -> A, has to have A be part of candidate keys (or X is a superkey)


## Lecture 11, Part 3

- Every relationship schema is NF 1
- 2NF
  - For every nontrivial FD X→Y, either
    X is not a proper subset of a candidate key
    
    or 
    
    every attribute inY is prime. 
- 3NF
  - For every nontrivial FD X→Y, either
    X is a superkey
    
    or 
    
    every attribute in Y is prime. 
- 2NF vs 3NF
  - LHS of X -> Y allows parts of X to not be in candidate key

First Normal Form:  The information is stored in a relational table and each column contains atomic values, and there are not repeating groups of columns.

Second Normal Form: The table is in first normal form and all the columns depend on the table’s primary key.

Third Normal Form: the table is in second normal form and all of its columns are not transitively dependent on the primary key

BCNF - Boyce-Codd
- Basically, the LHS has to be a super-key, no extraneous on RHS
- No redundancy
- has to be 3NF first
- always a lossless conversion
- All FD may *not* bre preserved
- Checking F is sufficient (no need for F+), check if the super key is the same
  - for derived schemas, check F+

You can construct a 3NF form using the canonical cover and the candidate key

Sometimes updating BCNF is inefficient
- you can go back to 3NF, which cost more space
- you can use a materialized view, just less prone to errors
- 