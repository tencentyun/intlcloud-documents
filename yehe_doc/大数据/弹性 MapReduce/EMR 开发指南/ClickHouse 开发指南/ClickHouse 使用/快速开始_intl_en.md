
1. In the EMR Console, create a ClickHouse cluster and log in to a server in it at the public IP address.
2. Prepare data in CSV format by creating an `account.csv` file in the `/data` directory.
```
AccountId, Name, Address, Year
1, 'GHua', 'WuHan Hubei', 1990
2, 'SLiu', 'ShenZhen Guangzhou', 1991
3, 'JPong', 'Chengdu Sichuan', 1992
```
3. Use `clickhouse-client` to connect to the service and create a database and table.
```
CREATE DATABASE testdb;
CREATE TABLE testdb.account (accountid UInt16, name String, address String, year UInt64) ENGINE=MergeTree ORDER BY(accountid);
```
4. Import data into the data table.
```
cat /data/account.csv | clickhouse-client --database=testdb --query="INSERT INTO account FORMAT CSVWithNames"
```
5. Query the imported data.
```
select * from testdb.account;
```
![](https://main.qcloudimg.com/raw/5d1ccbeb47e89de477375fec300174c6.png)
