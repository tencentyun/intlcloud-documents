## Inserting Data

1. Insert the data corresponding to the column name:

   ```
   INSERT INTO products (name, price, product_no) VALUES ('cheese', 99, 1);
   ```

2. Insert data in the order of the column names defined in the table:

   ```
   INSERT INTO products VALUES(2, 'chesse', 99);
   ```

3. Insert multiple data entries at once:

   ```
   INSERT INTO products VALUES (3, 'a', 1), (4, 'b', 2), (5, 'c', 3);
   ```

4. Import data from an external table. For more information on how to import data from external tables, see [here](https://cloud.tencent.com/document/product/878/20068).

5. Import data from CDB using a plug-in. For details, see [here](https://cloud.tencent.com/document/product/878/20069).

6. Insert data using the COPY command:
   You need to first log in to the database system, select a database, create a corresponding table and then use the COPY command to insert the data into the tablename from the specified file "filename" with the specified delimiter ",". The command is as follows:

   ```
   COPY tablename  FROM  'filename' WITH DELIMITER ','; 
   ```

## Updating Data

Update the data in the columns corresponding to the rows that satisfy the where condition to the specified values, as shown in the following example:

```
UPATE products SET price = 10 where product_no = 3;
```

## Deleting Data

Delete the rows that satisfy the where condition, as shown in the following example:

```
DELETE FROM products where price = 3;
```

The following is an example of deleting all the data in a table:

```
DELETE FROM products;
```

