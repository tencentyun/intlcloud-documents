

The `LIMIT` clause is used to limit the amount of data returned by the `SELECT` statement.

## LIMIT Syntax Format

Read the first `count` rows:

```plaintext
LIMIT count
```
>!`LIMIT` doesn't support the `[offset] rows` syntax.


## LIMIT Syntax Sample

Sort the request status code logs in descending order and only get the first 10 rows:

```plaintext
* | SELECT status, COUNT(status) as ct ORDER BY status DESC LIMIT 10
```
