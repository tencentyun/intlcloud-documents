## Getting All Metrics 
### Request address
The address is the instance IP and port, such as `10.13.20.15:9200`, which can be obtained in the console.

### Request path and method 
Path: `/_metrics`
Method: GET

### Request parameters 
None

### Request content 
None

### Response content 
You need to judge whether a request is successful based on the `error` field. If the response content contains the `error` field, the request failed. For the error details, please see the `error` field description.

### Sample code for curl
Request:
`curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/_metrics`

Response:

```
{
    "result": 
	{
	    "metrics": 
		[
		    "ctsdb_test",
		    "ctsdb_test1"
	    ]
    },
    "status": 200
}
```

## Getting Specified Metric 

### Request address 
The address is the instance IP and port, such as `10.13.20.15:9200`, which can be obtained in the console.

### Request path and method 
Path: `/_metric/${metric_name}`, where `${metric_name}` is the metric name.
Method: GET

### Request parameters
None

### Request content 
None

### Response content 
You need to judge whether a request is successful based on the `error` field. If the response content contains the `error` field, the request failed. For the error details, please see the `error` field description.

### Sample code for curl
Request:
`curl -u root:le201909 -H 'Content-Type:application/json' -X GET 172.16.345.14:9201/_metric/ctsdb_test`

Response:
```
{
    "result": 
	{
	    "ctsdb_test": 
		{
		    "tags": 
			{
		    	"region": "string"
		    },
		    "time": 
			{
			    "name": "timestamp",
			    "format": "epoch_second"
		    },
		    "fields": 
			{
		    	"cpuUsage": "float"
		    },
		    "options": 
			{
			    "expire_day": 7,
			    "refresh_interval": "10s",
			    "number_of_shards": 5
		    }
	    }
    },
    "status": 200
}
```
