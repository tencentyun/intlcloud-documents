Logstash, an open-source log processing tool, is used to collect data from multiple sources, filter collected data, and store data for other uses.

Logstash is highly flexible and has powerful syntax analysis capabilities. With a variety of plugins, it supports multiple types of inputs and outputs. In addition, as a horizontally scalable data pipeline, it has powerful log collection and retrieval features that work with Elasticsearch and Kibana.

## How Logstash Works

The Logstash data processing pipeline can be divided into 3 stages: inputs → filters → outputs.

1. Inputs: generate data. Inputs are data sources such as file, syslog, redis, and beats.
2. Filters: modify and filter data. Filters are intermediate processing components in the Logstash data pipeline. They can modify events based on specific conditions. Some commonly-used filters are grok, mutate, drop, and clone.
3. Outputs: transfer data to other locations. An event can be transferred to multiple outputs, and the event ends when the transfer is completed. Elasticsearch is the most commonly-used output.

In addition, Logstash supports encoding and decoding data, so you can specify data formats on the input and output ends.
![](https://mc.qcloudimg.com/static/img/17f1ac23a158b043091ebf48071f3a78/00.png)

## Advantages of Connecting Logstash to Kafka

- Data can be asynchronously processed to prevent traffic spikes.
- Components are decoupled, so when an exception occurs in Elasticsearch, the upstream work will not be affected.

>!Logstash consumes resources when processing data. If you deploy Logstash on a production server, the performance of the server may be affected.

![](https://mc.qcloudimg.com/static/img/bb8a396b1953ed487776281ef616a5c8/11.png)


## Directions

### Preparations

- Download and install Logstash. For more information, please see [Installing Logstash](https://www.elastic.co/guide/en/logstash/7.6/installing-logstash.html?spm=a2c4g.11186623.2.10.7d625287CKP6MX).
- Download and install JDK 8. For more information, please see [Java SE Development Kit 8 Downloads](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html).
- You have [created a CKafka instance](https://intl.cloud.tencent.com/document/product/597/39718).

### Step 1. Get the CKafka instance access address

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Select **Instance List** on the left sidebar and click the **ID** of an instance to enter the instance basic information page.
3. On the instance basic information page, get the instance access address in the **Access Mode** module.
   ![](https://main.qcloudimg.com/raw/a28b5599889166095c168510ce1f5e89.png)

### Step 2. Create a topic

1. On the instance basic information page, select the **Topic Management** tab on the top.
2. On the topic management page, click **Create** to create a topic named `logstash_test`.
   ![](https://main.qcloudimg.com/raw/76ca78b4058d40510ecd81c9cf40e5b5.png)

### Step 3. Connect to CKafka

>?You can click the following tabs to view the detailed directions for using CKafka as `inputs` or `outputs`.

<dx-tabs>
::: Connecting as \sinputs\s

1. Run `bin/logstash-plugin list` to check whether `logstash-input-kafka` is included in the supported plugins.
   ![](https://mc.qcloudimg.com/static/img/c5c876ea5ae5ce75307a5e307357e622/input1.png)

2. Write the configuration file `input.conf` in the `.bin/` directory.
   In the following example, Kafka is used as the data source, and the standard output is taken as the data destination.
   ```bash
   input {
       kafka {
           bootstrap_servers => "xx.xx.xx.xx:xxxx" // CKafka instance access address
           group_id => "logstash_group"  // CKafka group ID
           topics => ["logstash_test"] // CKafka topic name
           consumer_threads => 3 // Number of consumer threads, which is generally the same as the number of CKafka partitions
           auto_offset_reset => "earliest"
       }
   }
   output {
       stdout{codec=>rubydebug}
   }
   ```
3. Run the following command to start Logstash and consume messages.
   ```
   ./logstash -f input.conf
   ```
   
	 The returned result is as follows:
   ![](https://mc.qcloudimg.com/static/img/5c58f08f2fd0fff052cab655d00d4133/input3.png)
   You can see that the data in the topic above has been consumed now.

:::

::: Connecting as \soutputs\s

1. Run `bin/logstash-plugin list` to check whether `logstash-output-kafka` is included in the supported plugins.
   ![](https://mc.qcloudimg.com/static/img/c5c876ea5ae5ce75307a5e307357e622/77.png)

2. Write the configuration file `output.conf` in the `.bin/` directory.
   In the following example, the standard input is taken as the data source, and Kafka is used as the data destination.

   ```bash
   input {
       input {
         stdin{}
     }
   }
   
   output {
      kafka {
           bootstrap_servers => "xx.xx.xx.xx:xxxx"  // CKafka instance access address
           topic_id => "logstash_test" // CKafka topic name
          }
   }
   ```

3. Run the following command to start Logstash and send messages to the created topic:

   ```bash
   ./logstash -f output.conf
   ```

![](https://mc.qcloudimg.com/static/img/1f28c9cac2800e211695307e7138d812/image.png)

4. Start the CKafka consumer and verify the production data from the previous step.
![](https://mc.qcloudimg.com/static/img/ae85758a90a497235a90511770f959d2/10.png)

:::

</dx-tabs>
