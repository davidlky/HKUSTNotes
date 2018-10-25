## L5, Relational Algebra

Query Language - Retrieval of data from DB
- Not a Programming Language
- Not Turing Complete (recent SQL are)
- Not for complex calculation

Formal Relational Query Language
- Relational Algebra: Procedural (step-by-step) - describe how to compute query result
    - Our focus
- Relational Calculus: Non-procedural (declarative)
    - Describe what is wanted: not how to compute

Relational Algebra
- operands are relations/variable
- operations are common, basic manipulation
- closed -> takes in and output relations

![image](/DB/images/5.PNG)

Selection

$\sigma_{company='Boeing'}(Table)$

Projection - only keep certain column

$\pi_{company}(Table)$

Union, Set difference and Intersection

Cartesian Product (every combination)

Renaming

$\rho_{newName(attribute, att2)}(Table)$

Joins

$R_1 JOIN_{condition} R_2 = \sigma_{condition}(R_1 \times R_2)$

- natural join, `condition` join, equijoin

outer join is jst the join symbol with `2 lines` at the end of the outer join -> left outer = left side

