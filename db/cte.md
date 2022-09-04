# Common Table Expression

* A cte works as if it were a view that exists for the duration of a single statement
* there are two types of cte:
    1. ordinary cte
    2. recursive cte

## Recursive CTE

* the recursive cte must be **compound** select statement. that is to say, the body of the cte must consists of two or more 
  select statements connected with union, union all, except, intersect
* one of the select statements must be recursive
* one of the select statements must be non-recursive
* the non-recursive select statements must be before the recursive ones
* 
