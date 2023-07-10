## Feature

This API (ModifyShippingTask) is used to modify the existing shipping task. When using this API, you need to manually grant CLS the permission to write to the specified bucket.



#### Request sample

```plaintext
PUT /shipper HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
	"shipper_id": "xxxx-xx-xx-xx-xxxxxxxx",
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
	}
}
```



## Request line

```plaintext
PUT /shipper
```

#### Request headers

No special request header is used except for the common header.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| ------------ | ------ | ---- | -------- | ------------------------------------------------------------ |
| shipper_id | string | body | Yes | ID of the shipping task to be modified |
| bucket | string | body | No | New bucket for the shipping task. Format: {bucketName}-{appid} |
| prefix | string | body | No | Prefix of the new directory for the shipping task |
| shipper_name | string | body | No | Shipping rule name |
| interval     | int    | body | No       | Shipping interval in seconds. Default: 300. Valid values: [300, 360, 420, 480, 540, 600, 660, 720, 780, 840, 900] (equal to integer minutes) |
| max_size | int | body | No | The maximum size of a file to be shipped (in MB). Default is 100 MB. Value range: 100-256 |
| effective | bool | body | No | Indicates whether to enable the shipping task |
| partition | string | body | No | Rules for partitioning logs to be shipped. `Strftime` can be used to define the time format. |
| compress | object | body | No       | Compression configuration of logs to be shipped |
| content | object | body | No | Format configuration of logs to be shipped |

The `compress` format is as follows:

| Field Name | Type | Required | Description |
| ------ | ------ | -------- | ------------------------------------------ |
| format | string | Yes | Compression format, including `gzip`, `lzop` and `none` (do not compress). |

The `content` format is as follows:

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

>At least one of the following fields should be provided: bucket, prefix, shipper_name, interval, max_size, effective, filter_rules, and compress.

## Response

#### Response sample

```plaintext
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
```

#### Response headers

No special response header is used except for common response header.

#### Response parameters

None.

## Error Codes

For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
