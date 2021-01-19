

The `AS` clause is used to specify an alias for a column (KEY).

## AS Syntax Format

```sql
SELECT column (KEY) AS  alias
```

## AS Syntax Sample

#### Creating Chinese alias
```sql
SELECT remote_addr AS "客户端IP", request_time AS "请求时间(单位：秒)" 
```
>! If an alias contains Chinese or other special characters, they should be enclosed in double quotation marks.


#### Counting access requests
```sql
SELECT COUNT(*) AS PV
```




