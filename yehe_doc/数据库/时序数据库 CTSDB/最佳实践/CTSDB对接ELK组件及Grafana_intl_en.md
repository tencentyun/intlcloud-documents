## Overview 
CTSDB is a distributed and scalable time series database that supports near-real time data search and analysis. It is compatible with components in the ELK ecosystem, so you can conveniently connect your ELK components to CTSDB.
ELK ecosystem components provide a wide variety of data processing capabilities such as data collection, data cleansing, and visualized graph display. Common ELK components include Filebeat, Logstash, and Kibana. In addition, CTSDB also allows you to use Grafana as the visualized platform. A common architecture is as shown below: 
![](https://main.qcloudimg.com/raw/995ab29d6eb7ad7ce9472961776dfd07.png)

## Component Usage 
### Filebeat 
Filebeat is a lightweight open-source log file data collector and is installed on servers as an agent. It reads file content, sends the content to Logstash for parsing, and then transfers the parsed content to CTSDB, or directly sends the file content to CTSDB for centralized storage and analysis.
#### Filebeat directions 
1. **Install** 
For more information on how to install Filebeat, please see [Filebeat quick start: installation and configuration](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-installation.html).
2. **Configure** 
Filebeat configurations are in a YAML file, including the global, input, and output configurations. The following section provides a usage example.
3. **Start**
When starting Filebeat, you can specify the path of the configuration file; otherwise, `filebeat.yml` will be used by default.

#### Filebeat usage example 
1. First, decompress the Filebeat installation package into a directory as shown below: 
![](https://main.qcloudimg.com/raw/62440378c4f5dbde3169363178491623.png)
2. Then, configure `filebeat.yml`. The following sample is for reference: 
```
filebeat.shutdown_timeout: 5 # How long filebeat waits on shutdown for the publisher to finish.
max_procs: 4 # Maximum number of CPUs that can run concurrently, which is the number of available logical CPUs of the OS by default
filebeat.spool_size: 102400
filebeat.idle_timeout: 2s
processors:
  drop_fields: # Fields to be dropped
  fields: ["beat","input_type","source","offset"]
filebeat.prospectors:
  paths: ["/data/log/filebeat-tutorial.log"]   # Path of the sample data
  fields:
    metricname: metric1
  harvester_buffer_size: 1638400
  close_timeout: 0.5h
  scan_frequency: 2s
  paths: ["/mylog/*.log","/mylog1/*.log"]
  fields:
    metricname: table2
  harvester_buffer_size: 1638401
  close_timeout: 0.5h
  scan_frequency: 2s
output.elasticsearch:
  hosts: ["127.0.0.1:9200"]
  index: "%{[fields.indexname]}"  # Wildcard, which can be used to write different indexes for different types of data
  username: "root" # For CTSDB instances that require authentication, you need to enter the username and password
  password: "changeme"
  worker: 2 # Number of worker threads
  loadbalance: true # Whether to enable load balancing
  bulk_max_size: 512 # Maximum number of documents in one `bulk` request
  flush_interval: 2s
  template:
    enabled: false  # Note: after start, Filebeat will put a default template. When connecting to CTSDB, you need to disable the Filebeat template
```
Some sample data is as shown below: 
```
83.149.9.216 - - [04/Jan/2015:05:13:42 +0000] "GET /presentations/logstash-monitorama-2013/images/kibana-search.png HTTP/1.1" 200 203023 "http://semicomplete.com/presentations/logstash-monitorama-2013/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/32.0.1700.77 Safari/537.36" 
83.149.9.216 - - [04/Jan/2015:05:13:42 +0000] "GET /presentations/logstash-monitorama-2013/images/kibana-dashboard3.png HTTP/1.1" 200 171717 "http://semicomplete.com/presentations/logstash-monitorama-2013/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/32.0.1700.77 Safari/537.36" 
83.149.9.216 - - [04/Jan/2015:05:13:44 +0000] "GET /presentations/logstash-monitorama-2013/plugin/highlight/highlight.js HTTP/1.1" 200 26185 "http://semicomplete.com/presentations/logstash-monitorama-2013/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/32.0.1700.77 Safari/537.36"
```
3. Start Filebeat and observe the data in the corresponding CTSDB metric: 
```
nohup ./filebeat &
    	less logs/filebeat # View certain logs. Through the log `libbeat.es.published_and_acked_events=100`, you can see that all 100 logs have been successfully written into Elasticsearch
    	2018-05-25T14:32:24+08:00 INFO Non-zero metrics in the last 30s: filebeat.harvester.open_files=1 filebeat.harvester.running=1 filebeat.harvester.started=1 libbeat.es.call_count.PublishEvents=1 libbeat.es.publish.read_bytes=1535 libbeat.es.publish.write_bytes=40172 libbeat.es.published_and_acked_events=100 libbeat.publisher.published_events=100 publish.events=101 registrar.states.current=1 registrar.states.update=101 registrar.writes=2
    
    	# Check whether there is data written into `metric1` through Kibana or curl    
    	# Command:    
    	GET metric1/_search
    	{
    	  "sort": [
    	{
    	  "@timestamp": {
    	"order": "desc"
    	  }
    	}
    	  ], 
    	  "docvalue_fields": ["@timestamp", "message"]
    	}
    	# Result:
    	{
    	  "took": 2,
    	  "timed_out": false,
    	  "_shards": {
    	"total": 3,
    	"successful": 3,
    	"skipped": 0,
    	"failed": 0
    	  },
    	  "hits": {
    	"total": 100,
    	"max_score": null,
    	"hits": [
    	  {
    	"_index": "metric1@1525536000000_30",
    	"_type": "doc",
    	"_id": "AWOV_o1wBzkw2jsSfrLN",
    	"_score": null,
    	"fields": {
    	  "@timestamp": [
    	1527229914629
    	  ],
    	  "message": [
    	"218.30.103.62 - - [04/Jan/2015:05:27:57 +0000] \"GET /blog/geekery/c-vs-python-bdb.html HTTP/1.1\" 200 11388 \"-\" \"Sogou web spider/4.0(+http://www.sogou.com/docs/help/webmasters.htm#07)\""
    	  ]
    	},
    	"sort": [
    	  1527229914629
    	]
    	  },
    	# As the content is too much, it is omitted here. In `hits.total`, you can see that the query hit 100 documents, indicating that all the 100 logs have been successfully written into CTSDB
```
The above sample directly uses Filebeat to write the original log data into CTSDB without parsing the fields. The following section describes how to use Logstash to parse data and then write parsed data into CTSDB.

### Logstash  
Logstash is an open-source data collection engine that can parse data in real time. It can collect data from various sources, filter, analyze, and format the data, and then store the data into CTSDB.

#### Logstash directions  
1. **Install** 
For more information on how to install Logstash, please see [Installing Logstash](https://www.elastic.co/guide/en/logstash/current/installing-logstash.html). 
2. **Configure** 
Logstash configurations mainly include three modules: data source input, data parsing rule, and data output. The following section provides a usage example.
3. **Start**
When starting Logstash, you can specify the configuration file; otherwise, `logstash.yml` will be used as the configuration by default, and configuration in `pipelines.yml` will be used as the parsing rule by default.

#### Logstash usage example 
1. First, decompress the Logstash installation package into a directory as shown below: 
![](https://main.qcloudimg.com/raw/f1e07839951e7a7cb4f7d053ba7153af.png)
2. Then, create a configuration file. You can also configure in `logstash.yml` and `pipelines.yml`. In this example, create a configuration file named `first-pipeline.conf` and configure it as follows: 
```
# Input source
input {
	beats {
		port => "5044"
	}
}
# Parse and filter
filter {
	grok {
		match => {
			"message" => "%{COMBINEDAPACHELOG}"
		}
	}
}
# Output
output {
	elasticsearch {
		action => "index"
		hosts => ["localhost:9200"]
		index => "logstash_metric" # Name of the metric created in CTSDB
		document_type => "doc"
		user => "root" # For CTSDB instances that require authentication, you need to specify the username and password
		password => "changeme"
	}
}
```
The Grok filter plugin is available in Logstash by default and can parse unstructured data into structured data. For more information on how to use it, please see [Grok filter plugin](https://www.elastic.co/guide/en/logstash/6.2/plugins-filters-grok.html).
3. Start Logstash and Filebeat and observe the data in the corresponding CTSDB metric:
```
  # Here, you should note that the Filebeat output is Logstash; therefore, you need to modify the Filebeat output configuration item as follows:
	output.logstash:
	  hosts: ["localhost:5044"]
	# Clear the `data` directory of Filebeat and start Filebeat
	rm data/registry
	nohup ./filebeat &
	# Start Logstash
	nohup bin/logstash -f first-pipeline.conf --config.reload.automatic &
	# Check whether there is data written into `metric1` through Kibana or curl	
	# Command:
	GET logstash_metric/_search
	{
	  "sort": [
	    {
	      "@timestamp": {
	        "order": "desc"
	      }
	    }
	  ], 
	  "docvalue_fields": ["@timestamp","request", "response", "type", "bytes",  "verb", "agent", "clientip"]
	}
# Result: 
	{
	  "took": 0,
	  "timed_out": false,
	  "_shards": {
	    "total": 0,
	    "successful": 0,
	    "skipped": 0,
	    "failed": 0
	  },
	  "hits": {
	    "total": 0,
	    "max_score": 0,
	    "hits": []
	  }
	}
	# Here, you can see that the result is empty, indicating that there is no data written into CTSDB. View Logstash logs:
	[2018-05-25T21:00:07,081][ERROR][logstash.outputs.elasticsearch] Encountered a retryable error. Will Retry with exponential backoff  {:code=>403, :url=>"http://127.0.0.1:9200/_bulk"}
	[2018-05-25T21:00:07,081][ERROR][logstash.outputs.elasticsearch] Encountered a retryable error. Will Retry with exponential backoff  {:code=>403, :url=>"http://127.0.0.1:9200/_bulk"}
	# `bulk` processing was exceptional, and permission error 403 was returned. However, a careful check of the username and password found no problem. Continue to check the Elasticsearch logs:
	[2018-05-25T20:59:27,545][WARN ][o.e.p.o.OPackActionFilter] [1505480279000001609] process index failed: Invalid format: "2018-05-25T12:51:18.905Z"
	[2018-05-25T20:59:27,547][WARN ][o.e.p.o.OPackActionFilter] [1505480279000001609] process index failed: Invalid format: "2018-05-25T12:51:18.905Z"
	# The Elasticsearch logs show that an error occurred whiling parsing the time format, and the cause is that the time field format was not specified during metric creation. The default time format in CTSDB is `epoch_millis`, therefore, you need to change the time format:
	POST /_metric/logstash_metric/update?pretty
	{
	  "time": {                           
	         "name": "@timestamp",
	         "format": "strict_date_optional_time"
	    }
	}
	# Restart Logstash and Filebeat, write data again, and check CTSDB:
	# Result
	{
	  "took": 2,
	  "timed_out": false,
	  "_shards": {
	    "total": 3,
	    "successful": 3,
	    "skipped": 0,
	    "failed": 0
	  },
	  "hits": {
	    "total": 100,
	    "max_score": null,
	    "hits": [
	      {
	        "_index" : "logstash_metric@1527004800000_30",
	        "_type" : "doc",
	        "_id" : "AWOvG0YgQoCkIV2BLcov",
	        "_score" : null,
	        "fields" : {
	          "request" : [
	            "/blog/tags/puppet?flav=rss20"
	          ],
	          "agent" : [
	            "\"UniversalFeedParser/4.2-pre-314-svn +http://feedparser.org/\""
	          ],
	          "@timestamp" : [
	            1527651156725
	          ],
	          "response" : [
	            "200"
	          ],
	          "bytes" : [
	            14872
	          ],
	          "clientip" : [
	            "46.105.14.53"
	          ],
	          "verb" : [
	            "GET"
	          ],
	          "type" : [
	            "log"
	          ]
	        },
	        "sort" : [
	          1527651156725
	        ]
	      },
	    ... ...
	    # As the content is too much, it is omitted here. In `hits.total`, you can see that the query hit 100 documents, indicating that all the 100 logs have been successfully written into CTSDB
```
As can be seen from the above sample, logs are collected by Filebeat into Logstash, parsed by Logstash into multiple fields, and then written into CTSDB.

### Kibana  
Kibana is an open-source analysis and visualization platform designed for Elasticsearch. You can use it to search, view, and interact with the data stored in CTSDB metrics. Its diverse features such as graphs, forms, and curves help you visualize and analyze data easily.

#### Kibana directions 
1. **Install**
Download a Kibana version matching Elasticseach and decompress it into a directory.
2. **Configure**
Kibana configuration is simple, and a sample will be provided in the following section. For descriptions of the configuration items, please see [Configure Kibana](https://www.elastic.co/guide/en/kibana/current/settings.html).
3. **Run**
When Kibana runs, `config/kibana.yml` is used as the configuration by default.

#### Kibana usage example 
1. First, decompress the Kibana installation package into a directory as shown below: 
![](https://main.qcloudimg.com/raw/c170b5293f09a19c821bdee35cf58ce0.png)
2. Then, modify the configuration file under `config` as follows: 
```
# config/kibana.yml
# Port on which the Kibana server listens
server.port: 5601
# IP of the server to which the Kibana server is bound
server.host: 127.0.0.1
# URL of the CTSDB instance to be connected to
elasticsearch.url: "http://127.0.0.1:9200"
# For CTSDB instances that require authentication, you need to enter the username and password
elasticsearch.username: "root"
elasticsearch.password: "changeme"
```
- Start Kibana and access it in a browser 
```
nohup bin/kibana &
```
Access the Kibana server through `IP:port` or the domain name as shown below: 

You can use the development tool to conveniently access CTSDB as shown below: 
![](https://main.qcloudimg.com/raw/2e240510f9f4fac37ddbb61eacbc3c4d.png)
Create the index to be accessed on the management page as shown below: 
![](https://main.qcloudimg.com/raw/7841d9c9588cbc8c01e4fc8503e9bf54.png)
If you need to search for logs, you may use the search feature as shown below: 
![](https://main.qcloudimg.com/raw/d851b63760c8f7a89b80e9b27d22c9c7.png)
You can see that the search results show nothing but time. This is because the source feature is disabled by default in CTSDB to save storage space. If you need to search for logs, please contact us to enable the source feature. The effect after the feature is enabled is as shown below:
![](https://main.qcloudimg.com/raw/e5078b24014e620211714713cd8d0891.png)
By using visualization, you can create various graphs. Here, a line chart is used as an example to show the Kibana graph effect:
![](https://main.qcloudimg.com/raw/994a09e77304a42f63a8e9dc26351487.png)
Kibana not only provides a rich set of visual graph features but also uses dashboards to display the saved visual graphs on the same page in a unified manner, so that you can easily check the changes of multiple metrics. Below is a sample dashboard view of the monitoring data for demonstrating the display effect:
![](https://main.qcloudimg.com/raw/fb39df5d5de57c597a275d01beb2bd66.png)

### Grafana
Grafana is an open-source dashboard tool that provides various graph features just like Kibana. With its fine-grained display effects, you can effectively analyze data. Grafana supports more data sources than Kibana, including InfluxDB, OpenTSDB, and Elasticsearch. The following example shows how to use it to analyze CTSDB data in a visualized way.

####  Grafana  
1. Install 
For more information on how to install Grafana, please see [Install Grafana](http://docs.grafana.org/installation/).
2. Configure
Grafana has many configuration items. You can use the default configuration. For more information, please see [Configuration](http://docs.grafana.org/installation/configuration/).
3. Run 
When Grafana runs, it uses `/etc/grafana/grafana.ini` as its configuration by default.

#### Grafana usage example  
1. First, start the Grafana service.
```
sudo service grafana-server start
```
2. Then, access the Grafana service in a browser:
![](https://main.qcloudimg.com/raw/9f80d3188053b5ca3ef582adedb6a5f2.png)
3. Create a data source and dashboard as shown below:
![](https://main.qcloudimg.com/raw/2580d7a51918fa6beb9819182fca889b.png)
4. Use the dashboard to create a visual graph as shown below:
![](https://main.qcloudimg.com/raw/0f13d15fe87ce7c8766345209d90940f.png)
5. As shown above, the graph display effect of Grafana is slightly different from that of Kibana, but their features are essentially the same, so you can choose either one of them based on your use habits and preferences. Similarly, Grafana dashboard can also display multiple visual graphs as shown below:
![](https://main.qcloudimg.com/raw/ed8a50aec05aea155bfd951d9a0bcac3.png)

## Summary  
This document describes how to connect ELK ecosystem components and Grafana to CTSDB in detail. If you have any questions during use, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
