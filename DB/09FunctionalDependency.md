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