
If you use ODBC to connect to TDSQL-A for PostgreSQL databases for operations, you need to deploy the ODBC driver package in advance, which can be obtained [here](https://odbc.postgresql.org/) or from the software provider.

## ODBC-Based Development on Linux
On Linux, application development requires headers such as `sql.h` and `sqlext.h` provided by unixODBC and the `libodbc.so` library, which can be obtained from the ODBC installation package.

Deploy ODBC on Linux:
You can directly run the `yum` command to deploy ODBC and unixODBC.
```
yum install -y unixODBC
yum install -y postgresql-odbc
```
After the deployment is completed, if `isql` can be successfully executed as shown below, ODBC has been deployed successfully.
![](https://main.qcloudimg.com/raw/c0298cbf0e7988583dc6ccaccf16b6ac.png)

Linux ODBC configuration:
1. Create the `/etc/odbc.ini` file and modify parameters such as `Servername`, `UserName`, `Password`, and `Port` in it.
```
vi /etc/odbc.ini 
[tdapg]
Description = Test to tdapg
Driver = PostgreSQL
Database = postgres
Servername = localhost
UserName = dbadmin
Password = tdapg@tdapg
Port = 11345
ReadOnly = 0
ConnSettings = set client_encoding to UTF8
```
After completion, save and exit.
2. Run the `isql -v tdapg(data source name)` command.
If the following information is displayed, the configuration is correct, and connection succeeded.
```
+---------------------------------------+
| Connected!              |
|                   |
| sql-statement              |
| help [tablename]            |
| quit                  |
|                   |
+---------------------------------------+
SQL>
```
If `ERROR` is displayed, the configuration is wrong. Please check whether the above configuration is correct.

## ODBC-Based Development on Windows
On Windows, the relevant headers and library files required by application development are built in the system.
Configure the data source on Windows:
1. Decompress `psqlodbc_13_00_0000-x64.zip` to get the `psqlodbc_x64.msi` driver for direct deployment.
2. Press Win + R and directly run `odbcad32` to open Data Source Administrator.
![](https://main.qcloudimg.com/raw/225c100597f30cef8af2cbc7ed81c8ac.png)
3. Configure the data source. In the opened Data Source Administrator, select **User DSN** > **Add** > **PostgreSQL Unicode** and configure it.
![](https://main.qcloudimg.com/raw/03fee0de11884517bca025f654727b5a.png)
4. Click **Test** to test the connection. After the test succeeds, click **Save** to save the connection information. After configuring the data source, you can proceed with subsequent development.
![](https://main.qcloudimg.com/raw/22d3aa82b7591b0bbe70acd26495b595.png)
