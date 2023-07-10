## Feature

This API is used to create a shipping task. When using this API, you need to manually grant CLS the permission to write to the specified bucket.

## Request

#### Request samples

```plaintext
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
  "max_size": 100,
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
  }
}
```

#### Request line

```
POST /shipper
```

#### Request headers

No special request header is used except for the common header.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| ------------ | ------ | ---- | -------- | ------------------------------------------------------------ |
| topic_id | string | body | Yes | ID of the topic to which the shipping task to be created belongs |
| bucket | string | body | Yes | Shipping bucket of the shipping task to be created. Format: {bucketName}-{appid} |
| prefix | string | body | Yes | Prefix of the shipping directory of the shipping task to be created |
| shipper_name | string | body | Yes | Shipping rule name |
| interval     | int    | body | No       | Shipping interval in seconds. Default: 300. Valid values: [300, 360, 420, 480, 540, 600, 660, 720, 780, 840, 900] (equal to integer minutes) |
| max_size | int | body | No | The maximum size of a file to be shipped (in MB). Default is 100 MB. Value range: 100-256 |
| partition | string | body | No | Rules for partitioning logs to be shipped. `Strftime` can be used to define the time format. |
| compress | object | body | No | Compression configuration of logs to be shipped |
| content | object | body | No | Format configuration of logs to be shipped |

compress is composed as follows:

| Field Name | Type | Required | Description |
| ------ | ------ | -------- | ------------------------------------------ |
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

## Response

#### Response sample

```plaintext
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
{
 "shipper_id": "xxxx-xx-xx-xx-xxxxxxxx",
}
```

#### Response headers

No special response header is used except for the common response header.

#### Response parameters

| Field Name | Type | Required | Description |
| ---------- | ------ | -------- | ----------------- |
| shipper_id | string | Yes | ID of the new shipping task |

## Error Codes

For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
