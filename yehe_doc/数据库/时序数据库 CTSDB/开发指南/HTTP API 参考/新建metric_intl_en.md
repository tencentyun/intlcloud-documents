
## Request Address 
The address is the instance IP and port, such as `10.13.20.15:9200`, which can be obtained in the console.

## Request Path and Method
- Path: `/_metric/${metric_name}`, where `${metric_name}` is the name of the metric to be created.
- Method: PUT

>?For the naming limits of metrics, please see [System Limits](https://intl.cloud.tencent.com/document/product/1100/40910).

## Request Parameters 
None

## Request Content

| Parameter | Required | Type | Description                                                         |
| -------- | ---- | ---- | ------------------------------------------------------------ |
| tags     | Yes   | map  | Tag, which is used to uniquely identify data. It must contain at least one tag and supports the following data types: `text` (string with tokens and full-text index), `string` (string without tokens), `long`, `integer`, `short`, `byte`, `double`, `float`, `date`, and `boolean` <br>The format is `{"region": "string","set":  "long","host": "string"}` |
| time     | No   | map  | Configuration of time column, which is used to store the unique time when data is written into the database, such as `{"name": "timestamp", "format":  "epoch_second"}`. If this parameter is left empty, it will be specified as `{"name": "timestamp", "format":  "epoch_millis"}` by the system by default |
| fields   | No   | map  | Fields for data storage. We recommend you use data types most suitable for your actual business to save the space. The following data types are supported: `string`, `long`, `integer`, `short`, `byte`, `double`, `float`, `date`, and `boolean` <br>Example: `{"cpu_usage":"float"}` |
| options  | No   | map  | Common fine-tuning configuration information <br>Example: `{"expire_day":7,"refresh_interval":"10s","number_of_shards":5,"number_of_replicas":1,"rolling_period":1,"max_string_length": 256,"default_date_format":"strict_date_optional_time","indexed_fields":["host"]}` |


- The `name` of the `time` field is of the `timestamp` type by default. The time formats (`format`) are fully compatible with those in Elasticsearch, such as `epoch_millis` (Unix timestamp in milliseconds), `epoch_second` (Unix timestamp in seconds), `basic_date` (in `yyyyMMdd` format), and `basic_date_time` (in `yyyyMMdd'T'HHmmss.SSSZ` format).
- `options` values and their descriptions:
 - expire_day: data expiration time in days, which is a non-zero integer. Once expired, the data will be automatically cleared. By default, it is the minimum value -1, which indicates that the data will never expire.
 - refresh_interval: data refresh interval, which is 10 seconds by default. The written data can be queried after being refreshed from the memory to disk.
 - number_of_shards: number of metric shards, which is a positive integer and 3 by default. This parameter can be ignored for small metrics. A large metric can be divided into shards, and each shard can be up to 25 GB in size.
 - number_of_replicas: number of replicas, which is a non-negative integer; for example, 1 indicates one master and one replica. The default value is 1.
 - [rolling_period](id:rolling): child metric period (in days), which is a non-zero integer. When CTSDB stores data, to facilitate data expiration and improve query efficiency, it stores data in **child metrics** by the specified time interval, which is subject to the data expiration time by default. The relationships between the default child metric period and data expiration time are as detailed below:
 - max_string_length: maximum length of a custom string, which is a positive integer. Its maximum value is 2^31 - 1, and its default value is 256.
 - default_date_format: format of the `date` data type of custom tags and fields, which is `strict_date_optional_time` or `epoch_millis` by default.
 - indexed_fields: fields whose indexes need to be retained in the fields. You can use an array to specify multiple fields.
 - default_type: default type of new fields. Its valid values are `tag` and `field`, and its default value is `tag`.
<table>
<thead><tr><th>Expiration Time</th><th>Child Metric Period</th></tr></thead>
<tbody>
<tr>
<td>≤ 7 days</td><td>1 day</td></tr>
<tr>
<td>&gt; 7 day and ≤ 20 days</td><td>3 days</td></tr>
<tr>
<td>&gt; 20 days and ≤ 49 days</td><td>7 days</td></tr>
<tr>
<td>&gt; 49 days and ≤ 3 months</td><td>15 days</td></tr>
<tr>
<td>> 3 months</td><td>30 days</td></tr>
<tr>
<td>Never expire</td><td>30 days</td></tr>
</tbody></table>

## Response Content 
You need to judge whether a request is successful based on the `error` field. If the response content contains the `error` field, the request failed. For the error details, please see the `error` field description.

## Sample Code for curl
Request:
```
curl -u root:le201909 -H 'Content-Type:application/json' -X PUT 172.16.345.14:9201/_metric/ctsdb_test -d'
 {
	    "tags":
		{
	    	"region":"string"
	    },
	    "time":
		{
	    	"name":"timestamp",
	    	"format":"epoch_second"
	    },
	    "fields":
		{
	    	"cpuUsage":"float"
	    },
	    "options":
		{
	    	"expire_day":7,
	    	"refresh_interval":"10s",
	    	"number_of_shards":5
	    }
    }
	'
```

Response upon success:
```
	{
	    "acknowledged": true,
	    "message": "create ctsdb metric ctsdb_test success!"
    }
```

Response upon failure:
```
   {
	    "error": {
	    "reason": "table ctsdb_test already exist",
	    "type": "metric_exception"
	    },
	    "status": 201
    }

```

