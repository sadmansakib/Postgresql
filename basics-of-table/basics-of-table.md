## **Basics of Table**

After successful creation of a Postgresql database the first step is to create a table for structuring our database system. We have already saw how to create a database in [Getting Started](getting-started/getting-started.md)

### Connect to existing database

We can connect to existing database we built by putting the following simple command 

```sh
psql -h hostname/host ip address -p portnumber -d database name -U owner name of the database -W
```

by default database is hosted on portnumber 5432 if localhost is being used as host. So command for any database hosted on localhost with default configuration will be

```sh
psql -h localhost -p 5432 -d database name -U database owner name -W
```

for example,

```sh
psql -h localhost -p 5432 -d mydatabase -U sadmansakib -W
```

or alternatively we can use `\c database name` command in [postgresql user mode](/getting-started/getting-started.md)


### Create a table

A basic table can be created using this command

```sql
CREATE TABLE person(
    id INT,
    first_name VARCHAR(20),
    last_name VARCHAR(20),
    gender VARCHAR(8),
    email VARCHAR(40),
    date_of_birth DATE
);
```
But there are bunch of drawbacks in the command such as,

- Integer type id has to be maintained manually
- All columns of the table are nullable which means we can create a person table without email, date of birth and even without a name.

So there are few contraints and improvements are needed to create a proper person table.

```sql
CREATE TABLE person(
    id BIGSERIAL NOT NULL PRIMARY KEY,
    first_name VARCHAR(20) NOT NULL,
    last_name VARCHAR(20) NOT NULL,
    gender VARCHAR(8) NOT NULL,
    email VARCHAR(40),
    date_of_birth DATE NOT NULL
);
```
Now if we run `\d` is psql shell we get

```sh
                 List of relations
 Schema |      Name       |   Type   |    Owner    
--------+-----------------+----------+-------------
 public | person        | table    | sadmansakib
 public | person_id_seq | sequence | sadmansakib
```
there is an extra entry of `sequence` type because we have declared our primary key `BIGSERIAL`. `BIGSERIAL` is a data type which automatically manages increment of a value and sequence.

also if we run run,

```sh
\d person
```
our result will be something like,

```sh
                                       Table "public.person"
    Column     |          Type          | Collation | Nullable |              Default               
---------------+------------------------+-----------+----------+------------------------------------
 id            | bigint                 |           | not null | nextval('person_id_seq'::regclass)
 first_name    | character varying(20)  |           | not null | 
 last_name     | character varying(20)  |           | not null | 
 gender        | character varying(8)   |           | not null | 
 email         | character varying(40)  |           |          | 
 date_of_birth | date                   |           | not null | 
Indexes:
    "person_pkey" PRIMARY KEY, btree (id)
```
Here we can see that our necessary column informations are not nullable but email is still nullable because there can be a person without an email address.

### table constraint

we can not use some specific keywords such as `user` as our table name. If we try to create a table with the name user we will get an error something like this,

```sh
mydatabase=# CREATE TABLE user (
  id BIGSERIAL NOT NULL PRIMARY KEY,
  first_name VARCHAR(50) NOT NULL,
  last_name VARCHAR(50) NOT NULL,
  gender VARCHAR(8) NOT NULL,
  email VARCHAR(150),
  date_of_birth DATE NOT NULL
);
ERROR:  syntax error at or near "user"
LINE 1: CREATE TABLE user (
                     ^
mydatabase=# 
```

we can find the full list of keywords in  [Postgresql keyword list](https://www.postgresql.org/docs/current/sql-keywords-appendix.html)


### Inserting data into a table

There are two ways we can insert data into our table.

First approach,

```sh
mydatabase=# INSERT INTO person
mydatabase-# VALUES(1,'james','patrick','MALE','james46@gmail.com', date '1986-11-12');
```

here we haven't mention any column name thus we have to insert everything for every column.This approach has an issue. We have already mentioned that `BIGSERIAL` data structure automatically manages our id. Thus we should not be worried about id sequence but in this approach we have to explicitely insert a person id.

Second approach,

```sh
mydatabase=# INSERT INTO person(first_name,last_name,gender,email,date_of_birth)
mydatabase-# VALUES('james','patrick','MALE','james46@gmail.com', date '1986-11-12');
```
```sh
mydatabase=# INSERT INTO person(first_name,last_name,gender,date_of_birth)
mydatabase-# VALUES('james','patrick','MALE', date '1988-10-20');
```

In this approach we have to explicitely mention our column names. Benefit of this approach is that we can avoid inserting our id which should be auto generated and we can also create multiple queries with and without nullable columns such as `email`. here we have created two persons where one have an email and other one doesn't have one.

#### Insert multiple values in a table

In real life we generate hundreds and thousands of persons in a database but doing this manuall on a shell is a hectic job. So, we import a sql file. To do this we execute the following command in the `psql` shell

```sh
\i /pathto/people.sql
```
this will take all the queries from sql file execute in the database.

### Get data from a table

If we want to see the data we inserted in the table, we have to use `SELECT` keyword.

for example,

```sql
SELECT * FROM database_table;
```

here `*` indicates everthing. So, this command will fetch every values from every columns available from the table.

Alternatively if we want to fetch a specific column of the table we have to use

```sql
SELECT column_name FROM database_table;
```
This command will only show the values of a specific column name mentioned in the query.

for example if we want to see all the first names from the people table then we have to write

```sql
SELECT first_name FROM people;
```
This will show all the first names from the people table

### Deleting a table

If we want to delete a specific table then we have to use the following command,

```sql
DROP TABLE table_name;
```
for example if we want to remove the people table then all we have to is to put

```sql
DROP TABLE people;
```

command. Then our people table will be dropped.