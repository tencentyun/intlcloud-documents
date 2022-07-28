## Inserting Data
1. Insert data corresponding to the column name.
```
INSERT INTO products (name, price, product_no) VALUES ('cheese', 99, 1);
```
2. Insert data in the order of the column names defined in the table.
```
INSERT INTO products VALUES(2, 'chesse', 99);
```
3. Insert multiple data records at once.
```
INSERT INTO products VALUES (3, 'a', 1), (4, 'b', 2), (5, 'c', 3);
```
4. Import data through an external table as instructed in [Using External Table](https://intl.cloud.tencent.com/document/product/1138/45032).
5. Import data from TencentDB via extensions as instructed in [Importing External Data](https://intl.cloud.tencent.com/document/product/1138/45035).
6. Insert data by using the `COPY` command. You need to log in to the database system, select the database, create the corresponding table, and use `COPY` to insert the data from the specified `filename` into `tablename` with the specified delimiter `,`. The command is as follows:
```
COPY tablename  FROM 'filename'  WITH DELIMITER ','; 
```

## Updating Data
Update the data in the column corresponding to the row that satisfies the `WHERE` condition to the specified value as shown below:
```
UPDATE products SET price = 10 where product_no = 3;
```

## Deleting Data
Delete the row that satisfies the `WHERE` condition as shown below:
```
DELETE FROM products where price = 3;
```
Delete all data in the table as shown below:
```
DELETE FROM products;
```
## Querying Data

Access the database as instructed in [Accessing Data Warehouse](https://intl.cloud.tencent.com/document/product/1138/45128) and query data as shown below:

1. Enter the specified database, for example, `test`:
```
\c test;
```
2. Create the `test` table.
```
create table test(a1 int);
```
3. Insert the data.
```
insert into test values(3),(4);
```
4. Query the data. 
```
select * from test;
```
