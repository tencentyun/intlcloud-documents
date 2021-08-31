
CTSDB instances currently can be connected to only in VPCs. You can connect to an instance in the console or through RESTful APIs. In the latter case, you need to provide the root account password to ensure security.

Below is a code sample for connecting to an instance and creating a metric through curl. Here, `${user:password}` is the username and password of the instance, `${vip}:${vport}` the IP and port, and `${metric_name}` the name of the created metric. For parameter descriptions, please see [Creating Metric](https://intl.cloud.tencent.com/document/product/1100/40909).

```
   curl -u ${user:password} -H 'Content-Type:application/json' -X PUT ${vip}:${vport}/_metric/${metric_name} -d'
	 { 
	    "tags": {
	        "region": "string",
	        "set":  "long",
	        "host": "string"
	    },
	    "time": {
	         "name": "timestamp",
	         "format": "epoch_second"
	    },
	    "fields": {
	        "cpu_usage":  "float"
	    },
	    "options": {
	        "expire_day": 7,
	        "refresh_interval": "10s",
	        "number_of_shards": 5,
	        "number_of_replicas": 1,
	        "rolling_period": 1
	    }
	}'
```

