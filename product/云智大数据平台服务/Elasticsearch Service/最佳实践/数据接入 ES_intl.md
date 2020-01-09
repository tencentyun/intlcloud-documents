
Tencent Cloud Elasticsearch Service (ES) provides access to the cluster through its private VIP within your VPC. You can access your cluster by writing codes through the Elasticsearch REST client and import your data into the cluster. Of course you can also integrate your own data through officially provided components such as Logstash and Beats. The following takes the official components Logstash and Beats as examples to introduce the ways to link your data source of different types into ES.

## Preparations

You need to create a CVM instance or a Docker cluster in the same VPC as the ES cluster, as the access to the ES cluster has to be done within the VPC.

## Using Logstash to Access ES Clusters

### Access the ES clusters in CVM

1. Install and Deploy Logstash and Java 8.
```
wget https://artifacts.elastic.co/downloads/logstash/logstash-5.6.4.tar.gz
tar xvf logstash-5.6.4.tar.gz
yum install java-1.8.0-openjdk  java-1.8.0-openjdk-devel -y
```
2. Customize the configuration file \*.conf based on the data source type. For the content of the configuration file, see the description of the data source configuration file below.
3. Execute Logstash.
```
	nohup ./bin/logstash -f ~/*.conf 2>&1 >/dev/null &
```

### Access ES clusters in Docker
#### Create a Docker cluster.

1. Pull the official image of Logstash.
```
	docker pull docker.elastic.co/logstash/logstash:5.6.9
```
2. Customize the configuration file *.conf based on the data source type, and place it under the `/usr/share/logstash/pipeline/` directory, which can be customized.

3. Run Logstash.
```
docker run --rm -it -v ~/pipeline/:/usr/share/logstash/pipeline/ docker.elastic.co/logstash/logstash:5.6.9
```

#### Use Tencent Cloud TKE

Tencent Cloud's Docker clusters run on CVM instances, so you need to create a CVM cluster on the TKE console first.

