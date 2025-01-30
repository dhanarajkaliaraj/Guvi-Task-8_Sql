# Guvi-Task-8 SQL 

## Creating table  

### Customer Table
> CREATE TABLE customers (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    email TEXT,
    address TEXT
    );

Description: 
- The above query creates a table called 'customers' with columns as id with INTEGER datatype and    PRIMARY KEY constraints indicates its as unique key which also be used in other table as a reference key of this table with auto-incremental values which is denoted by AUTOINCREMENT.
- Column name, email, address are also created with the datatype as TEXT. 

### Orders Table
> CREATE TABLE orders (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    customer_id INTEGER,
    order TEXT,
    order_date DATE,
    total_amount FLOAT,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
    );

Description:
The above command creates table in the name of 'orders' and also columns as follows,
- id with INTEGER datatype and constrainted with 'PRIMARY KEY' and 'AUTOINCREMENT'
- customer_id with INTEGER datatype in last part of the command it is referenced as 'FOREIGN KEY' which holds the same id of customers table column id.
- order with TEXT datatype.
- order_date with DATE datatype.
- total_amount with FLOAT datatype.

### Product Table

> CREATE TABLE products (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT,
    price FLOAT,
    description TEXT
    );

Description:
The above command creates table in the name of 'products' and also some columns as follows,
- id with INTEGER datatype and constrainted with 'PRIMARY KEY' and 'AUTOINCREMENT'
- name with TEXT datatype .
- price with FLOAT datatype.
- description with TEXT datatype.


### Task Query

## Retrieve all customers who have placed an order in the last 30 days.

> SELECT name FROM customers 
    JOIN orders ON customers.id = orders.customer_id 
        WHERE order_date >= DATEADD(DAY, -30, GETDATE());

Description:
- The above query fetches all the 'name' column from customer table which also merges orders table by JOIN ON clause by equaling both primary and foreign key.
- Then the WHERE clause filters the order date from last 30days.

## Get the total amount of all orders placed by each customer.

> SELECT name, SUM(total_amount) AS sum_total FROM customer 
    JOIN orders ON customer.id = orders.customer_id 
        GROUP BY name;

Description:
- The above SELECT command fetches name, and total_amount by passing it to aggrigate SUM() function which sums up all total_amount.
- JOIN ON merges customers and orders table by matching PRIMARY and FOREIGN KEY id.
- Result data are filtered by name using GROUP BY keyword.

## Update the price of Product C to 45.00.

> UPDATE products SET price = 45.00
    WHERE name = 'C';

Description:
- The above UPDATE command will update the price value with 45.00 in products table.
- WHERE clause gives the exact place where it needs to be updated.

## Add a new column discount to the products table.

> ALTER TABLE products
    ADD COLUMN discount FLOAT;

Description:
- The above command alters products table by ALTER TABLE command and ADD COLUMN inserts new column in the name of 'discount' with FLOAT datatype.

## Retrieve the top 3 products with the highest price.

> SELECT name, price FROM products 
    ORDER BY price DESC 
        LIMIT 3;

Description:
- The above command fetches name, price data from products table.
- ORDER BY clause will orders the result in descending order.
- LIMIT 3 keywords filters first 3 rows of the result data.


## Get the names of customers who have ordered Product A.

> SELECT name, order AS order_name FROM customer 
    JOIN orders ON customer.id = orders.customer_id 
        WHERE order = 'A';

Description:
- The above command fetches name from customer table  and order_name from merged orders table by JOIN ON command by matching ids of PRIMARY and FOREIGN KEY.
- 'WHERE' keyword Filters only the customers who have orderd 'A'.

## Join the orders and customers tables to retrieve the customer's name and order date for each order.

> SELECT name, order_date AS order_name FROM customer
    JOIN orders ON customer.id = orders.customer_id;

Description:
- SELECT command fetches the given column name values, here name and order_date.
- JOIN ON command merges both tables orders and customers by matching the FOREIGN and PRIMARY KEY.

## Retrieve the orders with a total amount greater than 150.00.

> SELECT total_amount FROM orders 
    WHERE total_amount > 150.00;

Description:
- SELECT total_amount fetches all the total_amount from orders table.
- WHERE command filters data according to the given condition, here total_amount is greater than 150.00  


## Normalize the database by creating a separate table for order items and updating the orders table to reference the order_items table.

> CREATE TABLE order_items (
    item_id INTEGER AUTO_INCREMENT PRIMARY KEY,
    order_id INTEGER,
    FOREIGN KEY (item_id) REFERENCES orders(id));

Description:
- order_items table created using CREATE TABLE command with the item_id as PRIMARY KEY with AUTOINCREMENT and INTEGER as datatype.
- Assigning FOREIGN KEY as item_id by REFERENCES 'id' of 'orders table'. 

## Retrieve the average total of all orders.

> SELECT AVG(total_amount) AS average_order_total 
    FROM orders;

Description:
- Fetches all total_amount from orders table and which is being aggrigate by AVG() function which returns average value.
