
## Request Address 
The address is the instance IP and port, such as `10.13.20.15:9200`, which can be obtained in the console.

## Request Path and Method 
Path: `/_metric/${metric_name}/update`, where `${metric_name}` is the metric name.
Method: PUT

## Request Parameters 
None

## Request Content
The `tags`, `time`, `fields`, and `options` fields are all of the `map` type and optional. For their formats, please see [Creating Metric](https://intl.cloud.tencent.com/document/product/1100/40909). The specific requirements are as detailed below:
tags: you can add tag fields and modify the types of existing tag fields without deleting them.
time: you cannot modify `name` but can modify `format`.
fields: you can add metric fields and modify the types of existing metric fields without deleting them.
`options` attributes are as detailed below:

| Attribute            | Required | Type    | Description                                                         |
| ------------------- | ---- | ------- | ------------------------------------------------------------ |
| expire_day          | No   | integer | data expiration time, which is a non-zero integer. Once expired, the data will be automatically cleared. By default, data never expires |
| refresh_interval    | No   | string  | Data refresh interval, which is 10 seconds by default. The written data can be queried after being refreshed from the memory to disk |
| number_of_shards    | No   | integer | Number of metric shards, which is a positive integer and 3 by default. This parameter can be ignored for small metrics. A large metric can be divided into shards, and each shard can be up to 25 GB in size |
| number_of_replicas  | No   | integer | Number of replicas, which is a non-negative integer; for example, 1 indicates one master and one replica. The default value is 1         |
| rolling_period      | No   | integer | Child metric period (in days), which is a non-zero integer. <br>[When CTSDB stores data](id:rolling), to facilitate data expiration and improve query efficiency, it stores data into child metrics by the specified time interval, which is subject to the data expiration time by default |
| max_string_length   | No   | integer | Maximum length of a custom string, which is a positive integer. Its maximum value is 2^31 - 1, and its default value is 256 |
| default_date_format | No   | string  | Format of the `date` data type of custom tags and fields, which is `strict_date_optional_time` or `epoch_millis` by default |
| indexed_fields      | No   | array   | Fields whose indexes need to be retained in the fields. You can use an array to specify multiple fields   |
| default_type        | No   | string  | Default type of new fields. Its valid values are `tag` and `field`, and its default value is `tag` |

>?
> - As the historical data cannot be modified, after fields are updated, the metric information will not immediately change until the next [child metric](https://intl.cloud.tencent.com/document/product/1100/40909#rolling) is generated. If you want to confirm whether the update is successful, you can call the `GET /_metric/${metric_name}?v` API.
> - Only fields of the `short`, `integer`, `float` data types can be changed to another type. The `short` type can be changed to the `integer` or `long` type, `integer` to `long`, and `float` to `double`.

## Response Content
You need to judge whether a request is successful based on the `error` field. If the response content contains the `error` field, the request failed. For the error details, please see the `error` field description.

## Sample Code for curl
Request:
```
	curl -u root:le201909 -H 'Content-Type:application/json' -X PUT 172.16.345.14:9201/_metric/ctsdb_test/update -d'
	{
		"tags":{
			"set":"string"
		},
		"time":{
			"name":"timestamp",
			"format":"epoch_second"
		},
		"fields":{
			"diskUsage":"float"
		},
		"options":{
		    "expire_day":15,
		    "number_of_shards":10
	    }
    }'
```

Response:
```
{
    "acknowledged": true,
    "message": "update ctsdb metric test111 success!"
}
```
