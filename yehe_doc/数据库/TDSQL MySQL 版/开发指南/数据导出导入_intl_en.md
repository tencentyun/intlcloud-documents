## Exporting Data
TDSQL for MySQL supports exporting data with mysqldump. Before export, you need to set the `net_write_timeout` parameter (`set global net_write_timeout=28800`) in the [TDSQL for MySQL Console](https://console.cloud.tencent.com/dcdb). Note that command line utilities are not authorized by TDSQL for MySQL, so you can set the parameter only in the console.
```
mysqldump --compact --single-transaction --no-create-info -c db_name table_name  -utest -h10.xx.xx.34 -P3336  -ptest123
```

>?The `db` and `table` parameters should be specified based on the actual situation. If the exported data is to be imported into another set of TDSQL for MySQL environment, the `-c` option must be added.


## Importing Data
TDSQL for MySQL provides a professional tool to import data specified by `load data outfile`. This tool shards a source file into multiple files according to the shardkey routing rules, and passes each file through to the corresponding backend database.

[Download the tool](https://tdsqlfilebackup-1252014656.cos.ap-chengdu.myqcloud.com/load_data.tar).

```
[tdengine@TENCENT64 ~/]$./load_data

format:./load_data mode0/mode1 proxy_host proxy_port user password db_table shardkey_index file field_terminate filed_enclosed

example:./load_data mode1 10.xx.xx.10 3336 test test123 shard.table  1 '/tmp/datafile'  ' ' ''
```

>!
>- The source file must use '\n' as a line break.
>- `mode0` means that the source file is sharded but will not be imported, which is usually used for debugging. To import data, use `mode1`.
>- `shardkey_index` starts from 0. If the shardkey is the second field, `shardkey_index` should be 1.

