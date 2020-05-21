## Feature Description

This API is used to create a shipping task. To use this API, you need to grant CLS the write permission of the specified bucket.

## Request
### Sample request

```
POST /shipper HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
  "topic_id": "xxxx-xx-xx-xx-xxxxxxxx",
  "bucket": "test-1250000001",
  "prefix": "test",
  "shipper_name": "myname",
  "interval": 300,
  "max_size": 256,
  "partition": "%Y%m%d",
  "compress": {
    "format": "none"
  },
  "content": {
    "format": "csv",
    "csv_info": {
      "print_key": true,
      "keys": ["key1", "key2"],
      "delimiter": "|",
      "escape_char": "'",
      "non_existing_field": "null"
    }
  },
  "filter_rules": [{
    "key": "",
    "regex": "",
    "value": ""
  }]
}
```

### Request line

```
POST /shipper
```

### Request header

There are only common request headers but no special request headers.

### Request parameters

| Field Name | Type | Location | Required | Description |
| ------------ | ------ | ---- | ---- | ------------------------------------------------------------ |
| topic_id     | string | body | Yes   | Topic ID of the shipper to be created                               |
| bucket       | string | body | Yes   | Bucket to which the created shipper ships logs, which is in the format of `{bucketName}-{appid}`     |
| prefix       | string | body | Yes   | Directory prefix of the created shipper                                |
| shipper_name | string | body | Yes   | Shipping rule name                                               |
| interval     | int    | body | No   | Shipping time interval in seconds. Default value: 300. Value range: 60–3600            |
| max_size     | int    | body | No   | Maximum size of shipped file in MB. Default value: 256. Value range: 100–10240      |
| custom_uin   | long   | body | No   | Customer `uin` of the shipper to be created. It is retained for compatibility with legacy APIs              |
| filter_rules | array  | body | No   | Filter rules for shipped logs. Only logs matching the rules can be shipped. All rules are in the `and` relationship, and up to five rules can be added. If the array is empty, no filtering will be performed, and all logs will be shipped |
| partition    | string | body | No   | Partition rule of shipped log, which can be represented in `strftime` time format |
| compress     | object | body | No   | Compression configuration of shipped log                                           |
| content      | object | body | No   | Format configuration of shipped log content                                       |

`Rule` is in the following format:

| Field Name | Type | Required | Description |
| ------ | ------ | ---- | ----------------------------------------------------- |
| key    | string | Yes       | Key for comparison. `__CONTENT__` indicate the full text                |
| regex  | string | Yes       | Regex for extracting comparison content                               |
| value  | string | Yes       | Value to be compared with the content extracted with the above regex. If they are the same, there will be a hit |

`compress` is in the following format:

| Field Name | Type | Required | Description |
| ------ | ------ | ---- | ------------------------------------------ |
| format | string | Yes       | Compression format. `gzip` and `lzop` are supported, and `none` indicates no compression |

`content` is in the following format:

| Field Name | Type | Required | Description |
| -------- | ------ | -------- | --------------------------- |
| format   | string | Yes       | Content format. Valid values: `json`, `csv` |
| csv_info | object | No       | Configured when the content format is `csv`       |

`csv_info` is in the following format:

| Field Name | Type | Required | Description |
| ------------------ | ------------- | -------- | ------------------------------------------------ |
| print_key          | bool          | Yes       | Whether to print `key` on the first row of CSV file                              |
| keys               | array(string) | Yes       | Names of each keys                                  |
| delimiter          | string        | Yes       | Field delimiter                                 |
| escape_char        | string        | Yes       | Escape character used to enclose any field delimiter in field content |
| non_existing_field | string        | Yes       | Content used to populate non-existing fields           |


## Response
### Sample response

```
 HTTP/1.1 200 OK
 Content-Type: application/json
 Content-Length: 0
 {
   "shipper_id": "xxxx-xx-xx-xx-xxxxxxxx",
 }
```

### Response header

There are only common response headers but no special response headers.

### Response parameters

| Field Name | Type | Required | Description |
| ---------- | ------ | ---- | ----------------- |
| shipper_id   | string | Yes       | ID of created shipper                                          |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
