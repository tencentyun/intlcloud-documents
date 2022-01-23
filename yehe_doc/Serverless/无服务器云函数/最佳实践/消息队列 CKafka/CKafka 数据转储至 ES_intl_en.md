## Overview
With the prosperity of the Kafka community, more and more users have started to use Kafka for activities such as log collection, big data analysis, and streaming data processing. CKafka has made the following optimizations on open-source Kafka:
- It features distributed architecture, high scalability, and high throughput based on Apache Kafka.
- It is 100% compatible with Apache Kafka APIs (0.9 and 0.10).
- It offers all features of Kafka with no need for deployment.
- It encapsulates all cluster details, eliminating the need for OPS on your side.
- Its message engine is optimized to deliver a performance 50% higher than that of open-source Kafka.

SCF has been deeply integrated with CKafka, and a lot of practical features have been launched. With the help of SCF and CKafka trigger, it is easy to dump CKafka messages to COS, ES, and TencentDB. This document describes how to use SCF in place of Logstash to dump CKafka messages to ES as shown below:
 ![](https://main.qcloudimg.com/raw/742d23c1f95b9f3fbf50a099d0ce5ff5.png)

 

## How It Works
SCF can consume messages in CKafka in real time in various scenarios such as data storage, log cleansing, and real-time consumption, and the data dump feature has been integrated in the CKafka console and can be enabled quickly, making it easier to use as shown below:
![](https://main.qcloudimg.com/raw/994185353e9235c0f75e2dadf0feba41.png)

## Scheme Advantages

Compared to a CVM-based self-created CKafka consumer, SCF has the following advantages:
- You can enable the CKafka trigger quickly in the SCF console to automatically create a consumer, and SCF will maintain the high availability of components.
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
### Creating function and CKafka trigger

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default) and click **Function Service** on the left sidebar.
2. Select the region where to create a function at the top of the **Function Service** page and click **Create** to enter the function creation process.
3. Select a function template as follows on the **Create Function** page and click **Next** as shown below:
![](https://main.qcloudimg.com/raw/7366c21dc035812c40afcb861472ae57.png)
  - **Creation method**: select **Template**.
  - **Fuzzy search**: enter **CkafkaToElasticsearch** and search. This document uses the Python 3.6 runtime environment as an example. 
    Click **Learn More** in the template to view relevant information in the **Template Details** pop-up window, which can be downloaded.
4. In the **Basic Configurations** section, the function name has been automatically generated and can be modified as needed. Follow the prompts to configure environment variables, execution role, and VPC as shown below:
![](https://main.qcloudimg.com/raw/06422b76337b0c8f3f5c6941a425570e.png)
  - **Environment Variable**: add the following environment variables and configure them as shown below:
![](https://main.qcloudimg.com/raw/9ef490836df44ec54aa5ea2ba3bdbc47.png)
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
 - **Execution Role**: check **Enable**, select **Configure and use SCF template role**, and the system will automatically create and select an SCF template execution role associated with full access permissions of ES and CKafka. You can also check **Use the existing role** and select an existing role that has the above permissions in the drop-down list. This document takes **Configure and use SCF template role** as an example.
  - **VPC**: check **Enable** and select the VPC of ES.
5. In the **Trigger Configurations** section, select **Custom** and enter relevant 

  information according to the displayed parameters as shown below:

![](https://main.qcloudimg.com/raw/92eca3882647a8c58e6b8711256ce081.png)

​    The main parameter information is as follows. Keep the remaining parameters as default:
 - **Trigger Method**: select **CKafka trigger**.
 - **CKafka Instance and Topic**: select the corresponding topic as needed.
 - **Start Point**: select **Earliest**.
6. Click **Complete**.


### Viewing ES and function execution logs
>!If you have not ingested actual data into CKafka, you can use the [client tool](https://intl.cloud.tencent.com/document/product/597/32544) to simulate message production.
>
- Select **Log Query** on the sidebar of the function to view the function execution log.
- View Kibana. For more information, please see [Accessing Clusters from Kibana](https://intl.cloud.tencent.com/document/product/845/19541).
![](https://main.qcloudimg.com/raw/974199a28188cb11a43b5e89e5f660b5.png)



## Scalability
If you want to implement advanced log cleansing logic, you can modify the logic in the code location.

![](https://main.qcloudimg.com/raw/71b85519bb7334b4791f8e887906bacb.png)

