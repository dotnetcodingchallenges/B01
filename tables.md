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

The table is a list of entries represented by integer numbers. 



Following table represents **Entry** number and it's Value. The Value points to another **Entry**. If the Value is LE (Last Entry) there is no more  

| Entry |  01  |  02  |  03  |  04  |  05  |  06  |  07  |  08  |  09  |  10  |  11  |  12  |  13  |  14  |  15  |  16  |  17  |  18  |  19  |  20  |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| Value |  TM  |  TM  |  04  |  CE  |  06  |  07  |  08  |  09  |  10  |  CE  |  12  |  13  |  LE  |  15  |  11  |  CE  |  16  |  17  |  00  |  CE  |

The example table consist of 20 entries. The entries include 

* Table marker (TM)  

* Empty entry

* Chain with Chain End (CE) marker

  

  

##### Table marker

The first two entries in the table consist of table marker. 



##### Empty entry

The table may contain one or more empty entries. The entry is empty when the value is set to zero.



##### Entry chains

The chain can be composed of one or more entries.  

Chain with 2 entries:

###### 03, 04

| Entry |  01  |  02  |  03  |  04  |  05  |  06  |  07  |  08  |  09  |  10  |  11  |  12  |  13  |  14  |  15  |  16  |  17  |  18  |  19  |  20  |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| Value |      |      |  04  |  CE  |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |      |

Chain with 6 entries: 

###### 05, 08, 09, 06, 07, 10

| Entry |  01  |  02  |  03  |  04  |  05  |  06  |  07  |  08  |  09  |  10  |  11  |  12  |  13  |  14  |  15  |  16  |  17  |  18  |  19  |  20  |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| Value |      |      |      |      |  08  |  07  |  10  |  09  |  06  |  LE  |      |      |      |      |      |      |      |      |      |      |

Chain with 4 entries: 


###### 15, 11, 12, 13
| Entry |  01  |  02  |  03  |  04  |  05  |  06  |  07  |  08  |  09  |  10  |  11  |  12  |  13  |  14  |  15  |  16  |  17  |  18  |  19  |  20  |
| :---: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| Value |      |      |      |      |      |      |      |      |      |      |  12  |  13  |  LE  |      |  11  |      |      |      |      |      |

