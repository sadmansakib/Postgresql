## **Basics of Keywords**

### **ORDER BY**

Order by keyword is used for sorting database on either ascending or descending order based on a column or multiple columns

#### ASC

keyword for ordering database table by ascending order using one or multiple colummns

```sql
SELECT * FROM dbName ORDER BY columnNames ASC
```

#### DESC

keyword for ordering database table by descending order using one or multiple colummns

```sql
SELECT * FROM dbName ORDER BY columnNames DESC
```

### **DISTINCT**

Show values of a column without duplicates.

```sql
SELECT DISTINCT columnName FROM dbName
```
if combined with order by:

```sql
SELECT DISTINCT columnName FROM dbName ORDER BY columnName
```
