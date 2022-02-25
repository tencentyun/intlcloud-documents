Cloud Data Warehouse provides two types of client APIs over HTTP and TCP protocols respectively.

## Over HTTP
HTTP is mainly used to support simple lightweight operations and suitable in cross-platform and cross-programming language scenarios. The `clickhouse-server` process on the EMR cluster can start the HTTP service at port 8123 to send simple `GET` requests in order to check whether the service is normal.
```
$ curl http://127.0.0.1:8123Ok.
```
You can also send requests through `query` parameters. For example, the following sample code is to query data in the `account` table in `testdb`:
```
$ wget -q -O- 'http://127.0.0.1:8123/?query=SELECT * from testdb.account'1       GHua    WuHan Hubei     19902       SLiu    ShenZhen Guangzhou      19913       JPong   Chengdu Sichuan 1992
```
For other methods, see [HTTP Interface](https://clickhouse.tech/docs/en/interfaces/http/).

## Over TCP
TCP is used mainly on `clickhouse-client`. You can enter the `clickhouse-client` command in the Cloud Data Warehouse cluster to get information such as the version information, address of the connected `clickhouse-server`, and database used by default. **You can run `quit`, `exit`, or `q` to exit.**
```
$ clickhouse-client
ClickHouse client version 19.16.12.49.
Connecting to localhost:9000 as user default.
Connected to ClickHouse server version 19.16.12 revision 54427.
```
#### Main parameters used by ClickHouse client:

| Parameter | Description  |
|---------|----------|
|  -C --config-file | Specifies the configuration file used by the client |
|  -h --host  | Specifies the ClickHouse server IP address  |
|  --port | Specifies the ClickHouse server port address |
|   -u --user | Username  |
|  --password  | Password  |
|  -d --database | Database name |
|  -V --version | Displays the client version |
|  -E --vertical | Displays query results in vertical format |
|  -q --query | Passes in SQL statements in non-interactive mode |
| -t --time | Displays the execution time in non-interactive mode |
|  --log-level | Client log level |
| --send_logs_level | Specifies the level of log data returned by the server |
|  --server_logs_file | Specifies the server-side log storage path |

For more parameters, see [Command-line Client](https://clickhouse.tech/docs/en/interfaces/cli/).
