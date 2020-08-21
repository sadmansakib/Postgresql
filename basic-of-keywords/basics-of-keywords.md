## **Basics of Keywords**

### **ORDER BY**

Order by keyword is used for sorting database on either ascending or descending order based on a column or multiple columns

#### ASC

keyword for ordering database table by ascending order using one or multiple colummns

```sql
SELECT * FROM dbName ORDER BY columnNames ASC;
```

#### DESC

keyword for ordering database table by descending order using one or multiple colummns

```sql
SELECT * FROM dbName ORDER BY columnNames DESC;
```

### **DISTINCT**

Show values of a column without duplicates.

```sql
SELECT DISTINCT columnName FROM dbName;
```
if combined with order by:

```sql
SELECT DISTINCT columnName FROM dbName ORDER BY columnName
```

### **WHERE keyword and AND**

Where keyword is used for setting up conditions for query 

```sql
SELECT columnName FROM dbName WHERE condition;
```

For example:

```sql
SELECT first_name FROM dbName WHERE gender = 'male';
```

Using AND keyword we can use multiple conditions for a query

```sql
SELECT columnName FROM dbName WHERE condition1 AND condition2;
```

For example:

```sql
SELECT first_name FROM dbName WHERE gender = 'male' AND country = 'Bangladesh';
```

### **Comparision Operators**

Comparision Operators are used to make logical and arithmatic operation under WHERE keywords to filter down data.


| Operator 	|    Description    	|
|:--------:	|:-----------------:	|
|     <    	|     less than     	|
|     >    	|     more than     	|
|    <=    	|  less or equal to 	|
|    =>    	| great or equal to 	|
|     =    	|       equal       	|
| <> or != 	|     not equal     	|

