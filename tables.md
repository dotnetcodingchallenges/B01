# Tables

Tables are provided as a single comma delimited file.  Each row represents a table file. 
The file name is `tables.csv`



### CSV file format

The `tables.csv` is a standard CSV file format. 

| Column  | Type    | Description                 |
| ------- | ------- | --------------------------- |
| Name    | string  | Table file name             |
| Size    | integer | Table file size             |
| Bits    | byte    | Table file entry size       |
| SHA256  | string  | Content's SHA256            |
| SHA1    | string  | Content's SHA1              |
| MD5     | string  | Content's MD5               |
| Content | string  | Base64 encoded file content |









### Table file format

The table is a set of entries represented by integer numbers.  The entry is represented by entry position and the value. 



##### Example table

| Entry |  01  |  02  |  03  |  04  |  05  |  06  |  07  |  08  |  09  |  10  |  11  |  12  |  13  |  14  |  15  |  16  |  17  |  18  |  19  |  20  |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| Value |  TM  |  TM  |  04  |  CE  |  06  |  07  |  08  |  09  |  10  |  EC  |  12  |  13  |  LE  |  15  |  11  |  EC  |  16  |  17  |  00  |  EC  |

The example table consist of 20 entries. The entries includes 

* Table marker (TM)  

* Empty entry

* Chain with end of chain (EC) marker

  

  

#### Table marker

The first two entries in the table consist of table marker. 



#### Empty entry

The table may contain one or more empty entries. The entry is empty when the value is set to zero.



#### Entry chains

The chain can be composed of one or more entries. The example table consist of 5 chains: 


###### 03, 04

| Entry |  01  |  02  |  03  |  04  |  05  |  06  |  07  |  08  |  09  |  10  |  11  |  12  |  13  |  14  |  15  |  16  |  17  |  18  |  19  |  20  |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| Value |      |      |  04  |  EC  |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |



###### 05, 08, 09, 06, 07, 10

| Entry |  01  |  02  |  03  |  04  |  05  |  06  |  07  |  08  |  09  |  10  |  11  |  12  |  13  |  14  |  15  |  16  |  17  |  18  |  19  |  20  |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| Value |      |      |      |      |  08  |  07  |  10  |  09  |  06  |  EC  |      |      |      |      |      |      |      |      |      |      |



###### 15, 11, 12, 13

| Entry |  01  |  02  |  03  |  04  |  05  |  06  |  07  |  08  |  09  |  10  |  11  |  12  |  13  |  14  |  15  |  16  |  17  |  18  |  19  |  20  |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| Value |      |      |      |      |      |      |      |      |      |      |  12  |  13  |  EC  |      |  11  |      |      |      |      |      |

