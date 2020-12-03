## Feature Description

This API is used to get the detailed list of shipping policies of a specified log topic.

## Request

#### Sample request

```plaintext
GET /shippers?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <Authorization String>
```

#### Request line 

```plaintext
GET /shippers
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| -------- | ------ | ----- | -------- | ----------------------------- |
| topic_id | string | query | Yes       | Topic ID to the shipper to be queried |
| offset   | int    | query | No       | Query start position. Default value: 0         |
| count    | int    | query | No       | Number of entries to be queried. Default value: 50. Maximum value: 1000  |

## Response

#### Sample response

```plaintext
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
    "max_size": 100,
    "effective": true,
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

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
| -------- | --------- | -------- | ------------ |
| shippers | JsonArray | Yes       | Shipping information array |

`ShipperInfo` is in the following format: 

| Field Name | Type | Required | Description |
| ------------ | ------ | -------- | -------------------------------------------------- |
| shipper_id   | string | Yes       | Shipper ID                                          |
| topic_id     | string | Yes       | Topic ID of shipping rule                            |
| bucket       | string | Yes       | Bucket address shipped to                                 |
| prefix       | string | Yes       | Shipping prefix directory                                     |
| shipper_name | string | Yes       | Shipping rule name                                     |
| interval     | int    | Yes       | Shipping time interval in seconds                            |
| max_size     | int    | Yes       | Maximum size of shipped file in MB                        |
| effective    | bool   | Yes       | Whether it is effective                                           |
| create_time  | string | Yes       | Creation time of shipped log                                 |
| partition    | string | Yes       | Partition rule of shipped log, which can be represented in `strftime` time format |
| compress     | object | Yes       | Compression configuration of shipped log                                 |
| content      | object | Yes       | Format configuration of shipped log content                             |

`compress` is in the following format:

| Field Name | Type | Required | Description |
| ------ | ------ | -------- | ------------------------------------------ |
| format | string | Yes       | Compression format. gzip and lzop are supported, and `none` indicates no compression |

`content` is in the following format:

| Field Name | Type | Required | Description |
| -------- | ------ | -------- | --------------------------- |
| format   | string | Yes       | Content format. Valid values: json, csv |
| csv_info | object | No       | Returned when the content format is `csv`        |

`csv_info` is in the following format:

| Field Name | Type | Required | Description |
| ------------------ | ------------- | -------- | ------------------------------------------------ |
| print_key          | bool          | Yes       | Whether to print `key` on the first row of CSV file                              |
| keys               | array(string) | Yes       | Names of each keys                                  |
| delimiter          | string        | Yes       | Field delimiter                                 |
| escape_char        | string        | Yes       | Escape character used to enclose any field delimiter in field content |
| non_existing_field | string        | Yes       | Content used to populate non-existing fields           |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
