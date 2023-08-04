## Use Cases
iPaaS provides various status management solutions. You can log in to the [iPaaS console](https://ipaas.tencentcloud.com/login) and click **Integration tools** > **General storage** on the left sidebar to manage storage structures and data used in your project.


## General Storage Management
The **General storage** homepage is the storage management page, where you can create storages and view the list of all created storages, including storage name, storage type, and operations that can be performed on different storage types.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/mc2T784_175.png)

## Creating a Storage
You can quickly create a storage simply by configuring the storage name and type.
- Storage name: Enter up to 25 letters and underscores.
- Storage type: Select table structure, hash structure, list, or string.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/eyYM492_176.png)


### Table structure
#### Editing a structure
You can use the structure editing feature to maintain table structures, including column information, index information, and relationship configuration.
- **Column information**: You can add, modify, and delete a column in the table to quickly orchestrate the structure. Currently, you can edit the column name, data type (the following data types are supported: `string`, `bool`, `int`, `float`, `decimal`, `datetime`, `date`, and `time`), value length (if the type is `string`), precision, and decimal places (if the type is `decimal`), set a column as the primary key, and enable automatic numbering (only if the column is the primary key).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/s8ZI640_177.png)

- **Index configuration**: The index configuration is similar to that in MySQL. On this tab, you can create indexes to accelerate MySQL search. Currently, you can create, delete, and name indexes, configure the index type (two types are supported: `index` and `unique`; for their differences, see [13.1.15 CREATE INDEX Statement](https://dev.mysql.com/doc/refman/8.0/en/create-index.html)), and configure the index column (select a column in the maintained column list).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/y7vA546_178.png)

- **Relationship configuration**: You can also configure foreign key information for an iPaaS general storage. You can name a foreign key, configure the foreign key column, and select the foreign key source table and column. To configure foreign key event triggering, you can configure **On Delete** and **On Update** options as instructed in [13.1.15 CREATE INDEX Statement](https://dev.mysql.com/doc/refman/8.0/en/create-index.html).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9IWb691_179.png)

#### More operations
- **Clearing the table structure**: You can click **Clear** to clear all data in the current table structure.
>!This operation is a high-risk operation, after which all data in the storage will be cleared and cannot be recovered, so proceed with caution.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/UhMK740_180.png)
- **Copying a table with the same structure**: You can click **Copy table with same structure** to quickly create a table with the current structure, which facilitates data structure migration and backup.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/AevH596_181.png)
- **Deletion**: You can click **Delete** to delete the corresponding storage record. **This operation is also a high-risk operation and will affect the data in the production environment, so proceed with caution.**

### Hash structure
A hash is a data structure that can be directly accessed through a key value. It maps a key value to a position in the table to access the record, so as to accelerate search. iPaaS allows you to create hash table structures containing data in key-value format.

### List
A list is also called an array, which is an ordered element sequence, i.e., a group of data elements with IDs. It is used to store a set of elements of the same data type.

### String
A string consists of digits, letters, and underscores. You can create and use strings through the general storage feature in iPaaS, so as to quickly reuse strings to simplify operations.
