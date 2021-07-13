
## Bulk Writing Data into Single Metric
This API can be used to write data records into a single metric either in bulk or not. To improve the write efficiency, we recommend you write data in bulk.

### Request address 
The address is the instance IP and port, such as `10.13.20.15:9200`, which can be obtained in the console.

### Request path and method 
Request path: `/${metric_name}/doc/_bulk`, where `${metric_name}` is the metric name.
Method: POST

>?The `doc` keyword is the `_type` of the written data and must be added to facilitate subsequent system parsing and upgrade.

### Request parameters
You can set the `filter_path` parameter to filter and simplify the returned results. For more information, please see [Batch Querying Data](https://intl.cloud.tencent.com/document/product/1100/40903).

### Request content
You need to bulk write data as structured data in NDJSON format into a metric, which is similar to the following:

```
Metadata\n
Data to be written\n
....
Metadata\n
Data to be written\n
```

The format of the metadata is as shown below:

```
{ 
	"index" : 
	{ 
		"_id" : "1", 			   # Document ID (optional)
		"_routing": "sh"			# Routing value (optional)
	}
}
```

The format of the written data is as shown below:

```
 { 
	"field1" : "value1",
	"field2" : "value2"
 }
```

>!When writing data, you can set the `_routing` parameter to specify the shards where data to be written. This parameter is optional and can be specified to any value. You can specify the same `_routing` value for different data records to route them into the same shard. In addition, if you specify an already set `_routing` parameter value during a query, the system will query data in the specified shard, which can greatly accelerate the query. You need to add a line break at the end of the request body.

### Response content 
You should note that the returned result of the bulk data write API is different from those of other APIs. Please pay attention to the `errors` (not `error`) field in the JSON result first. If it is `false`, all data records were successfully written; if it is `true`, some data records failed to be written, and you can get the failure details from the `items` field.
The `items` field is an array, where each element corresponds to a write request. You can check whether each element has the `error` field to judge whether the corresponding request is successful. If the `error` field exists, the request failed. The specific error information is in the `error` field. If the `error` field doesn't exist, the request succeeded.

### Sample code for curl 
**Sample response upon success:**
Request:
```
curl -u root:le201909 -H 'Content-Type:application/json' -X POST 172.16.345.14:9201/ctsdb_test/doc/_bulk -d'
{"index":{"_routing": "sh" }}
{"region":"sh","cpuUsage":2.5,"timestamp":1505294654}
{"index":{"_routing": "sh" }}
{"region":"sh","cpuUsage":2.0,"timestamp":1505294654}
'
```

Response:
```
{
    "took": 134,
    "errors": false,
    "items": 
	[
	    {
		    "index": 
			{
			    "_index": "ctsdb_test@1505232000000_1",
			    "_type": "doc",
			    "_id": "AV_8eeo_UAkC9PF9L-2q",
			    "_version": 1,
			    "result": "created",
			    "_shards":
				 {
				    "total": 2,
				    "successful": 2,
				    "failed": 0
			    },
			    "created": true,
			    "status": 201
			    }
		    },
		    {
		    "index": 
			{
			    "_index": "ctsdb_test2@1505232000000_1",
			    "_type": "doc",
			    "_id": "AV_8eeo_UAkC9PF9L-2r",
			    "_version": 1,
			    "result": "created",
			    "_shards": 
				{
				    "total": 2,
				    "successful": 2,
				    "failed": 0
			    },
			    "created": true,
			    "status": 201
		    }
	    }
    ]
}
```

>?The `errors` value returned above is `false`, indicating that all data records were successfully written. The `items` array indicates the write result of each record in the same order as in the `bulk` request. For single records in `items`, the `status` of `2XX` indicates that the record was successfully written. `_index` indicates the [child metric](https://intl.cloud.tencent.com/document/product/1100/40909#rolling) where the data was written, and `_shards` indicates the replica write status. In the above sample, `total` indicates two replicas, and `successful` indicates that data was successfully written into both replicas.

**Sample response upon failure:**
Request:

```
curl -u root:le201909 -H 'Content-Type:application/json' -X POST 172.16.345.14:9201/hcbs_client_trace/doc/_bulk -d'
{"index":{"_type":"type"}}
{"vol_id":"c57e008c-0ae0-41cd-8da8-6989d0522fc6","io_type":2,"data_len":4096,"latency":3,"try_times":1,"errcode":0,"start_time":1503404266}
{"index":{"_type":"type"}}
{"vol_id":"c57e008c-0ae0-41cd-8da8-6989d0522fc6","io_type":"abc","data_len":4096,"latency":1,"try_times":1,"errcode":0,"start_time":1503404266}
'
```

Response:
```
{
  "took": 7,
  "errors": true,
  "items": [
    {
      "index": {
        "_index": "hcbs_client_trace",
        "_type": "type",
        "_id": "AWMe9r9lNifptzIWMVPT",
        "_version": 1,
        "result": "created",
        "_shards": {
          "total": 2,
          "successful": 2,
          "failed": 0
        },
        "created": true,
        "status": 201
      }
    },
    {
      "index": {
        "_index": "hcbs_client_trace",
        "_type": "type",
        "_id": "AWMe9r9lNifptzIWMVPU",
        "status": 400,
        "error": {
          "type": "mapper_parsing_exception",
          "reason": "failed to parse [io_type]",
          "caused_by": {
            "type": "number_format_exception",
            "reason": "For input string: \"abc\""
          }
        }
      }
    }
  ]
}
```

>?The `errors` value returned above is `true`, indicating that some data records failed to be written. The `items` array indicates the write result of each record in the same order as in the `bulk` request. For single records in `items`, the `status` of `2XX` indicates that the record was successfully written. The `error` field indicates the detailed error information. `_index` indicates the child metric where the data was written, and `_shards` indicates the replica write status. In the above sample, `total` indicates two replicas, and `successful` indicates that data was successfully written into both replicas.

## Bulk Writing Data into Multiple Metrics
This API can be used to write data records into multiple metrics either in bulk or not. To improve the write efficiency, we recommend you write data in bulk.

### Request address
The address is the instance IP and port, such as `10.13.20.15:9200`, which can be obtained in the console.

### Request path and method
Request path: `_bulk`
Method: PUT

>?The `doc` keyword is the `_type` of the written data and must be added to facilitate subsequent system parsing and upgrade.

### Request parameters 
You can set the `filter_path` parameter to filter and simplify the returned results. For more information, please see [Batch Querying Data](https://intl.cloud.tencent.com/document/product/1100/40903).

### Request content
You need to bulk write data as structured data in NDJSON format into a metric, which is similar to the following:
```
Metadata\n
Data to be written\n
....
Metadata\n
Data to be written\n
```

The format of the metadata is as shown below:
```
{ 
	"index" : 
	{ 
		"_index" :"metric_name",	# Metric where data is to be written
		"_type" : "doc",			# Document type of the data to be written
		"_id" : "1", 			   # Document ID (optional)
		"_routing": "sh"			# Routing value (optional)
	}
}
```
The format of the written data is as shown below:

```
 { 
	"field1" : "value1",
	"field2" : "value2"
}
```
>?When writing data, you can set the `_routing` parameter to specify the shards where data to be written. This parameter is optional and can be specified to any value. You can specify the same `_routing` value for different data records to route them into the same shard. In addition, if you specify an already set `_routing` parameter value during a query, the system will query data in the specified shard, which can greatly accelerate the query. Note that you need to add a line break at the end of the request body.

### Response content 
You need to judge whether a request is successful based on the `error` field. If the response content contains the `error` field, the request failed. The specific error information is in the `error` field. Note: if the request succeeded but the `errors` (not `error`) field is not `false`, the specific data that failed to be written is indicated in the `errors` field.

### Sample code for curl 
Request:
```
curl -u root:le201909 -H 'Content-Type:application/json' -X PUT 172.16.345.14:9201/_bulk -d'
{"index":{"_index" : "ctsdb_test", "_type" : "doc", "_routing": "sh" }}
{"region":"sh","cpuUsage":2.5,"timestamp":1505294654}
{"index":{"_index" : "ctsdb_test2", "_type" : "doc", "_routing": "sh" }}
{"region":"sh","cpuUsage":2.0,"timestamp":1505294654}
'
```

Response:
```
{
    "took": 134,
    "errors": false,
    "items": 
	[
	    {
		    "index": 
			{
			    "_index": "ctsdb_test@1505232000000_1",
			    "_type": "doc",
			    "_id": "AV_8eeo_UAkC9PF9L-2q",
			    "_version": 1,
			    "result": "created",
			    "_shards":
				 {
				    "total": 2,
				    "successful": 2,
				    "failed": 0
			    },
			    "created": true,
			    "status": 201
			    }
		    },
		    {
		    "index": 
			{
			    "_index": "ctsdb_test2@1505232000000_1",
			    "_type": "doc",
			    "_id": "AV_8eeo_UAkC9PF9L-2r",
			    "_version": 1,
			    "result": "created",
			    "_shards": 
				{
				    "total": 2,
				    "successful": 2,
				    "failed": 0
			    },
			    "created": true,
			    "status": 201
		    }
	    }
    ]
}
```

>?The `errors` value returned above is `false`, indicating that all data records were successfully written. The `items` array indicates the write result of each record in the same order as in the `bulk` request. For single records in `items`, the `status` of `2XX` indicates that the record was successfully written. `_index` indicates the child metric where the data was written, and `_shards` indicates the replica write status. In the above sample, `total` indicates two replicas, and `successful` indicates that data was successfully written into both replicas.
