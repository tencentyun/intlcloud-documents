This document describes how to create databases and tables in TencentDB for MySQL instances.

## Concepts
- **Instance**: a standalone database environment running in Tencent Cloud, which can include multiple databases created by users and can be accessed using the same tools and applications as those for a standalone database instance.
- **Database**: a warehouse that organizes, stores, and manages data based on its structure.

## Creating Database
1. Log in to the [phpMyAdmin Console](https://intl.cloud.tencent.com/document/product/236/32341), click **New** or **Databases** to enter the database creation page.
![](https://main.qcloudimg.com/raw/e7fab349b3854db1fa15b111a7d99786.png)
2. Enter the database name, select the collation (`utf8_general_ci` by default), and click **Create**.
>
>- Database name: a database name contains 1-64 characters, and must be unique in the instance.
>- Collation: click <img src="https://main.qcloudimg.com/raw/63e8499b6204a9e75179809e80d7867c.png"  style="margin:0;"> next to "Create database" to be redirected to [MySQL official documentation](https://dev.mysql.com/doc/refman/5.7/en/create-database.html) for details.
>
![](https://main.qcloudimg.com/raw/b4a4fe5ab5f19ebef146f8a81813ad95.png)
3. Select the desired database and click **Operations** on the navigation bar at the top to enter the database operation page, where you can **Create table**, **Remove database**, or perform other operations. You can also move, rename, or copy the database after creation.
![](https://main.qcloudimg.com/raw/b1316742957bcfa1846ea93ab19b045b.png)

## Creating Table
1. Log in to the [phpMyAdmin Console](https://intl.cloud.tencent.com/document/product/236/32341). Select the database where you want to create a table, click **New** or enter the table name and select the number of columns in the **Create table** bar, and then click **Go**.
>Table name: a table name contains 1-64 characters, and must be unique in the database.
>
![](https://main.qcloudimg.com/raw/c267998c45afb6bd58218ca08117e7dc.png)
2. On the table creation page, if you need to add columns, you can enter the number of columns to be added in the **Add** box and then click **Go**. You can enter the column information in **Structure** and partition information in **PARTITION definition** (see [MySQL partitioning chapter](https://dev.mysql.com/doc/refman/5.6/en/partitioning.html)). After entering all the information, click **Save** to create the table.
>You can click <img src="https://main.qcloudimg.com/raw/63e8499b6204a9e75179809e80d7867c.png"  style="margin:0;"> next to the fields for more information.
>
![](https://main.qcloudimg.com/raw/a2599ceef079be861cf797c247da3e03.png)
