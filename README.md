# F001


The task is divided into three parts

* Decode and Validate
* Parse and Search 
* Read and Iterate



### Decode 

`F001.exe decode --csv tables.csv`




### Parse


`F001.exe parse --input table.bin --output entries.lst`

* Detect table entry size - 12 bit, 16 bit or 32 bit
* 







### Read 


`F001.exe read --input entries.lst --output chains.txt`

* Create table reader
* The reader must read  table files 