An instance provided by ES consists of an ES cluster and a Kibana Console. The former can be accessed via the VIP address and port of your VPC, and the latter provides a public IP address for you to access from a browser. Currently, you can only ingest your data into the ES cluster on your own. The following describes how to import your logs into ES and access Kibana from a browser to perform query and analysis by taking the most typical log analysis architectures Filebeat + Elasticsearch + Kibana and Logstash + Elasticsearch + Kibana as examples.

## Filebeat + Elasticsearch + Kibana
### Deploying Filebeat
1. Download the Filebeat package and decompress it
>The Filebeat version should be compatible with the ES version.

	```
	wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-6.4.3-linux-x86_64.tar.gz   
	tar xvf filebeat-6.4.3-linux-x86_64.tar.gz
	```
2. Configure Filebeat
	In this example, NGINX log is used as the input source, and the output is configured as the private VIP address and port of the ES cluster. If you use a Platinum Edition cluster, you need to add username and password to the output.
Enter the `filebeat-6.4.3-linux-x86_64` directory and modify the `filebeat.yml` configuration file, as shown below:
```
	filebeat.inputs:
	- type: log
  		enabled: true
  		paths:
    		- /var/log/nginx/access.log
	output.elasticsearch:
  		hosts: ["10.0.130.91:9200"]
  		protocol: "http"
  		username: "elastic"
  		password: "test"
```
3. Run Filebeat
	In the `filebeat-6.4.3-linux-x86_64` directory, run:
	```
	nohup ./filebeat -c filebeat.yml 2>&1 >/dev/null &
	```

