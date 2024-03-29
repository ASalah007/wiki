# Query Execution


* sorting is useful in dbms world, but the sorting algorithm used should be mindful of random io

# External Merge Sort

* first we divide the data set into seperate **runs** and then sort them individually
* it has two phases:
    * **sorting** sort blocks of data that fits in memory and then write back the sorted block on disk
    * **merging** combine sorted sub-files into a single larger file

## 2-way external merge sort

# Aggregation

you have two implementation choices:
    1. sorting
    2. hashing (always better)

* when doing for example a **Distinct** operation you can make a hash table on the column you want 
  then while you are making the hash table if you hashed a value and found that it is already exists in the hash table 
  you discard it
* for other operation you might want to modify the old value with the new value
* after the query is finished we discard the hash table
* the hash approach is only good when it fits in memory, if i need to spill data to disk we will use the **external hashing aggregate**


## External hashing Aggregate

* Phase #1- Partition:
    * hash the tubles and the tuples that has the same hash key put it in the same partition
    * write them into disk when they are full
* Phase #2- Rehash:
    * for each partition hash again and start doing the aggregate
