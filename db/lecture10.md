# Query Execution


* sorting is useful in dbms world, but the sorting algorithm used should be mindful of random io

# External Merge Sort

* first we divide the data set into seperate **runs** and then sort them individually
* it has two phases:
    * **sorting** sort blocks of data that fits in memory and then write back the sorted block on disk
    * **merging** combine sorted sub-files into a single larger file

## 2-way external merge sort