### <span id="jump">Querying a log</span>
1. On the cluster list page in the ES Console, select **Operation** > **Kibana** to enter the Kibana Console.
![](https://main.qcloudimg.com/raw/3f9be1e4f0782cff576ec83f8dda7b84.png)
2. Go to **Management** > **Index Patterns** and add an index pattern named `filebeat-6.4.3-*`.
	![](https://main.qcloudimg.com/raw/237c9406b30023323fa4108e4575488f.png)
3. Click **Discover** and select the `filebeat-6.4.3-*` index to retrieve the NGINX access logs.
	![](https://main.qcloudimg.com/raw/552277436bab4818fedce01b410703e5.png)

## Logstash + Elasticsearch + Kibana

### Environment preparations
* You need to create one or more CVM instances as needed in the same VPC as the ES cluster and deploy the Logstash component on them;
* A CVM instance should have at least 2 GB of memory;
* You need to install Java 8 or above on the CVM instances.

### Deploying Logstash

1. Download the Logstash package and decompress it
>The Logstash version should be compatible with the ES version.
>
```
wget https://artifacts.elastic.co/downloads/logstash/logstash-6.4.3.tar.gz
tar xvf logstash-6.4.3.tar.gz
```
2. Configure Logstash
In this example, NGINX log is used as the input source, and the output is configured as the private VIP address and port of the ES cluster. Create a `test.conf` configuration file, as shown below:
	```
	input {
	    file {
	        path => "/var/log/nginx/access.log" # Path to the NGINX access log
	        start_position => "beginning" # Read the log from the beginning of the file. If this parameter is not set, the log will be read when data is written to the file, just like `tail -f`
	        }
	}
	filter {
	}
	output {
	  elasticsearch {
	    hosts => ["http://172.16.0.145:9200"] # Private VIP address and port of the ES cluster
	    index => "nginx_access-%{+YYYY.MM.dd}" # Index name. Indices are automatically created on a daily basis
	    user => "elastic" # Username
	    password => "yinan_test" # Password
	 }
	}
	```
The ES cluster is configured to automatically create an index by default. The `nginx_access-%{+YYYY.MM.dd}` index will be automatically created, and unless you need to set the mapping of the fields in the index in advance, you don't need to additionally call the API of ES to create indices.

3. Start Logstash
Enter the extracted `logstash-6.4.3` directory of the Logstash package and run the following command to start Logstash in the background. Be sure to enter the path you create as the path to the configuration file.
	```
nohup ./bin/logstash -f test.conf 2>&1 >/dev/null &
	```
View the `logs` directory in the `logstash-6.4.3` directory to confirm that Logstash has been started and can record the following logs:
	```
	Sending Logstash logs to /root/logstash-6.4.3/logs which is now configured via log4j2.properties
	[2019-05-29T12:20:26,630][INFO ][logstash.setting.writabledirectory] Creating directory {:setting=>"path.queue", :path=>"/root/logstash-6.4.3/data/queue"}
	[2019-05-29T12:20:26,639][INFO ][logstash.setting.writabledirectory] Creating directory {:setting=>"path.dead_letter_queue", :path=>"/root/logstash-6.4.3/data/dead_letter_queue"}
	[2019-05-29T12:20:27,125][WARN ][logstash.config.source.multilocal] Ignoring the 'pipelines.yml' file because modules or command line options are specified
	[2019-05-29T12:20:27,167][INFO ][logstash.agent           ] No persistent UUID file found. Generating new UUID {:uuid=>"2e19b294-2b69-4da1-b87f-f4cb4a171b9c", :path=>"/root/logstash-6.4.3/data/uuid"}
	[2019-05-29T12:20:27,843][INFO ][logstash.runner          ] Starting Logstash {"logstash.version"=>"6.4.3"}
	[2019-05-29T12:20:30,067][INFO ][logstash.pipeline        ] Starting pipeline {:pipeline_id=>"main", "pipeline.workers"=>1, "pipeline.batch.size"=>125, "pipeline.batch.delay"=>50}
	[2019-05-29T12:20:30,871][INFO ][logstash.outputs.elasticsearch] Elasticsearch pool URLs updated {:changes=>{:removed=>[], :added=>[http://elastic:xxxxxx@10.0.130.91:10880/]}}
	[2019-05-29T12:20:30,901][INFO ][logstash.outputs.elasticsearch] Running health check to see if an Elasticsearch connection is working {:healthcheck_url=>http://elastic:xxxxxx@10.0.130.91:10880/, :path=>"/"}
	[2019-05-29T12:20:31,449][WARN ][logstash.outputs.elasticsearch] Restored connection to ES instance {:url=>"http://elastic:xxxxxx@10.0.130.91:10880/"}
	[2019-05-29T12:20:31,567][INFO ][logstash.outputs.elasticsearch] ES Output version determined {:es_version=>6}
	[2019-05-29T12:20:31,574][WARN ][logstash.outputs.elasticsearch] Detected a 6.x and above cluster: the `type` event field won't be used to determine the document _type {:es_version=>6}
	[2019-05-29T12:20:31,670][INFO ][logstash.outputs.elasticsearch] New Elasticsearch output {:class=>"LogStash::Outputs::ElasticSearch", :hosts=>["http://10.0.130.91:10880"]}
	[2019-05-29T12:20:31,749][INFO ][logstash.outputs.elasticsearch] Using mapping template from {:path=>nil}
	[2019-05-29T12:20:31,840][INFO ][logstash.outputs.elasticsearch] Attempting to install template {:manage_template=>{"template"=>"logstash-*", "version"=>60001, "settings"=>{"index.refresh_interval"=>"5s"}, "mappings"=>{"_default_"=>{"dynamic_templates"=>[{"message_field"=>{"path_match"=>"message", "match_mapping_type"=>"string", "mapping"=>{"type"=>"text", "norms"=>false}}}, {"string_fields"=>{"match"=>"*", "match_mapping_type"=>"string", "mapping"=>{"type"=>"text", "norms"=>false, "fields"=>{"keyword"=>{"type"=>"keyword", "ignore_above"=>256}}}}}], "properties"=>{"@timestamp"=>{"type"=>"date"}, "@version"=>{"type"=>"keyword"}, "geoip"=>{"dynamic"=>true, "properties"=>{"ip"=>{"type"=>"ip"}, "location"=>{"type"=>"geo_point"}, "latitude"=>{"type"=>"half_float"}, "longitude"=>{"type"=>"half_float"}}}}}}}}
	[2019-05-29T12:20:32,094][INFO ][logstash.outputs.elasticsearch] Installing elasticsearch template to _template/logstash
	[2019-05-29T12:20:33,242][INFO ][logstash.inputs.file     ] No sincedb_path set, generating one based on the "path" setting {:sincedb_path=>"/root/logstash-6.4.3/data/plugins/inputs/file/.sincedb_d883144359d3b4f516b37dba51fab2a2", :path=>["/var/log/nginx/access.log"]}
	[2019-05-29T12:20:33,329][INFO ][logstash.pipeline        ] Pipeline started successfully {:pipeline_id=>"main", :thread=>"#<Thread:0x12bdd65 run>"}
	[2019-05-29T12:20:33,544][INFO ][logstash.agent           ] Pipelines running {:count=>1, :running_pipelines=>[:main], :non_running_pipelines=>[]}
	[2019-05-29T12:20:33,581][INFO ][filewatch.observingtail  ] START, creating Discoverer, Watch with file and sincedb collections
	[2019-05-29T12:20:34,368][INFO ][logstash.agent           ] Successfully started Logstash API endpoint {:port=>9600}
	```
For more information on the features of Logstash, see [Elastic's official documentation](https://www.elastic.co/products/logstash).

### Querying a log

See [Querying a log](#jump).

For more information on the features of the Kibana Console, see [Elastic's official documentation](https://www.elastic.co/cn/products/kibana).
