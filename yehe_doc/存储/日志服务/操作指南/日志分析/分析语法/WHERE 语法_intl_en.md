

The `WHERE` statement is used to extract the logs that meet the specified conditions.

## WHERE Syntax Format

```sql
SELECT column (KEY)
WHERE column (KEY) operator value
```

The operator can be `=`, `<>`, `>`, `<`, `>=`, `<=`, `BETWEEN`, `IN`, or `LIKE`.

## WHERE Syntax Sample

Query logs with status code greater than 400 in the log data:

```sql
SELECT * 
WHERE status > 400
```

Query the number of logs whose request method is GET and client IP is 192.168.10.101 in the log data:

```sql
SELECT count(*) as count
WHERE method='GET' and remote_addr='192.168.10.101'
```

Count the average size of requests with the URL suffix of .mp4:

```sql
SELECT round(sum(body_bytes_sent) / count(body_bytes_sent), 2) AS avg_size  WHERE url like '%.mp4'
```
