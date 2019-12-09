## Via the GUI of the phpMyAdmin Console
### Dropping a Database
1. Log in to the [phpMyAdmin Console](https://intl.cloud.tencent.com/document/product/236/32341), click the name of database to be managed to enter the database management page, and click **Operation**.
![](https://main.qcloudimg.com/raw/ff37d09e2844114378b6952dcfe9a5c6.png)
2. You can perform various operations on databases on this page, such as **creating a table** and **dropping a database**. To drop a database, click **Drop Database (DROP)**.


### Dropping a Table
Select the database for which to drop a table. You can perform various operations on tables on this page, such as **viewing**, **structuring**, **searching**, and **dropping**. Click **Drop**.
![](https://main.qcloudimg.com/raw/d782e2f163851208d175b58e4d1383b6.png)

## Via SQL Commands in the phpMyAdmin Console
### Dropping a Database
1. Log in to the phpMyAdmin Console. To drop a database with an SQL command, click **SQL**.
![](https://main.qcloudimg.com/raw/d6ddac058780924dc717d54c61e92083.png)
2. Run the following command to drop a database.
```
drop database <database name>;
```

### Dropping a Table
1. To drop a table with an SQL command, click **SQL**.
![](https://main.qcloudimg.com/raw/b487a3625a974f45f9b5ebc6c58372f0.png)
2. Run the following command to drop a table.
```
drop table <table name>;
```
