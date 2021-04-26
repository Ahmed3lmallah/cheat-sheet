# PostgreSQL DB Cheat Sheet

* **[PostgreSQL Documentation](https://www.postgresql.org/docs/9.5/index.html)**

* **[PostgreSQL Data Types](https://www.postgresql.org/docs/9.5/datatype.html)**

## Create Database

```sql
CREATE DATABASE db_name;
```

## Create Table [Reference](https://www.postgresqltutorial.com/postgresql-create-table/)

```sql
CREATE TABLE table_name (
	id INTEGER,
	a TEXT,
	b VARCHAR (255)
)
```



## Drop Table

```sql
DROP TABLE table_name;
```

## Inserting Data

```sql
INSERT INTO table_name VALUES (1, 'a value', 'b value');
```

* Specifying Data - **useful when we don't know the order of fields**

```sql
INSERT INTO table_name (id, a, b) VALUES (1, 'a value', 'b value');
```

## Updating Data

* Update all records:

```sql
UPDATE table_name SET a = 'new a value';
```

* Update a selected record:

```sql
UPDATE table_name SET a = 'new a value' WHERE a = 'a value';
```

## Deleting Data

* Delete all records:

```sql
DELETE FROM table_name
```

* Delete specific record:

```sql
DELETE FROM table_name WHERE a = 'a value';
```

## Retrieving DATABASE

* Retrieving All Data

```sql
SELECT * FROM table_name;
```

* Retrieving Specific Columns

```sql
SELECT a, b FROM table_name;
```

* Retrieving Specific Records

```sql
SELECT * FROM table_name 
WHERE a = 'a value';
```

## Sorting Results

```sql
[SOME QUERY]
ORDER BY a;
```

```sql
[SOME QUERY]
ORDER BY a DESC;
```

* Sorting Results by Multiple Columns

```sql
[SOME QUERY]
ORDER BY a, b;
```

## Operators

* `OR` operator

```sql
SELECT * FROM table_name
WHERE a = 'a value'
OR a = 'different a value';
```

* `AND` operator

```sql
SELECT * FROM table_name
WHERE a = 'a value'
AND b = 'b value';
```