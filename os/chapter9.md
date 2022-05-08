# Permissions

* Access Rights to files/folders are defined in terms of: 
  - read access
  - write access
  - execution access

* when you execute a `ls -l` command you can see the **file attribut**
* the first character represents the file type 
  - - -> regular file
  - d -> directory
  - l -> symbolic link
  - and more ...

* the other 9 character are called **file mode**: rwx rwx rwx 
  the first three for the *owner* then the *group* then the *world*
* to change the mode of a file `chmod {oct_num}{oct_num}{oct_num} {file_name}` 
* you can also use the symbolic notaion with chmod  
  e.g: `chmod u+x,go-r,g=wx {file_name}`
 
* by default when you create a new file it is given the permission --- rw- rw- rw- 
  then some values get disabled according to the mask(by default it is 0002)
  --- rw- rw- rw-  
  000 000 000 010  
  --- rw- rw- r--  
  
  
  
