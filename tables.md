# Tables





### CSV file

Table files are provided in a single CSV file. Each row in `tables.csv` represents a new table file. 
The CSV file consist of 7 columns: 

| Column  | Type    | Description                 |
| ------- | ------- | --------------------------- |
| Name    | string  | Table file name             |
| Size    | integer | Table file size             |
| Bits    | byte    | Table file entry size       |
| SHA256  | string  | Content's SHA256            |
| SHA1    | string  | Content's SHA1              |
| MD5     | string  | Content's MD5               |
| Content | string  | Base64 encoded file content |

The *Size*, *SHA256*, *SHA1*, *MD5* are provided to validate the new table file created from decoded *Content* and saved as *Name* .  
The *Bits* column is informational and provides table entry size in bits.



### Table file

The table is a set of values represented by a fixed size integer numbers. The integer numbers are stored one after the other.  The table entry is represented by a position in the table and the value stored under that position. The table holds a number of entry chains. 


#### Table layout

The example table demonstrate table file structure.  

| Entry |  01  |  02  |  03  |  04  |  05  |  06  |  07  |  08  |  09  |  10  |  11  |  12  |  13  |  14  |  15  |  16  |  17  |  18  |  19  |  20  |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| Value |  TM  |  TM  |  04  |  CE  |  06  |  07  |  08  |  09  |  10  |  EC  |  12  |  13  |  LE  |  15  |  11  |  EC  |  16  |  17  |  00  |  EC  |



The table file consist of 

* Table marker (TM)

* Empty entries (00)

* Entry chains with end of chain markers (EC)

  

#### Table marker

The first two entries in the table file are always reserved for table marker. This marker is a signature of the table file.



#### Empty entry

The table may contain one or more empty entries. The entry is empty when the value is set to zero. Empty entries can be found anywhere in the table. 



#### Entry chains

The chain can be composed of one or more entries. The entry value points to another entry position and so on until the value indicates end of chain (EC).

The example table above consist of 5 chains: 




###### 03, 04

| Entry |  01  |  02  |  03  |  04  |  05  |  06  |  07  |  08  |  09  |  10  |  11  |  12  |  13  |  14  |  15  |  16  |  17  |  18  |  19  |  20  |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| Value |      |      |  04  |  EC  |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |

###### 05, 08, 09, 06, 07, 10

| Entry |  01  |  02  |  03  |  04  |  05  |  06  |  07  |  08  |  09  |  10  |  11  |  12  |  13  |  14  |  15  |  16  |  17  |  18  |  19  |  20  |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| Value |      |      |      |      |  08  |  07  |  10  |  09  |  06  |  EC  |      |      |      |      |      |      |      |      |      |      |

###### 14, 15, 11, 12, 13

| Entry |  01  |  02  |  03  |  04  |  05  |  06  |  07  |  08  |  09  |  10  |  11  |  12  |  13  |  14  |  15  |  16  |  17  |  18  |  19  |  20  |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| Value |      |      |      |      |      |      |      |      |      |      |  12  |  13  |  EC  |  15  |  11  |      |      |      |      |      |


###### 18, 17, 16

| Entry |  01  |  02  |  03  |  04  |  05  |  06  |  07  |  08  |  09  |  10  |  11  |  12  |  13  |  14  |  15  |  16  |  17  |  18  |  19  |  20  |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| Value |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |  EC  |  16  |  17  |      |      |


###### 20

| Entry |  01  |  02  |  03  |  04  |  05  |  06  |  07  |  08  |  09  |  10  |  11  |  12  |  13  |  14  |  15  |  16  |  17  |  18  |  19  |  20  |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| Value |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |  EC  |



