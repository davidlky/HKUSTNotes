## L19, Query Optimization
- selecting the most efficient query amongst all strategies

Evaluation Plan: exactly what algorithm is used for each operation and define how execution is coordinated

Cost Based Optimization
- generate logical equiv plans, cost compare, use the min expected cost
- based on stats on relations, intermediary and cost for algorithm

Heuristic Optimization
- perform cheapest first, maximize the use of indexes
- remove unused attributes early

Transformation of Relational Expressions
- two relational algebra expressions are equiv if they generate the same set of tuples
    - only care about tuples, order doesn't matter
    - assume the database has no integrity violations
- 