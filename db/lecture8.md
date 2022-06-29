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
