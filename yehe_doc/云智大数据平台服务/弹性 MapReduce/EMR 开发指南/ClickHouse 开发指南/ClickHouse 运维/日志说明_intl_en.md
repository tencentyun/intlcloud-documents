## ClickHouse Server Log Description	

ClickHouse server log configuration items are in the `config.xml` file in the `/etc/clickhouse-server` directory by default.
```
    <logger>
        <level>trace</level>
        <log>/data/clickhouse/clickhouse-server/logs/clickhouse-server.log</log>
        <errorlog>/data/clickhouse/clickhouse-server/logs/clickhouse-server.err.log</errorlog>
        <size>100M</size>
        <count>10</count>
    </logger>
```

- `level` records the server log level, which can be `trace`, `debug`, `information`, `warning`, or `error`.
- `log` records the file path.
- `errlog` records the error log file path.
- `size` and `count` record the maximum size of historical log file and maximum number of historical log entries that can be retained respectively.

## ClickHouse Client Log Description

When using the `clickhouse-client` command line to run SQL statements, you can set the `send_logs_level` parameter in interactive mode to view the logs of each execution.
```
172.30.1.15 :) set send_logs_level='trace';  
SET send_logs_level = 'trace'
Ok.

0 rows in set. Elapsed: 0.001 sec. 
```

When starting `clickhouse-client`, you can specify the `send_logs_level` and `log-level` parameters.
```
clickhouse-client  --send_logs_level=trace --log-level=trace
```
You can use the command with `--server_logs_file` to save the logs to the specified file.
```
clickhouse-client  --send_logs_level=trace --log-level=trace --server_logs_file='/data/query.log'
```
