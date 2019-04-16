## Description

This API is used to modify the existing shipping task. When using this API, you need to manually grant CLS the permission to write to the specified bucket.



### Request example

```
 PUT /shipper HTTP/1.1
 Host: <Region>.cls.myqcloud.com
 Authorization: <AuthorizationString>
 Content-Type: application/json
 
 {
   "shipper_id": "xxxx-xx-xx-xx-xxxxxxxx",
   "bucket": "test-1250000001",
   "prefix": "test",
   "shipper_name": "myname",
   "interval": 300,
   "max_size": 256,
   "effective": true,
   "partition": "%Y%m%d",
     "compress": {
         "format": "none"
     },
     "content": {
         "format": "json",
     },
   "filter_rules": [{
     "key": "",
     "regex": "",
     "value": ""
   }]
 }
```



## Request Line

```
PUT /shipper
```

### Request header

No special request header is used except for the common header.

### Request parameters

| Field Name | Type | Location | Required | Description |
| ------------ | ------ | ---- | ---- | ------------------------------------------------------------ |
| shipper_id | string | body | Yes | ID of the shipping task to be modified |
| bucket | string | body | No | New bucket for the shipping task. Format: {bucketName}-{appid} |
| prefix | string | body | No | Prefix of the new directory for the shipping task |
| shipper_name | string | body | No | Shipping rule name |
| interval | int | body | No | Shipping interval (in sec). Default is 300. Value range: 60-3600 |
| max_size | int | body | No | The maximum size of a file to be shipped (in MB). Default is 256 MB. Value range: 100-10240 |
| effective | bool | body | No | Indicates whether to enable the shipping task |
| filter_rules | array | body | No | Rules for filtering logs to be shipped. Logs that match the rules are shipped. The relation between rules is `and`. The number of rules is limited to 5. If the array is left empty, all logs are shipped without filtering. |
| partition | string | body | No | Rules for partitioning logs to be shipped. `Strftime` can be used to define the time format. |
| compress | object | body | Yes | Compression configuration of logs to be shipped |
| content | object | body | Yes | Format configuration of logs to be shipped |

Rule is composed as follows:

| Field Name | Type | Required | Description |
| ------ | ------ | ---- | ----------------------------------------------------- |
| key | string | Yes | The key used for comparison. `__CONTENT__` means full text. |
| regex | string | Yes | The regular expression used to extract the comparison content |
| value | string | Yes | The value used to compare with the content extracted by using the above regex. The rule is hit if they are consistent. |

compress is composed as follows:

| Field Name | Type | Required | Description |
| ------ | ------ | ---- | ------------------------------------------ |
| format | string | Yes | Compression format, including `gzip`, `lzop` and `none` (do not compress). |

content is composed as follows:

| Field Name | Type | Required | Description |
| -------- | ------ | -------- | --------------------------- |
| format | string | Yes | Content format, which supports `json` and `csv`. |
| csv_info | object | No | Required when the content format is `csv` |

csv_info is composed as follows:

| Field Name | Type | Required | Description |
| ------------------ | ------------- | -------- | ------------------------------------------------ |
| print_key | bool | Yes | Indicates whether to write the first line of key to the csv file |
| keys | array(string) | Yes | Key name of each column |
| delimiter | string | Yes | The separator between fields |
| escape_char | string | Yes | Escape characters are used to enclose the separators contained in a field. |
| non_existing_field | string | Yes | It is used to populate the fields specified above that do not exist or are invalid. |

> At least one of the following fields should be provided: bucket, prefix, shipper_name, interval, max_size, effective, filter_rules, and compress.

## Response

### Response example

```
 HTTP/1.1 200 OK
 Content-Type: application/json
 Content-Length: 0
```

### Response header

No special response header is used except for the common response header.

### Response parameters
None

## Error Codes

For more information, see [Error Codes](https://cloud.tencent.com/document/product/614/12402).

