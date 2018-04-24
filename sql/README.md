# Exercice SQL


## FUNDAMENTALS

Make exercices of [SQL Bolt](https://sqlbolt.com/)

## PRACTICE

Create Postgresql database using docker

1. Create docker file `docker-compose.yml`

```yml
version: '2'

services:

 pgsql:
   image: postgres:9.6.1-alpine
   ports:
     - "0.0.0.0:3333:5432"
   restart: "always"
   environment:
     - POSTGRES_USER=agd
     - POSTGRES_PASSWORD=agd
     - POSTGRES_DB=BDD
     - PGDATA=/var/lib/postgresql/data/BDD

```

2. Start docker container (containing database)

```bash
$ docker-compose up -d && docker-compose logs -f
```

3. Add your new database using `SQLectron` with following configuration:
* `Name`: name used for record database connection
* `Client`: choose Mysql or Postgresql depending of your databese language
* `Server Address`: refer to `docker-compose.yml` where:
	* `Host`: 0.0.0.0
	* `Port`: 3333
* `Database/keyspace`: refer to `docker-compose.yml` where keyspace =  `BDD`

4. Connect and use your database

## CMD

### Quick use docker

* start container: docker-compose up -d
* log container: docker-compose logs -f
* stop container: docker-compose stop
* remove container: docker-compose rm

### Quick set table

* Create Two table: `customers` and `customers_sales`:
```sql
CREATE TABLE customers (
    id INTEGER PRIMARY KEY,
    company TEXT,
    function TEXT,
    name TEXT,
    email TEXT
);
CREATE TABLE customers_sales (
    id INTEGER PRIMARY KEY,
    id_customer INTEGER,
    item TEXT,
    amount INTEGER
);
```

* Insert data in tables `customers` and `customers_sales`:

```sql
INSERT INTO customers (id, company, function, name, email)
VALUES (1, 'Cisco', 'Manager', 'Rico D.', 'r.d@cisco.com'),
(2, 'Pivotal', 'Director', 'Henry B.', 'h.b@pivotal.io'),
(3, 'Xebia', 'Sales', 'Tony F.', 'tony.f@xebia.fr');

INSERT INTO customers_sales (id, id_customer, item, amount)
VALUES (1, 2, 'Software', 90000),
(2, 1, 'Website', 25000),
(3, 3, 'Email server', 45000),
(4, 1, 'Software', 150000),
(5, 2, 'Mobile application', 15000);
```

* Check table `customers`:

```sql
SELECT * FROM customers;
```

* Check table `customers_sales`:

```sql
SELECT * FROM customers_sales;
```

### Common CMD

##### Maintain DDB

* create table

```sql
CREATE TABLE table_name (
    column_name data_type,
    column_name data_type
);
```

* insert data
```sql
INSERT INTO MyTable ( Column1, Column2 ) VALUES
( Value1, Value2 ), ( Value1, Value2 )
```

* add column to existing table
```sql
ALTER TABLE table_name
ADD column_name datatype;
```

* remove column to existing table
```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

* change datatype of column in existing table
```sql
ALTER TABLE table_name
MODIFY COLUMN column_name datatype;
```

* change date of column in existing table
```sql
UPDATE table_name SET column_name = 'new data' WHERE column_name = 'existing data reference'
```

##### Use DDB

* Sum cell of multiple row
```sql
SELECT id_customer, company, sum(amount)
FROM customers
  LEFT JOIN customers_sales
    ON customers_sales.id_customer = customers.id
GROUP BY id_customer, company
ORDER BY id_customer ASC;
```

#### CMD References

##### SQL QUERIES FUNDAMENTALS

`SELECT` 
- `DISTINCT` => no duplicate
- `*` => select all column
- `column_name-1, column_name-2`...   => select specific column


`FROM` `table_name` 

`WHERE` condition  `AND` / `OR` other condition
- `=` / `!=` / `<` / `<=` / `>` / `>=`
- `BETWEEN` ... `AND`...
- `NOT BETWEEN` ... `AND`...
- `IN` (...)
- `NOT IN` (...)
- `LIKE` "ABC" (strict querie)    or   "%ABC%"  (partial querie)
- `NOT LIKE` "ABC" 

`ORDER BY` column_name `ASC` or `DESC`

`LIMIT` num_limit `OFFSET` num_offset


##### MULTI SQL QUERIES (JOINS)

###### INNER JOIN
```
INNER JOIN another_table 
    ON mytable.id = another_table.id
```
> where ON link to reference cell and INNER JOIN === JOIN

###### OUTER JOINs
```
INNER/LEFT/RIGHT/FULL JOIN another_table 
    ON mytable.id = another_table.matching_id
```
> to use when data is entered in different stages

##### Date
Date format


concat

##### Math
aroundir (round)
sum
truncate