1. Create a cluster.
![](https://main.qcloudimg.com/raw/bef34f94f675e6930d4065294372e80b.png)

2. Create the service.
![](https://main.qcloudimg.com/raw/be5d094efdbe3af4188d3ed7b87132fb.png)

3. Select Logstash image.
In this example, the Logstash image provided by TencentHub image repository is used. You can also create a Logstash image by yourself.
![](https://main.qcloudimg.com/raw/750a904e83ffeb026391f42e1f9fa2be.png)

4. Create a data volume.
Create a data volume to store the logstash configuration file. In this example, a configuration file named logstash.conf is added to the CVM's `/data/config` directory and mounted to the Docker's `/data` directory, so that the logstash.conf file can be read when the container starts.
![](https://main.qcloudimg.com/raw/586d21e0309f162d2a054fdc48372b88.png)

5. Configure the operating parameters.
![](https://main.qcloudimg.com/raw/c134f1daa02aa08bae193b5e0ecf37e6.png)
![](https://main.qcloudimg.com/raw/30c138c7117729a83e1e320d90d64287.png)

6. Configure service parameters and create services.
![](https://main.qcloudimg.com/raw/7bdaea6c6bb48c731b26fb1f2ea21425.png)

## Description of Configuration Files
### File data sources

```
input {
    file {
        path => "/var/log/nginx/access.log" # File path
        }
}
filter {
}
output {
  elasticsearch {
    hosts => ["http://172.16.0.89:9200"] # Elasticsearch cluster's private VIP address and port
    index => "nginx_access-%{+YYYY.MM.dd}" #  Custom index names. One index is generated every day with the date as suffix.
 }
}
```
For more information on integrating File data sources, see the official document [File Input Plugin](https://www.elastic.co/guide/en/logstash/5.6/plugins-inputs-file.html).


### Kafka data sources

```
input{
      kafka{
        bootstrap_servers => ["172.16.16.22:9092"]
        client_id => "test"
        group_id => "test"
        auto_offset_reset => "latest" # Start consuming from the latest offset.
        consumer_threads => 5
        decorate_events => true # This attribute will also bring the current topic, offset, group, partition and other information to the message.
        topics => ["test1","test2"] # Array type. Multiple topics supported.
        type => "test" # Data source identifier field
      }
}

output {
  elasticsearch {
    hosts => ["http://172.16.0.89:9200"] # Elasticsearch cluster's private VIP address and port
    index => "test_kafka"
 }
}
```
For more information on accessing Kafka data sources, see the official document [Kafka Input Plugin](https://www.elastic.co/guide/en/logstash/5.6/plugins-inputs-kafka.html).

### Database data sources connected with JDBC

```
input {
    jdbc {
      # mysql Database address
      jdbc_connection_string => "jdbc:mysql://172.16.32.14:3306/test"
      # User name and password
      jdbc_user => "root"
      jdbc_password => "Elastic123"
      # Driver jar package. You need to download the jar if installing and deploying Logstash on your own as it is not provided with Logstash by default.
      jdbc_driver_library => "/usr/local/services/logstash-5.6.4/lib/mysql-connector-java-5.1.40.jar"
      #  Driver class name
      jdbc_driver_class => "com.mysql.jdbc.Driver"
      jdbc_paging_enabled => "true"
      jdbc_page_size => "50000"
      # The SQL file path and name to be executed.
      #statement_filepath => "test.sql"
      #  SQL statements to be executed.
      statement => "select * from test_es"
      #  Set the monitoring interval. The meaning of each field (from left to right) is minute, hour, day, month and year. If all are *, it means to update every minute by default.
      schedule => "* * * * *"
      type => "jdbc"
    }
}

output {
    elasticsearch {
        hosts => ["http://172.16.0.30:9200"]
        index => "test_mysql"
        document_id => "%{id}"
    }
}
```
For more information on accessing database data sources connected with JDBC, see the official document [jdbc input plugin](https://www.elastic.co/guide/en/logstash/5.6/plugins-inputs-jdbc.html).


## Access ES Clusters with Beats

Beats contains a variety of single-purpose collectors. These collectors are relatively lightweight and can be deployed and run on the server to collect logs, monitor data etc. Compared with Logstash, Beats occupies less system resources.

Beats includes FileBeat for collecting file type data, MetricBeat for collecting monitoring metric data, PacketBeat for collecting network packet data, etc. You can also develop your own Beat components based on the official libbeat library as needed.

### Access the ES clusters in CVM

1. Install and deploy Filebeat.
```
	wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-5.6.4-linux-x86_64.tar.gz
	tar xvf filebeat-5.6.4.tar.gz
```
2. Configure the filebeat.yml.
3. Execute Filebeat.
```
	nohup ./filebeat 2>&1 >/dev/null &
```

### Access ES clusters in Docker
#### Create a Docker cluster

1. Pull the official image of Filebeat.
```
	docker pull docker.elastic.co/beats/filebeat:5.6.9
```
2. Customize the configuration file \*.conf based on the data source type, and place it in the `/usr/share/logstash/pipeline/` directory, which can be customized.
3. Run Filebeat.
```
	docker run docker.elastic.co/beats/filebeat:5.6.9
```

#### Use Tencent Cloud TKE

The deployment of Filebeat using Tencent Cloud TKE is similar to that of Logstash, and you can use the Filebeat image officially provided by Tencent Cloud.
![](https://main.qcloudimg.com/raw/67f84497e15809a4a92bbe64ade43327.png)

### Description of configuration files
Configure the filebeat.yml file as follows:

```
// Input source configuration
filebeat.prospectors:
- input_type: log
    paths:
    - /usr/local/services/testlogs/*.log

// Output to ES
output.elasticsearch:
  # Array of hosts to connect to.
  hosts: ["172.16.0.39:9200"]
```

