## Logstash Overview
Logstash is an open-source log processing tool used to collect data from multiple sources, filter the collected data, and store the data for other purposes.

Logstash is highly flexible and has powerful syntax analysis capabilities with a wide variety of plugins. It also supports multiple input/output sources. In addition, as a horizontally scalable data pipeline, it is powerful in log collection and retrieval when working together with Elasticsearch and Kibana.

### How Logstash works
Logstash data processing can be divided into three stages: inputs → filters → outputs.
1. inputs: data sources are generated, such as file, syslog, redis, and beats.
2. filters: data is modified and filtered. This is an intermediate link in the Logstash data pipeline. You can change events based on specific conditions. Common filters include `grok`, `mutate`, `drop`, and `clone`.
3. outputs: data is shipped elsewhere. An event can be shipped to multiple outputs and it ends when the shipping is completed. Elasticsearch is the most common output.

In addition, Logstash supports encoding/decoding, so you can specify the format on the inputs/outputs side.
![](https://mc.qcloudimg.com/static/img/17f1ac23a158b043091ebf48071f3a78/00.png)

## Advantages of Logstash for Kafka

![](https://mc.qcloudimg.com/static/img/bb8a396b1953ed487776281ef616a5c8/11.png)
- Data can be asynchronously processed to prevent traffic spikes.
- Components are decoupled, so when an exception occurs in Elasticsearch, the upstream work will not be affected.
- Filtering data using Logstash consumes resources. The performance of Logstash may be compromised if it is deployed on the production server.

## Connection to CKafka
### Supported version
#### inputs
The compatibility with official versions is as described below:
![](https://mc.qcloudimg.com/static/img/7a25c5c3381a9f615701e88964ee8204/22.png)

The latest version is v5.1.8, which uses Consumer API v0.10 to consume data.

For more information on parameter configuration, please see [Kafka input plugin](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-kafka.html).
#### outputs
The compatibility with official versions is as described below:

![](https://mc.qcloudimg.com/static/img/bd2ca98c3b0d392abe77a337450bb132/33.png)

The latest version is v5.1.7, which uses Consumer API v0.10 to produce data.

For more information on parameter configuration, please see [Kafka output plugin](https://www.elastic.co/guide/en/logstash/current/plugins-outputs-kafka.html).
### Preparations
- Java version: Java 8
- Logstash version: 5.5.2 (August 17, 2017)
- Apply for a CKafka instance and create a corresponding topic

#### Creating a CKafka instance
1. After an instance is created, you can view its information in the console.
2. Click the instance name to view the specific information assigned to the instance.
3. Click **Topic Management** to create a topic named **logstash_test**.
Now, the operating environment of CKafka has been created.

### Connecting CKafka as inputs
1. Run `bin/logstash-plugin list` to check whether `logstash-input-kafka` is contained in the supported plugins.
![](https://mc.qcloudimg.com/static/img/c5c876ea5ae5ce75307a5e307357e622/input1.png)

2. Write the configuration file `input.conf`.
Here, standard output is taken as the key data, and Kafka is used as the data source.
```
input {
    kafka {
        bootstrap_servers => "172.16.16.12:9092" // CKafka VIP
        group_id => "logstash_group"  // CKafka `groupid`
        topics => ["logstash_test"] // CKafka topic name
        consumer_threads => 3 // Number of consumer threads, which is generally the same as the number of CKafka partitions
        auto_offset_reset => "earliest"
    }
}
output {
    stdout{codec=>rubydebug}
}
```
3. Launch Logstash to consume messages.
![](https://mc.qcloudimg.com/static/img/5c58f08f2fd0fff052cab655d00d4133/input3.png)
You can see that the data in the topic above has been consumed now.

For more information on parameter configuration when using Kafka as an input, please see [Kafka input plugin](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-kafka.html#plugins-inputs-kafka-auto_offset_reset).

### Connecting CKafka as outputs
1. Run `bin/logstash-plugin list` to check whether `logstash-output-kafka` is contained in the supported plugins.
![](https://mc.qcloudimg.com/static/img/c5c876ea5ae5ce75307a5e307357e622/77.png)

2. Write the configuration file `output.conf`.
Here, standard input is taken as the data source, and Kafka is used as the data destination.

3. Launch Logstash to produce messages.

4. Verify the production data from the previous step.
![](https://mc.qcloudimg.com/static/img/ae85758a90a497235a90511770f959d2/10.png)

For more information on parameter configuration when using Kafka as an output, please see [Kafka output plugin](https://www.elastic.co/guide/en/logstash/current/plugins-outputs-kafka.html).




