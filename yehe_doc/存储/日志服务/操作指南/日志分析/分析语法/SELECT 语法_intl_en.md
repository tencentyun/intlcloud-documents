

The `SELECT` statement is used to select data from a table.

## Syntax Format

```plaintext
* | SELECT column (KEY)
```

__BLANK__and__BLANK__

```plaintext
* | SELECT *
```

>? SQL statements are case insensitive, so `SELECT` is equivalent to `select`.
>

## Syntax Examples

Select values whose columns (KEY) are `remote_addr` and `method` from the log data. The columns should be separated by comma:

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

>! When logs are searched, a search statement is used; when logs are analyzed, an analysis statement is used. The backend distinguishes between them by whether the input query statement starts with the `SELECT` keyword:
>- If a query statement starts with `SELECT`, such as `SELECT method, request_size GROUP BY method`, then it is considered an SQL analysis statement.
>- If a query statement does not start with `SELECT`, such as `method:GET`, then it is considered a search statement.
