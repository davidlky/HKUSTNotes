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
