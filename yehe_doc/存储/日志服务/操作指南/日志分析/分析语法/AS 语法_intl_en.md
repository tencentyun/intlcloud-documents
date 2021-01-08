

The `AS` clause is used to specify an alias for a column (KEY).

## AS Syntax Format

```plaintext
* | SELECT column name (KEY) AS  alias
```

## AS Syntax Sample

#### Creating Chinese alias
```plaintext
* | SELECT remote_addr AS "客户端IP", request_time AS "请求时间(单位：秒)" 
```
>! If an alias contains Chinese or other special characters, they should be enclosed in double quotation marks.


#### Counting access requests
```plaintext
* | SELECT COUNT(*) AS PV
```




