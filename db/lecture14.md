# Query Planning and Optimization

there are two approaches in query optimization:
* Rules/heuristics: rewrite the query but remove ineffecient things, you dont need to look at the data only the catalog
* Cost-Based Search: use model to estimate the cost of exec plan, evaluate multible plans and then choose the best

# Architecture

Application →  SQL Rewriter(optional) →  SQL Parser →  Binder → Tree Rewriter(optional) →  Optimizer →  Execute plan

# SQL Rewriter

* two relational algerbra expressions are equivalent if they produce the same set of tuples

* Optimization:
    * **predicate pushdown**:
      for example if you have a query that joins two tables then filter them based on some predicate 
      it is better to do the filtering first then joining
    * **Reorder Predicates**:
      do the more selective predicate first
    * **break complex predicate and push down**
    * **Projection pushdown**: 
      if the query only needs one column then removing the other columns as early as possible in the query plan
    * **Impossible predicate**:
      select * from A where 1=0; -> the optimizer will see it is impossible for a tuple to match so it will skip the scan
      and produce empty table
