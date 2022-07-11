# Data Storage Architecture

    
* HDD and SSD are usually block/page structured 
* most dbms uses operating systems file as intermediate step to store records
* for cpu to access data it must be in memory, in many cases the databse is larger than the main memory 
  so the dbms takes a place in memory (buffer) to fetch the data from an to the desk.
  
# File Organization

* A **database** is mapped into files that are maintained by the operating system
* A **file** is logically partitioned into **fixed-length** storage units called blocks/pages (4 to 8 KB)
* A **Block** may contain several records

## Fixed Sized Records

* when storing records in the blocks we first give each attribute the maximum size that it could take 
  for example -> if we have a varchar(25) att. then we give it 25 Bytes of space
* then give each record the total size of its attribtues 
  for example if we have a relation that looks like this rel(A varchar(3), B varchar(23), C numeric(8,2))
  then each record is 34 Byte
* after that we store the records in a linear fashion in the block, the first 34 byte contains the first record and 
  the second 34 bytes contain the second record and so on...


* The problems of such technique:
    * the block size is not multiple of 34 -> some space are left empty
    * it is difficult to delete a record from this structure 
      
      to solve this problem there are multiple solution:
      1. shift all records to fill the empty space
      2. only move the last record to fill the empty space
      3. mark the empty space and fill it with the next insert
    
    * the third solution is preferable but it has some problems 
      **problem**: how to know that a block has some empty space in it (we don't want to linearly search it every time)
    
      **Solution**: in the first bytes of the block we store the location(address/offset) of the first record whose contents are deleted 
      and in this first record we store the address location of the second available record, so we formed a linked list of the free spaces 
      inside of the record, we call this list **the free list**.

## Variable Length Record

there are two main problems that any technique that implements VLR must solve: 

1. How to represent a single record in such a way that individual attributes can be extracted easily 
   (for example how to know the start and the end of each attribute in a given record)
2. How to store a variable length record within a block, such that records in a block can be extracted easily

* for the first problem, we split the each record into two parts:
    1. initial part with **fixed Length** information, and its structure is the same for all the records
    2. the content of the variable length attributes
    
    * for example if the record has a varchar attribute, then in the initial part we store the (offset, length) of the varchar
      offset: the place of the value in the record, length: the length of the value
      
* for the second problem we use the **slotted-page** technique


# Organization of Records in Files

we have discussed how records are stored in pages, now we will discuss how pages are stored in files.

## Heap File Organization

* a file represents a relation, and a record can be stored in anywhere in the file(anywhere -> block -> each block keep track of its records as discussed above)
* when inserting a new record one option is to insert it at the end of the file
* if a record gets deleted it creates a free space and the dbms must fill this free space of keep track of it 
  so that it can insert new records inside of it 
* one way of keeping track of free space is **free-space map**
* **free-space map** is an array that stores the amount of free space inside each block
 

# Database Dictionary

* the database dictionary stores the schemas and other metadata about the relations
* 
  
















mm
