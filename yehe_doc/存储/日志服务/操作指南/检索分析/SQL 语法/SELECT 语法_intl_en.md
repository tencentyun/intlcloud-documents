The `SELECT` statement is used to select data from a table. It selects eligible data from the current log topic by default.

## Syntax Format

```plaintext
* | SELECT [Column name(KEY)]
```

## Syntax Example

Select values whose columns (KEY) are `remote_addr` and `method` from the log data:

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

