## [Performance Overview](id:xngs)
CTSDB consists of nodes. The specification and number of single nodes determine the processing capacity of the CTSDB instance. In theory:
CTSDB instance read/write concurrency performance = ∑ (single node performance * number of nodes)
Therefore, the higher the node specification and quantity, the higher the processing capacity of the instance. The performance of a single node is mainly subject to CPU and memory. **The specific instance performance is subject to factors such as single node configuration, number of nodes, and number of written fields.**
The test results listed in this document are reference values under specified parameters and only for your reference. To have a better picture, please conduct tests in your real business environment.

## Performance Test 
### Test tool 
[Download the test tool](https://main.qcloudimg.com/raw/5d99924f07ffadfe62109411186718c9.py).

### Directions 
**1. Create a metric**
The command is as follows:
```
    # Create a metric (note that there is only one `host` in `tags`; however, if there are new fields in the written data, they will be automatically put in `tags` as tags)
	curl -u {user}:{passwd} -XPUT {ctsdb_ip_port}/_metric/testa10?pretty -d '{ 
	"tags": {
	"http_code": "string"
	},
	"fields": {"count1":"long","count2":"long","count3":"long","count4":"long","count5":"long","count6":"long","count7":"long","count8":"long","count9":"long","count10":"long"
	},
	"time": {   
	"name": "timestamp",
	"format": "epoch_second"
	},
	"options": { 
	"expire_day": -1, 
	"refresh_interval": "10s",   
	"number_of_shards": 3, 
	"number_of_replicas": 1, 
	"rolling_period": -1
	}
	}'
	# Query a metric
	curl {ctsdb_ip_port}/_metric/testa10?pretty
	# Delete a metric (all corresponding data will also be deleted)
	curl -XDELETE  {ctsdb_ip_port}/_metric/testa10
```

>?Here, `{ctsdb_ip_port}` is the access port of CTSDB, `{user}` the username, and `{passwd}` the password.

**2. Write data**
Write data in bulk by using the script available [here](https://main.qcloudimg.com/raw/5d99924f07ffadfe62109411186718c9.py). The parameters are as detailed below: 
```
 - db_url string
    Instance VIP and Vport (example: 10.02.36.89:9200)
 - metric_name string
    Name of the metric to be written 
 - data_num int
    Number of records to be written by the client at a time
 - threads_nmb int
    Number of concurrent writes 
 - counts int
    Number of fields in a record
```
Modify `userpwd` in line 18 in the script before running it.

Sample code:
```
    python testa.py 10.0.1.10:9200 testa10 4000 9 10
```

Script output: 
It consists of two parts: `params` (option parameters) and `results` (final results).
```
    -------------- params --------------
	put_url http://10.0.1.10:9200/testa10/doc/_bulk
	dataNum: 4000
	threads_nmb: 9
	counts: 10
	-------------- results --------------
	start all threads 2018-12-25 20:10:24

	exit all threads 2018-12-25 20:10:24
	startTime: 1545739824.51
	endTime: 1545739824.55
	diffTime: 0.0414531230927
	wps: 158450.850363

```
>?The average write speed is the output of the `wps` field.

### Performance reference values 
>?You can select any CTSDB node configuration and number of nodes as desired. This document provides reference values of only three instance configurations. You can evaluate the performance of other configurations according to the performance evaluation formula in [Performance Overview](#xngs) or test the performance with a test script. 

Number of concurrent threads: 9 
Number of written fields: 10 

| Single Node Configuration  | Number of Nodes | Write Capacity     |
| :---------- | :----- | :----------- |
| 1 CPU core and 4 GB memory  | 3      | 30,000–50,000 data points per second  |
| 4 CPU cores and 20 GB memory | 3      | 90,000–120,000 data points per second   |
| 8 CPU cores and 40 GB memory | 3      | 110,000–150,000 data points per second  |
