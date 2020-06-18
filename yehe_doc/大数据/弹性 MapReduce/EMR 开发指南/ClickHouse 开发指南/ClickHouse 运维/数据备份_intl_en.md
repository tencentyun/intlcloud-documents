The ClickHouse data directory can be configured in the `path` field in `config.xml` by default, and the default directory is `/data/clickhouse/clickhouse-server/data`.

## Data Directory Format

The structure of a `clickhouse-server` data directory is as follows:

```
test
|-- account
|   |-- all_1_1_0
|   |   |-- checksums.txt
|   |   |-- columns.txt
|   |   |-- count.txt
|   |   |-- name.bin
|   |   |-- name.mrk2
|   |   |-- id.bin
|   |   |-- id.mrk2
|   |   |-- age.bin
|   |   |-- age.mrk2
|   |   |-- primary.idx
|   |-- detached
|-- |-- format_version.txt
```

- The first-level directory displays the database name such as `test`.
- The second-level directory is the table name. In the example above, the `account` table exists in the `test` database.
- The third-level directory displays the partition directories.
 - `checksum.txt` stores the data checksum information.
 - `columns.txt` stores the data column names and data types.
 - `count.txt` stores the total number of data entries in the partition.
 - `.bin` and `.mrk2` store the data.

## Data Backup Method

ClickHouse officially provides the `clickhouse-backup` backup tool that can back up the data directories of the `clickhouse-server` process to COS in the public cloud.

#### Step 1. Prepare the config.yml configuration file

Add the COS information such as URL, `secret_id`, `secret_key`, `clickhouse-server` address, and access information to the file. Create a `/etc/clickhouse-backup` directory and move the configuration file into it.
```
general:
remote_storage: cos
disable_progress_bar: false
backups_to_keep_local: 0
backups_to_keep_remote: 0
clickhouse:
username: default
password: ""
host: 127.0.0.1
port: 9000
data_path: ""
skip_tables:
- system.*
timeout: 5m
cos:
url: "https://${bucket-name}.cos.${region}.myqcloud.com"
timeout: 100
secret_id: "xxxxxx"
secret_key: "yyyyy"
path: "/"
compression_format: gzip
compression_level: 1
debug: false
```

#### Step 2. Use the clickhouse-backup tool to create a backup directory

```
$ ./clickhouse-backup create testbak1
# Run `list` to check whether the creation succeeds
$ ./clickhouse-backup list local
- 'testbak1'    (created at 26-03-2020 02:55:23)
```
#### Step 3. Use the clickhouse-backup tool to package data and upload it to COS

After running the following command, check whether the compressed file `testbak1.tar.gz` exists in the corresponding directory in the COS bucket:
```
$ ./clickhouse-backup upload testbak1 2020/03/25 12:58:25 Upload backup 'testbak1' 1.27 MiB / 1.27 MiB [===========================] 100.00% 0s 2020/03/25 12:58:26 Done.
```

## References
[clickhouse-backup tool](https://github.com/AlexAkulov/clickhouse-backup)

