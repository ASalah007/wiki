# Chapter 7

* before the command is passed to the program/command in the shell 
  the shell perform **expansion** to it for example the wildcard '*' 
  will be expanded to the names of files/folders in the current folders 
  so you can do something like this -> echo /usr/*/lib

* **Integer Arithmatic Expansion:** `echo $(( 2+5 ))` -> 7
  
* **Brace Expansion**:  
    `echo ahmed{1,2,3} -> ahmed1 ahmed2 ahmed3`  
    `echo version{1..5} -> version1 version2 ...`

* **Variable Expansion**: `echo $USER`
* **Command Expansion**: `echo $(ls)` or echo \`ls\`

if you do not want expansion you can escape it with quoting

* **double quoting**: all expansions are suprressed except for *parameter*, *arithmatic* and *command* expansion 
  for example: echo `"this is     a cal $(cal)"`
* **single quoting**: all expansions are suppressed 
