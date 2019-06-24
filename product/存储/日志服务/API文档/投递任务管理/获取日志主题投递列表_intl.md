## Description

This API is used to get the details of all shipping policies under a specified log topic.

## Request

### Request example

```shell
 GET /shippers?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
 Host: <Region>.cls.myqcloud.com
 Authorization: <Authorization String>
```

### Request line 

```shell
GET /shippers
```

### Request header

No special request header is used except for the common header.

### Request parameters

| Field Name | Type | Location | Required | Description |
| -------- | ------ | ----- | -------- | ----------------------------- |
| topic_id | string | query | Yes | ID of the topic to which the shipping task to be queried belongs |
| offset | int | query | No | Starting point for query. Default is 0. |
| count | int | query | No | Number of shipping tasks to be queried. Default is 50, and maximum is 1000. |

## Response

### Response example

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "shippers": [
  {
    "shipper_id": "xxxx-xx-xx-xx-xxxxxxxx",
    "topic_id": "yyyy-yy-yy-yy-yyyyyyyy",
    "bucket": "test-1250000001",
    "prefix": "test",
    "shipper_name": "myname",
    "interval": 300,
    "max_size": 256,
    "effective": true,
    "filter_rules": [{
      "key": "",
      "regex": "",
      "value": ""
    }],
    "partition": "%Y%m%d",
    "compress": {
        "format": "none"
    },
    "content": {
        "format": "json"
    },
    "create_time": "2017-12-12 12:12:12"
  }
  ]
}
```

### Response header

No special response header is used except for the common response header.

### Response parameters

| Field Name | Type | Required | Description |
| -------- | --------- | -------- | ------------ |
| shippers | JsonArray | Yes | Array of shipping information |

ShipperInfo is composed as follows: 

| Field Name | Type | Required | Description |
| ------------ | ------ | -------- | -------------------------------------------------- |
| shipper_id | string | Yes | Shipping task ID |
| topic_id | string | Yes | ID of the topic to which shipping rules belong |
| bucket | string | Yes | Address of the bucket to which logs are shipped |
| prefix | string | Yes | The directory to which logs are shipped |
| shipper_name | string | Yes | Shipping rule name |
| interval | int | Yes | Shipping interval (in sec) |
| max_size | int | Yes | The maximum size of a file to be shipped (in MB) |
| effective | bool | Yes | Indicates whether the shipping task configuration takes effect |
| filter_rules | array | Yes | Rules for filtering logs to be shipped |
| create_time | string | Yes | Time when the log to be shipped is created |
| partition | string | Yes | Rules for partitioning logs to be shipped. `Strftime` can be used to define the time format. |
| compress | object | Yes | Compression configuration of logs to be shipped |
| content | object | Yes | Format configuration of logs to be shipped |

filter_rules is composed as follows:

| Field Name | Type | Required | Description |
| ------ | ------ | -------- | ----------------------------------------------------- |
| key | string | Yes | The key used for comparison. `__CONTENT__` means full text. |
| regex | string | Yes | The regular expression used to extract the comparison content |
| value | string | Yes | The value used to compare with the content extracted by using the above regex. The rule is hit if they are consistent. |

compress is composed as follows:

| Field Name | Type | Required | Description |
| ------ | ------ | -------- | ------------------------------------------ |
| format | string | Yes | Compression format, including `gzip`, `lzop` and `none` (do not compress). |

content is composed as follows:

| Field Name | Type | Required | Description |
| -------- | ------ | -------- | --------------------------- |
| format | string | Yes | Content format, which supports `json` and `csv`. |
| csv_info | object | No | Returned when the content format is csv |

csv_info is composed as follows:

| Field Name | Type | Required | Description |
| ------------------ | ------------- | -------- | ------------------------------------------------ |
| print_key | bool | Yes | Indicates whether to write the first line of key to the csv file |
| keys | array(string) | Yes | Key name of each column |
| delimiter | string | Yes | The separator between fields |
| escape_char | string | Yes | Escape characters are used to enclose the separators contained in a field. |
| non_existing_field | string | Yes | It is used to populate the fields specified above that do not exist or are invalid. |

### Error codes

For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).

