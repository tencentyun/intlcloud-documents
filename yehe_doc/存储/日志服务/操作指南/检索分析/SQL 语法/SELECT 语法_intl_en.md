The `SELECT` statement is used to select data from a table. It selects eligible data from the current log topic by default.

## Syntax Format

```plaintext
* | SELECT [Column name(KEY)]
```

## Syntax Example

Select values with columns (KEY) being `remote_addr` and `method` from the log data:

```plaintext
* | SELECT remote_addr, method 
```

Select all columns (KEY) from the log data:

```plaintext
* | SELECT *
```

`SELECT` can also be followed by arithmetic expressions; for example, you can query the download speed of log data:

Download speed (`speed`) = total number of bytes sent (`body_bytes_sent`) / request time (`request_time`)

```plaintext
* | SELECT body_bytes_sent / request_time AS speed
```

## Column Naming Conventions

In SQL specifications, a column name consists of letters, digits, and underscores and starts with a letter, such as `remote_addr`. If a field in a log has a non-compliant name, you need to surround the name by `""`. You can also specify an alias for the field with [AS syntax](https://intl.cloud.tencent.com/document/product/614/38731) in SQL.

If a log field is named `remote_addr`, which conforms to SQL's column naming conventions, it can be queried by SELECT:

```
* | SELECT remote_addr
```

If a log field is named `__TAG__.pod_label_qcloud-app`, which does not conform to SQL's column naming conventions, it needs to be surrounded by `""`:

```
* | SELECT "__TAG__.pod_label_qcloud-app"
```

If a log field is named `__TIMESTAMP__`, which does not conform to SQL's column naming conventions, it needs to be surrounded by `""` and specified with an alias through the AS syntax:

```
* | SELECT "__TIMESTAMP__" AS log_time
```

