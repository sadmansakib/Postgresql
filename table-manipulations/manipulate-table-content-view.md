## **Basics of table view manipulation**

### Limit keyword

If we want to fetch a limited number of rows from a table we can use Limit keyword.

```sql
SELECT * FROM tableName LIMIT 10;
```

This command will show the first 10 rows from table instead of all rows.

### Offset keyword

Fetch Keyword is used for skipping a number of rows from the begining of the table

```sql
SELECT * FROM tableName OFFSET 5 LIMIT 10;
```
This command will skip first 5 rows from the table and show 10 rows. That means first row of our output will be from row 06.

### Fetch keyword

Fetch works the same thing that limit does but this is a standard SQL keyword where limit is not a standard SQL keyword.

```sql
SELECT * FROM tableName OFFSET 5 FETCH 10 ROW ONLY;
```
This command also shows first 10 rows and also skips first 5 rows though this is standard SQL usage.

also if we want to see the first row only then we can use.

```sql
SELECT * FROM tableName OFFSET 5 FETCH FIRST ROW ONLY;
```
This command will only show the 6th row from the table

### In keyword

In keyword is used for narrowing down query using an array of values. For example, Suppose we have a person table of 1000 rows where every person has different place of birth. If we want to find people who born in 3 or 4 countries we can search using two approaches.

Firstly approach is using repititive conditions using WHERE keyword

```sql
SELECT * FROM person WHERE place_of_birth = 'United States', OR place_of_birth = 'Bangladesh' OR place_of_birth = 'Ukraine';
```

This query is very length and if we keep increasing our searching parameter than the query will become a mess.

Instead, we can use the second approach which is using IN keyword

```sql
 SELECT * FROM people 
 WHERE place_of_birth
 IN ('United States', 'Bangladesh', 'Ukrain'); 
```

### Between keyword

BETWEEN keyword is used for searching for data in a range of numerical values such as dates and age

```sql
SELECT * FROM people 
WHERE date_of_birth
BETWEEN DATE '1990-01-01' AND '2020-01-01'; 
```
BETWEEN can be used with order by to give a sorted view

```sql
SELECT * FROM people 
WHERE date_of_birth
BETWEEN DATE '1990-01-01' AND '2020-01-01' ORDER BY date_of_birth ASC/DESC; 
```

### Like and ILike keywords

Using Like and ILike keywords we can norrowdown searching queries using patterns.

```sql
SELECT * FROM people 
WHERE email LIKE '%@gmail.com'
```
Here we are searching for all the information where email belongs to gmail.com. `%` indicates wild card entry which means there could be any number of characters there followed by `@` and `gmail.com`

```sql
SELECT * FROM people 
WHERE email LIKE '______@%'
```
in `LIKE` keyword we can determine any number character checking using `_` .
In the command stated above we are checking six characters followed by `@` and any domain name.

The key difference between `LIKE` and `ILIKE` that `ILIKE` is case insensitive.