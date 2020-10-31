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

The table file is a binary file. The file consist of integer numbers stored one after another. The integer numbers have fixed size within the table file. 

There are three types of table files: 12, 16 and 32 bits.  The table file type can be recognized by table marker.  

| Entry Size | Description         | Table Marker           |
| ---------- | ------------------- | ---------------------- |
| 12 bit     | 1.5 bytes per entry | 0xFF0, 0xFFF           |
| 16 bit     | 2 bytes per entry   | 0xFFF8, 0xFFFF         |
| 32 bit     | 4 bytes per entry   | 0x0FFFFFF8, 0xFFFFFFFF |



#### Table

The table is a set of fixed size integer numbers. The entry is represented by a position within the table and the value in that position.  It is like index of the list and the value.  The table holds a number of entry chains. The chains are represented by set of entry positions. 

posistions within the table and the values are pointers to the next position or indicate end of the chain.




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

The chain can be composed of one or more entry positions. The entry value points to another entry position and so on until the value indicates end of chain (EC).

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

#### Entry Size



##### 12 bit

First five values of 12 bit entries

```
A		1		 2		     3	     	4		 5			 6			7		 8
B		11110000 1111	1111 11111111	00000011 0100	0000 00000000	00000101 0110	0000
C		1111 11110000	11111111 1111	0000 00000011	00000000 0100	0000 00000101	
D		F F0			FF F			0 03			00 4			0 05
E		0xFF0			0xFFF			0x3				0x4				0x5
F		4080			4095			3				4				5
```

##### 16 bit

First five values of 16 bit entries 

```
A		1		 2			3		 4			5		 6			7		 8			9		 10
B		11111000 11111111	11111111 11111111	00000000 00000000	00000101 00000000	00000110 00000000
C		11111111 11111000	11111111 11111111	00000000 00000000	00000000 00000101	00000000 00000110
D		FF F8				FF FF				00 00				00 05				00 06
E		0xFFF8				0xFFFF				0x0					0x5					0x6
F		65528				65536				0					5					6
```

##### 32 bit

First two values in 32 bit entries

```
A		1		 2        3        4         5        6	       7		8			
B		11111000 11111111 11111111 00001111	 11111111 11111111 11111111 11111111	
C		11111111 11111111 11111111 11111000	 11111111 11111111 11111111 11111111	
D		0F FF FF F8			                 FF FF FF FF
E		0x0FFFFFF8		 					 0xFFFFFFFF		
F		268435448							 4294967295
```





| Row  | Description                                         |
| :--: | --------------------------------------------------- |
|  A   | Byte number                                         |
|  B   | Bits in little endian byte order.                   |
|  C   | Bits in reversed byte order                         |
|  D   | Hexadecimal representation of the n-bit entry value |
|  E   | Entry value in hex                                  |
|  F   | Entry value                                         |

