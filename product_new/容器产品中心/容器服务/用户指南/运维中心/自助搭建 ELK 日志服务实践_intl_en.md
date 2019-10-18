## Operation Scenario
In large-scale distributed applications, or when the workloads of a service are distributed across multiple servers, you can use Linux commands to view application logs one by one. However, this method is highly inefficient, and it is even more complicated when using container deployment services rather than normal distributed applications. Because containers are managed by an upper-level orchestration system, their associated connections with the server are variable. Without a single service to collect and display the application logs, exploring the logs becomes even more difficult.

That’s why TKE is integrated with Tencent Cloud Log Service (CLS), which supports the configuration of collection rules to automatically collect and report logs. It also supports using the log collection and visualization service ELK (Elasticsearch + Logstash + Kibana). This document introduces the application of basic templates provided by Tencent Cloud TKE to create an ELK deployment that uses log data read from Kafka.

## Prerequisites
- Create a cluster. For more information, please see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- Ensure the cluster has enough resources before deployment.
- Log into the node.

## Steps
### Deploying Elasticsearch + Kibana for Log Retrieval and Display
Elasticsearch is an open source, distributed search engine based on Apache Lucene (TM) that provides a RESTful API. Within the framework of ELK, Elasticsearch provides quick data storage and query capabilities. Kibana is an open source data analysis and visualization platform for Elasticsearch. It is used to search and display data stored in the Elasticsearch search engine.
The following steps use the ELK basic template provided by TKE to build an Elasticsearch cluster and Kibana.

>!If the node does not have Git, first executes the `yum install git` command to install Git.
>
1. Execute the following command to download the required YAML files to nodes in a TKE cluster.
```
git clone https://github.com/tencentyun/ccs-elasticsearch-template.git /tmp/kubernetes-elasticsearch
```

2. Execute the following commands to create an Elasticsearch deployment.
```
cd /tmp/kubernetes-elasticsearch
kubectl create -f es-svc.yaml
kubectl create -f es-client.yaml
kubectl create -f es-data.yaml
kubectl create -f es-discovery-svc.yaml
kubectl create -f es-master.yaml
```
3. Execute the following commands to create a Kibana deployment.
```
cd /tmp/kubernetes-elasticsearch
kubectl create -f kibana-svc.yaml
kubectl create -f kibana.yaml
```


### Deploying Logstash to Collect Data Specified by a Kafka Topic
Logstash is an open source log analysis and processing program that can collect and transform data from a variety of sources, including Syslog, Filebeat, Kafka, etc. It also supports sending collected data to Elasticsearch.
The Logstash deployed in this example reads data from the configured Kafka by default, and then sends it to the deployed Elasticsearch service.
1. Log in to [TKE console](https://console.cloud.tencent.com/tke2) and click on the cluster with Elasticsearch + Kibana already deployed to go to the cluster deployment page.
2. <span id="step2"></span>Select **Service** > **Service** to go to the service details page and view the IP of the created Elasticsearch service. See the figure below:
![](https://main.qcloudimg.com/raw/f9671468af487a04b6e5871b5d968a71.png)
3. Execute the following commands to modify `/tmp/kubernetes-elasticsearch/logstash-config.yaml`.
```
cd /tmp/kubernetes-elasticsearch
vim logstash-config.yaml
```
4. Press **i** or **Insert** to switch to editing mode, then modify the Kafka and Elasticsearch addresses. See the figure below:
>? 
>- Kafka address: obtain this address from the deployed Kafka service, or [Ckafka](https://cloud.tencent.com/product/ckafka).
>- Elasticsearch address: obtain this address from [Step 2](#step2).
>
![](https://main.qcloudimg.com/raw/3a4f6c4ed288c4b5f80a720254751f74.png)
5. After modifying the address, press **Esc** and enter **:wq** to save the file and go back.
6. Execute the following commands to deploy Logstash.
```
kubectl create -f logstash-config.yaml
kubectl create -f logstash-consumer.yaml
```

###  Log Data in Kibana
This text takes ELK deployment in a TKE cluster and log data read from Kafka as an example. For more instructions on using and troubleshooting ELK, check online.
1. Log in to [TKE console](https://console.cloud.tencent.com/tke2) and click the deployed cluster to go to the cluster deployment page.
2. Select **Service** > **Service** to go to the service details page and obtain the Load Balancer IP of the Kibana service that has already been created. See the figure below:
![](https://main.qcloudimg.com/raw/45d534ce91f072c963fc27ea1f9d803f.png)
3. Access its public Load Balancer IP to open a Kibana dashboard and explore the logs. See the figure below:
![](https://mc.qcloudimg.com/static/img/a233130efb256ef5836b294e9ec65a35/ccs-log-visual.jpeg)
Before using Kibana to retrieve logs, you must ensure that there is a corresponding index pattern configured in Elasticsearch. See the figure below:
![](https://mc.qcloudimg.com/static/img/da4ea19aa75ffbf94b38e39a6e781082/ccs-log.jpeg)





