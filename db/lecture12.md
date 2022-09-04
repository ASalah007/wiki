# Processing Model

* Processing Model: defines how the system executes query plan
* there are three approaches:
    * Iterator Model (most common)
    * Materialization Model
    * vectorized/Batch Model
* each query plan implements a **Next** function

## Iterator Model

* when the next function is called it returns the next tuple to be processed
* the operator implements a loop that call **next** on its children, process the received tuples and then return the result to its parent
* the operator gets the data from its children tuple by tuple
* some operator requires more than one tuple to produce a result, they are called **pipeline breakers**
* joins, sub queries, order by -> are pipeline breakers

## Materialization Model

* in the materialization model the children produces all tuples at once (not tuple by tuple) like the iterator model
* better for OLTP but bad for OLAP  
* used in in-memory model not good for disk-based system

## Vectorized Model 

* for every next invocation the child produces a batch of tuples to the parent
* ideal for analytical queries
* better for disk-based system


# Plan Processing Direction

* Approach #1: Top-to-Bottom (most dbms implements this)
* Approach #2: Bottom-to-Top (hard to implement)

# Access Methods

* it is a way that the dbms can access data stored in a table
* three basic approaches:
    * sequential scan
    * Index scan 
    * Multi-Index / Bitmap Scan

# Sequential Scan

* it is the worst approach
* we can make some optimization to make sequential scan run faster:
    * **Zone Map** -> compute some metadata about each page (max val, min, avg, sum, count ... ) so you can decide 
      before fetching that page whether you are going to find a match for your query or not 
      usually good for olap but bad for oltp because you have to maintain it for every insert
    * **late materialization** -> good for column based dbms
    * **heap clustering** -> cluster the table based on an index, then if the query access the data based on the clustering 
      index then the dbms can jump directly to the pages it needs in a sequential manner (i/o is better for sequential scans)
      
    
# Index Scan

* the dbms picks an index to find the tuples that the query needs
* the trick in which index to use 

* when we do index scan that is not clustered we could end up doing random I/Os
* to solve this dbms uses **Index Scan Page Sorting**
* the idea of it is that first we do the index scan to find the pages that I need to fetch (but don't fetch) them 
  then sort the pages and then start fetching them one by one, as a result we will only need to fetch ever page 
  exactly once


# multi-index scan 
    
* if you have multiple index applies for the given query you can use multiple of them, 
  for example: 
  ```
  select * from students  
  where age < 30
    and dept = 'CS'
  ```
  and you have an index on age and dept, you can get all the tuples that match age < 30 
  using the first index and all the tuple that matches dept = 'CS' 
  and then return the intersection between the two tuples
* it is called bitmap scan in postgres





