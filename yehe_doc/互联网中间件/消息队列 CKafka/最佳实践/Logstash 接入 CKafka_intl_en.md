## Logstash Introduction
Logstash, an open-source log processing tool, is used to collect data from multiple sources, filter collected data, and store data for other uses.

Logstash is highly flexible and has powerful syntax analysis capabilities. With a variety of plugins, it supports multiple types of inputs and outputs. In addition, as a horizontally scalable data pipeline, it has powerful log collection and retrieval features that work with Elasticsearch and Kibana.

#### Working principles of Logstash
The Logstash data processing pipeline can be divided into 3 stages: inputs → filters → outputs.
1. Inputs: generate data. Inputs are data sources such as file, syslog, redis, and beats.
2. Filters: modify and filter data. Filters are intermediate processing components in the Logstash data pipeline. They can modify events based on specific conditions. Some commonly-used filters are grok, mutate, drop, and clone.
3. Outputs: transfer data to other locations. An event can be transferred to multiple outputs, and the event ends when the transfer is completed. Elasticsearch is the most commonly-used output.

In addition, Logstash supports encoding and decoding data, so you can specify data formats on the input and output ends.
![](https://mc.qcloudimg.com/static/img/17f1ac23a158b043091ebf48071f3a78/00.png)

## Advantages of Connecting Logstash to Kafka
- Data can be asynchronously processed to prevent traffic spikes.
- Components are decoupled, so when an exception occurs in Elasticsearch, the upstream work will not be affected.
Note: Logstash consumes resources when processing data. If you deploy Logstash on a production server, the performance of the server may be affected.
![](https://mc.qcloudimg.com/static/img/bb8a396b1953ed487776281ef616a5c8/11.png)


## Connecting to CKafka
### Supported versions
#### Inputs
The compatibility of official versions is described in the following table:

| Kafka Client Version | Logstash Version | Plugin Version | 
|---------|---------|---------|
| 0.8 | 2.0.0 - 2.x.x | < 3.0.0 |  
| 0.9 | 2.0.0 - 2.3.x | 3.x.x | 
| 0.9 | 2.4.x - 5.x.x | 4.x.x | 
| 0.10.0.x | 2.4.x - 5.x.x | 5.x.x | 

The latest version is V5.1.8, which uses the Consumer API V0.10 to read data.

For information about parameter configuration, see [Kafka input plugin](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-kafka.html).

#### Outputs
The compatibility of official versions is described in the following table:

| Kafka Client Version | Logstash Version | Plugin Version |
|---------|---------|---------|
| 0.8 | 2.0.0 - 2.x.x | < 3.0.0 |  
| 0.9 | 2.0.0 - 2.3.x | 3.x.x  | 
| 0.9 | 2.4.x - 5.x.x | 4.x.x | 
| 0.10.0.x | 2.4.x - 5.x.x | 5.x.x  | 
 
The latest version is V5.1.7, which uses the Producer API V0.10 to produce data.

For information about parameter configuration, see [Kafka output plugin](https://www.elastic.co/guide/en/logstash/current/plugins-outputs-kafka.html).

### Preparations
- Java version: Java 8
- Logstash version: 5.5.2 (August 17, 2017)
- A CKafka instance and a topic

#### Creating a CKafka topic
1. After an instance is created, you can view its information in the [CKafka console](https://console.cloud.tencent.com/ckafka).
![](https://main.qcloudimg.com/raw/91dfb78f2400262f51ff4222dc01d967.png)
2. Click the instance name to view the instance details.
![](https://main.qcloudimg.com/raw/5a29f22f13e2758cf161b2913ecbdec3.png)
3. Click **Topic Management** to create a topic. In this example, the topic is named **logstash_test**.
![](https://main.qcloudimg.com/raw/7a3bf312e8121c097dbfbe5839490975.png)
Now, the operating environment of CKafka has been created.

### CKafka as inputs
1. Run `bin/logstash-plugin list` to check whether logstash-input-kafka is included in the supported plugin list.
![](https://mc.qcloudimg.com/static/img/c5c876ea5ae5ce75307a5e307357e622/input1.png)

2. Write a configuration file `input.conf`.
In the following example, Kafka is used as the data source, and the standard output is taken as the data destination.
```
input {
    Kafka {
        bootstrap_servers => "172.16.16.12:9092" // VIP address of the CKafka instance
        group_id => "logstash_group" // CKafka group ID
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
In the proceeding figure, you can see that messages in the topic have been consumed.


### CKafka as outputs
1. Run `bin/logstash-plugin list` to check whether logstash-output-kafka is included in the supported plugin list.
![](https://mc.qcloudimg.com/static/img/c5c876ea5ae5ce75307a5e307357e622/77.png)

2. Write a configuration file `output.conf`.
In the following example, the standard input is taken as the data source, and Kafka is used as the data destination.
![](https://main.qcloudimg.com/raw/834c54ed67efac389dd979976b3f2494.png)

3. Launch Logstash to produce messages.
![](https://mc.qcloudimg.com/static/img/1f28c9cac2800e211695307e7138d812/image.png)

4. Verify the production data from the previous step.
![](https://mc.qcloudimg.com/static/img/ae85758a90a497235a90511770f959d2/10.png)



