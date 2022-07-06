# Duplicate keys

* approach #1: append record id 
  append the record id of the tuple which is unique at the back of the key 
  se we end up with unique key every time and then use partial key to traverse the B+ tree
* approach #2: overflow leaf node 
  allow leaf nodes to spill into overflow nodes that contain the duplicate key


* COPY emails(email) from 'path/file' delimiter ',' CSV;
  this copy into the column email the values inside the file 


* Create index idx_emails_hash on emails using hash (email); 
  in most systems when you create an index it will create a b+ index 
  in postgres you can force it to use hash table by typint **using hash**
  
  
* CLUSTER emails USING idx_emails_tree; 
  this tells postgres to resort the entire table based on the sort ordering to find by this index

# implicit indexes
* most dbms automatically create an index to enforce integrity constraints but not referential constraints
* whenever you create an integerity constraint the dbms automatically create an index for you (like primary keys, unique constraints)
* if it didn't create that index, whenever i insert a new tuple inside a table it would scan the whole table to check that
  this primary key doesn't exist in the table
* if you tried to make a foreign key that references a column that doesn't have an index on it, it will throw an error  

# partial indexes

* instead of creating an index on the whole table you can create an index on part of the data, 
  for example -> `create an index on foo(a,b) where c = 'wutang';` 
  in this example the querey that has the condition c = 'wutang' in it, is the one which can use this querey
  like -> `select b from foo where c = 'wutang';`
  
# covering index

* if all the fields needed by a query are available in the index and the dbms doesn't need to look up the table 
  like the above querey where it needs b which is part of the key of the index and it is stored in the index

* another example -> `create index idx_foo on foo(a,b)`, `select b from foo where a = '123'`

in postgres it is called index-only scan and the index must satisfy two conditions in order to use it
1. the index type must support index-only scan (btree always do)
2. the query must references only the columns stored in the index 
   
* you can include some extra columns in the index in order to achieve covering indexes on more queries like this 
  `create an index on foo(a,b) include(c)`

* these included columns are not part of the key and they are included only in the leaf node
* but this inclusion support is rare in dbms

# Functional/Expression Indexes

`select * from users where extract(dow from login) = 2;` 

in the abover query the following index won't work -> `create index on users(login)`
this will work -> `create an index on users (extract(dow from login))` 


# TRIE

you can use trie instead of Btree,
it will be faster for point queries but slower for scan queries

the **span** of a trie level is the number of bits that each partial key/digit represents

# Inverted indexes / full-text search index 

inverted indexes stores a mapping of words to records that contain these words

with inverted indexes you can speed up these queries:
    * phrase searches: find records that contain a list of words in the given order
    * proximity search: find records where two words occur within n words of each other 
    * wild card searches: find records that contain words that match some pattern (regexp)
