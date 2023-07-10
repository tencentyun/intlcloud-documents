## Function decode_url

### Function definition

This function is used to decode an encoded URL.

### Syntax description

```sql
decode_url(value)
```

### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| url | URL value | string | Yes |-|-|

### Sample

Raw log:
```
{"url":"https%3A%2F%2Fcloud.tencent.com%2F"}
```
Processing rule:
```
fields_set("result",decode_url(v("url")))
```
Processing result:
```
{"result":"https://cloud.tencent.com/","url":"https%3A%2F%2Fcloud.tencent.com%2F"}
```

## Function md5_encoding
### Function definition
This function is used to calculate and return the MD5 checksum.

### Syntax description
```
md5_encoding(value)
```

### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| Value |	 The data for which to calculate the MD5 checksum |	String|	 Yes |	-|	-|

### Sample
Raw log:
```
{"field": "haha"}
```
Processing rule:
```
fields_set("field", md5_encoding(v("field")))
```
Processing result:
```
{"field":"4e4d6c332b6fe62a63afe56171fd3725"}
```



## Function uuid
### Function definition
This function is used to generate a universally unique identifier (UUID).

### Syntax description
```
uuid() 
```

### Parameter description
No input parameters

### Sample
Raw log:

```
{"key":"value"}
```

Processing rule:
```
fields_set("field",uuid())
```
Processing result:
```
{"field":"8c2db704-45c0-4ea1-9e2c-cf9c966e35cd","key":"value"}
```
