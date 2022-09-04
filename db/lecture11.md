# Join Algorithms 

## Nested Loop Join
if you have two table R and S
```
for each r in R:
    for each s in S:
        emit, if s and r match
```

This is stupid since for each tuple in the outer table we will fetch the pages in the inner table
the I/O cost of this algorithm is **M + (m.N)** 
M -> the number of pages of in the outer table
m -> the number of tuples in the inner table
N -> the number of pages in the inner table 

We can speed this algorithm a bit by making the smaller table as the outer table to decrease 'm'

## Block Nested for join

```
foreach block br in R:
    foreach block bs in S:
        foreach tuple r in br:
            fro each tuple s in bs:
                emit, if r and s match
```
cost -> M + (M.N)

## Index Nested loop join 

```
foreach tuple r in R:
    foreach tuple s in Index(ri = si):
        emit, if r ans s match
```
cost -> M + (m.C) where c is a constant

## sort-merge

* Phase #1: Sort (we can use external merge sort)
* Phase #2: Merge

approx algorithm
```
sort R and S on join keys
cursorR <- Rsorted, cursorS <- Ssorted
while cursorR and cursorS :
    if cursorR > cursorS :
        increment cursorS
    if cursorR < cursorS :
        increment cursorR
    elif cursorR and cursorS match:
        emit, increment cursorS
```
we might need to backtrack and keep track of the start index of the last value seen in the inner table

* Sort Cost(R): 2M.(log M / log B)
* Sort Cost(S): 2N.(log N / log B)
* merge Cost: (M+N)

* total cost = merge cost + sort cost
    
* the worst case scenario if the two tables have the same values for all attributes

## Hash join

* Phase #1: build 
  scan the outer table hash it and populate the hash table
* Phase #2: probe 
  scan the inner table and use the same hash function to see if we have a match
   

If the hash table is so big that it doesn't fit in memory, then we will end up of doing so many random i/o
it is better to use **grace hash join**

Cost -> 3(M.N)




