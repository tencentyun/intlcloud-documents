## Overview
With the prosperity of the Kafka community, more and more users have started to use Kafka for activities such as log collection, big data analysis, and streaming data processing. CKafka has made the following optimizations on open-source Kafka:
- It features distributed architecture, high scalability, and high throughput based on Apache Kafka.
- It is 100% compatible with Apache Kafka APIs (0.9 and 0.10).
- It offers all features of Kafka with no need for deployment.
- It encapsulates all cluster details, eliminating the need for OPS on your side.
- Its message engine is optimized to deliver a performance 50% higher than that of open-source Kafka.

SCF has been deeply integrated with CKafka, and a lot of practical features have been launched. With the help of SCF and Ckafka trigger, it is easy to dump CKafka messages to COS, ES, and TencentDB. This document describes how to use SCF in place of Logstash to dump CKafka messages to ES as shown below:
 ![](https://main.qcloudimg.com/raw/742d23c1f95b9f3fbf50a099d0ce5ff5.png)

 

## How It Works
SCF can consume messages in CKafka in real time in various scenarios such as data storage, log cleansing, and real-time consumption, and the data dump feature has been integrated in the CKafka Console and can be enabled quickly, making it easier to use as shown below:
![](https://main.qcloudimg.com/raw/994185353e9235c0f75e2dadf0feba41.png)

## Scheme Advantages

Compared to a CVM-based self-created CKafka consumer, SCF has the following advantages:
- You can enable the CKafka trigger quickly in the SCF Console to automatically create a consumer, and SCF will maintain the high availability of components.
- The CKafka trigger itself supports many practical configurations, such as the offset position, 1–10,000 messages to be aggregated, and 1–10,000 retry attempts.
- Business logic developed based on SCF naturally supports auto scaling, eliminating the need to build and maintain server clusters.
 
Compared to CVM-based self-created Logstash service, SCF has the following advantages:
- SCF comes with a consumer component that allows for aggregation.
- The scalable function template of SCF provides message aggregation and partial cleansing capabilities.
- SCF clusters are highly available and support log monitoring, enabling you to launch your business more quickly.
- SCF is pay-as-you-go and more cost effective than self-created clusters, saving 50% of costs.


## Prerequisites
This document uses the **Guangzhou** region as an example:
- You need to activate Elasticsearch Service.
- You need to activate the CKafka service.
 

## Directions
### Creating function
1. Log in to the [SCF Console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default) and click **Functions** on the left sidebar.
2. Select the region where to create a function at the top of the "Functions" page and click **Create** to enter the function creation process.
3. Create a function as follows in "Basic Info" on the "Create Function" page and click **Next**.

	- **Function Name**: enter a custom function name. This document uses `ckafka_to_es_demo`.
	- **Runtime Environment**: select "Pyhton 3.6".
	- **Create Method**: select **Function Template**.
	- **Fuzzy Search**: enter "CKafka" and search.
Click **Learn More** in the template to view relevant information in the "Template Details" pop-up window, which can be downloaded.
4. On the "Function configuration" page, keep the default configuration and click **Complete**.
5. Enter the "Function configuration" page of the created function, click **Edit** in the top-right corner, and complete the function configuration as follows:
 - **Environment Variable**: add the following environment variables and configure them.

<table>
<tr>
<th>key</th><th>value</th><th>Required</th>
</tr>
<tr>
<td>ES_Address</td><td>ES address.</td><td>Yes</td>
</tr>
<tr>
<td>ES_User</td><td>ES username, which is `elastic` by default.</td><td>Yes</td>
</tr>
<tr>
<td>ES_Password</td><td>ES password.</td><td>Yes</td>
</tr>
<tr>
<td>ES_Index_KeyWord</td><td>ES keyword index.</td><td>Yes</td>
</tr>
<tr>
<td>ES_Log_IgnoreWord</td><td>Keyword to be deleted. If this parameter is left empty, all keywords will be written. For example, you can enter `name` or `password`.</td><td>No</td>
</tr>
<tr>
<td>ES_Index_TimeFormat</td><td>Index by day or hour. If this parameter is left empty, the index will be by day. For example, you can enter `hour`.</td><td>No</td>
</tr>
</table>
 - **VPC**: check "Enable" and select the VPC of ES.

6. Click **Save**.



### Creating CKafka trigger
1. Select **Trigger Management** on the sidebar of the "Function configuration" page and click **Create a Trigger**.
2. In the "Create a Trigger" pop-up window, configure the trigger.

The main parameter information is as follows. Keep the remaining parameters as default:
 - **Trigger Method**: select "CKafka trigger".
 - **Ckafka Instance and Topic**: select the corresponding topic as needed.
 - **Start Point**: select "Earliest".
3. Click **Submit**.





### Viewing ES and function execution logs
>!If you have not ingested actual data into CKafka, you can use the [client tool](https://intl.cloud.tencent.com/document/product/597/32544) to simulate message production.
>
- Select **Log Query** on the sidebar of the function to view the function execution log.

- View Kibana. For more information, please see [Accessing Clusters from Kibana](https://intl.cloud.tencent.com/document/product/845/19541).






## Scalability
If you want to implement advanced log cleansing logic, you can modify the logic in the code location as shown below:
![](https://main.qcloudimg.com/raw/8e71698dd087bed4b888773ce0db3175.png)
