The `WHERE` statement is used to extract the logs that meet the specified conditions.

## Syntax Format

```plaintext
* | SELECT column (KEY) WHERE column (KEY) operator value
```

The operator can be `=`, `<>`, `>`, `<`, `>=`, `<=`, `BETWEEN`, `IN`, or `LIKE`.

>!
> - In SQL, search conditions deliver higher performance than filters. You are advised to use search conditions to meet data filtering requirements. For example, you can use `status:>400 | select count(*) as logCounts` instead of `* | select count(*) as logCounts where status>400` to get the statistical result faster.
> - The `WHERE` statement does not allow the `AS` clause. For example, if `level:* | select level as log_level where log_level='ERROR'` is run, an error will be reported because the statement does not comply with the SQL-92 specifications.
>

## Syntax Example

Query logs with status code greater than 400 in the log data:

```plaintext
* | SELECT * WHERE status > 400
```

Query the number of logs whose request method is GET and client IP is 192.168.10.101 in the log data:

```plaintext
* | SELECT count(*) as count WHERE method='GET' and remote_addr='192.168.10.101'
```

Count the average size of requests with the URL suffix of .mp4:

```plaintext
* | SELECT round(sum(body_bytes_sent) / count(body_bytes_sent), 2) AS avg_size  WHERE url like '%.mp4'
```
