# F001


* Provide solution as console application
* You are allowed to use nuggets to handle command line parsing or logging



1. Create three table files which content is stored in each row of the provided CSV file.
2. Find all the chains and provide first entry index in text file.  
3.   



The task is divided into three stages



Three features

* decode
* find
* read




### Stage 1 
###### Decode and Validate

`F001.exe decode --csv tables.csv`


### Stage 2
###### Parse and Search



`F001.exe find --input table.bin --output entries.lst`

* Detect table entry size - 12 bit, 16 bit or 32 bit
* 



### Stage 3
###### Read 



`F001.exe read --input entries.lst --output chains.txt`

* Create table reader
* The reader must read  table files 