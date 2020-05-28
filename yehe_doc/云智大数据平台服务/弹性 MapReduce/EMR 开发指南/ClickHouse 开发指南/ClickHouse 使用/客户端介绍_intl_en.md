ClickHouse provides two types of client APIs over HTTP and TCP protocols respectively.

## Over HTTP

HTTP is mainly used to support simple lightweight operations and suitable in cross-platform and cross-programming language scenarios. The `clickhouse-server` process on the EMR cluster can start the HTTP service at port 8123 to send simple `GET` requests in order to check whether the service is normal.
```
$ curl http://127.0.0.1:8123
Ok.
```
You can also send requests through `query` parameters. For example, the following sample code is to query data in the `account` table in `testdb`:
```
$ wget -q -O- 'http://127.0.0.1:8123/?query=SELECT * from testdb.account'
1       GHua    WuHan Hubei     1990
2       SLiu    ShenZhen Guangzhou      1991
3       JPong   Chengdu Sichuan 1992
```

For other methods, please see [HTTP Interface](https://clickhouse.tech/docs/en/interfaces/http/).

## Over TCP

TCP is used mainly on `clickhouse-client`. You can enter the `clickhouse-client` command in the EMR cluster to get information such as the version information, address of the connected `clickhouse-server`, and database used by default. **You can run `quit`, `exit`, or `q` to exit.**
```
$ clickhouse-client
ClickHouse client version 19.16.12.49.
Connecting to localhost:9000 as user default.
Connected to ClickHouse server version 19.16.12 revision 54427.
```


**Key parameters used by `clickhouse-client`:**
- -C --config-file: configuration file used by client.
- -h --host: IP address of `clickhouse-server`.
- --port: port address of `clickhouse-server`.
- -u --user: username.
- --password: password.
- -d --database: database name.
- -V --version: displays client version.
- -E --vertical: displays query results in vertical format.
- -q --query: passed-in SQL statement in non-interactive mode.
- -t --time: displays execution time in non-interactive mode.
- --log-level: client log level.
- --send_logs_level: level of log data returned by server.
- --server_logs_file: server log storage path.

For other parameters, please see [Command-line Client](https://clickhouse.tech/docs/en/interfaces/cli/).
