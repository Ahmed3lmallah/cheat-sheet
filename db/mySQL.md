# MySQL DB Cheat Sheet

* [mySQL Data Types](https://www.w3schools.com/sql/sql_datatypes.asp)

### Creating a schema
	
```sql
CREATE SCHEMA IF NOT EXISTS book_store;
```
* In MySQL, a schema is synonymous with a database.

### Creating a table

```sql
USE book_store;
CREATE TABLE IF NOT EXISTS book (
	book_id int not null auto_increment primary key,
	isbn varchar (15) not null,
	publish_date date not null,
	author_id int not null,
	title varchar (70) not null,
	publisher_id int not null,
	price decimal(5,2) not null
);
```

### Setting Foreign Keys

```sql
/* Foreign Keys: book */
alter table book add constraint fk_book_author foreign key (author_id) references author(author_id);
alter table book add constraint fk_book_publisher foreign key (publisher_id) references publisher(publisher_id);
```

## CRUD Queries

[C]reate, [R]ead, [U]pdate, and [D]elete

### Create 

```sql
INSERT INTO book (title, isbn, price, publish_date, author_id, publisher_id) VALUES (?, ?, ?, ?, ?, ?)
```
### ReadAll

```sql
SELECT * FROM book
```

* Instead of `SELECT * FROM book` we can specify which columns to be retrieved by using `SELECT title, isbn FROM book`

* To rename headers in the result grid we can use `SELECT title "Book Title", isbn "Book ISBN" FROM book`

### Read

```sql
SELECT * FROM book WHERE book_id = ?
```

### Update

```sql
UPDATE book SET title = ?, isbn = ?, price = ?, publish_date = ?, author_id = ?, publisher_id = ? WHERE book_id = ?;
```

### Delete

```sql
DELETE FROM book WHERE book_id = ?
```

## Operators:

* For the condition `WHERE book_id = ?` we can also use comparators & boolean operators: `SELECT * from book WHERE book_id < ? or book_id > ?`

* In mySQL `<>` represents the "Not Equal" operator.

* For null values we can use `WHERE book_id is null` or `WHERE book_id is not null`

* `WHERE city in ('Albany','Boston');` is equivalent to `WHERE city = 'Albany' or city = 'Boston';`

#### The LIKE operator

* To find entries with title starting with a specific letter (s, for example): `where title like 'S%';`

* To find entries with title containing a specific letter: `where title like '%S%';`

* To find entries with title ending with a specific letter: `where title like '%S';`

* We can use any compination we want. For example, `where title like 'S%' and isbn like 'G%';`

* Under_scores are used as place holders for letters. If we need to find entries where third letter is 'a' we can use 2 underscores: `where title like '__a%';`

## Sorting Results

* To sort data we can use `ORDER BY` with `asc` (ascending) or `desc` (descending). `asc` is set by default.

```sql
select first_name, last_name from employees ORDER BY last_name;
```

```sql
select first_name, last_name from employees ORDER BY last_name desc;
```

```sql
select city, first_name, last_name from employees ORDER BY city, last_name;`
```

## Joins

### Inner join Example:

```sql
select * from northwind.orders inner join northwind.employees on orders.employee_id = employees.id;
```

### Multiple Inner joins:

```sql
select orders.id "Order ID", 
	customers.id "Customer ID",
	customers.first_name,
	customers.last_name,
	employees.first_name "Employee", 
	orders.order_status "Status",
	order_details.product_id "Product id",
	order_details.unit_price "Price",
	products.product_name "Product Name"
from northwind.orders
inner join northwind.employees on  employees.id = orders.employee_id
inner join northwind.customers on orders.customer_id = customers.id
inner join northwind.order_details on orders.id = order_details.order_id
inner join northwind.products on order_details.product_id = products.id
where orders.employee_id = 208 and orders.order_status = 'complete';
```
	
### Outer Left Join:

```sql
select employees.first_name, employees.last_name, orders.order_status
from northwind.employees left outer join northwind.orders
on orders.employee_id = employees.id;
```