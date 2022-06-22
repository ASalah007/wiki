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




 
