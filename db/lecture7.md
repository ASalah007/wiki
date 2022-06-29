# Indexes 

* there is a trade-off on the number of Indexes per database:
    * storage overhead
    * maintenance overhead -> if you updated the table the index table must be updated
* B Tree is a term used to describe the following data structures:
    1. B Tree
    2. B+ Tree
    3. B* Tree
    4. Blink Tree

## B+ Tree
    
* It is a self balancing tree data structure that keep data **sorted** allow **searches, sequential access,**
**insertion and deletions in O(log n)**

* when you reach a leaf node you can do a sequential scan on the leaf nodes without going to back up

* it is M-way search tree -> which means that a node can have up to M children
* it is perfectly balanced tree -> the distance between the any leaf node to the root is exactly log n
* every node other than the node is at least half full -> **M/2-1<= #keys <= M-1**
* every inner node with k keys has k+1 non-null children
* the values are **only** in the leaf nodes 

* every node is an array of key value pair
* in inner nodes the value is pointer to a child
* in leaf nodes the value are:
    * approach 1: Record Ids -> a pointer to the location of the tuple that the index corresponds to 
    * approach 2: Tuple data -> the actual contents of the tuple is stored in the leaf node and secondary indexes 
      have to store the record id as their values

### B+ Insert

* find the correct leaf node L
* put data entry into L in sorted order
* if L has enough space done!
* else split L keys into L and a new node M:
    * redistribute entries evenly
    * insert index entry pointing to M into parent of L 
      
### B+ Delete

* start at the root, find leaf L where the entry belong
* Remove the entry
* if L is at least half full done!
* if L has only M/2 -1 entries:
    * try to redistribute borrowing from sibling 
    * if redistribute failed merge
* if merge occurred must delete entry (pointing to L or sibling) from parent of L  


## Clustered index 

* the table heap is unordered so you can insert tuples in any table in any page without any order (no sorting happens)
so when you ask for a table sorted in sql the dbms sorts the data after it gets it from the disk

* sometimes you want the data to be always sorted(physically on disk) in certain way. 
so when you define a cluster index on the table when it is created the dbms will guarantee
that the physical layout of tuples on pages will match the order in the index

* mysql always use clustered index on the primary key and if you didn't provide a primary key it will
create one but it is hidden from you 

* in postgres there is clustered index but it will not maintain the order, that is it will just sort it one time and that is it 

* the dbms can use a B+ tree index if the query **provides any of the attributes of the search key**
  for example: index on <a,b,c>
  → supported: (a=3, c=4) so in this case you can use the index if you provide only the attributes of the prefix and postfix 
  and not the middle (most dbms) provide this one
  → supported: (b=3) you can only also provide the middle one (only few supports this one)


* some dbms do not always merge nodes when they are half full
* delaying merge operation may reduce the amount of reorganization
* it may also be better to just let underflows to exist and then periodically rebuild entire tree 
  enterprise business in weekends shut down the database and then rebuild the indexes
  
## variable length keys

* approach #1: pointers (super slow no one uses it)
  store a pointer to the key in the nodes 

* approach #2: variable length node (no on uses this also)

* approach #3: padding (postgres uses this but its a trade off we are wasting space to have fixed length nodes)
  always pad the key to be the max length of the key type
  for example if its varchar(13) and the key is 10 chars then we will pad it with spaces until it is 13 chars

* approach #4 key map/ indirection
  embed an array of pointers that points to a location in the node itself not another random place in memory

## non unique indexes (on the node level)

* approach #1: duplicate keys
* approach #2: value lists -> store each key only once and maintain a linked list of unique values

## intra node searches 

* linear search 
* binary search 
* interpolation


# Optimization

* prefix compressions 
  for example if you to store run running runway -> you can store them as prefix = run and ( ,ning, way) 
* suffix truncation -> if the keys looks like that → abcdef, lmnobq you can store them as abc, lmn 
  and you still can determine what key is less than which 
* bulk insert -> create the index table bottom up is faster 

* pointer swizzling




 
