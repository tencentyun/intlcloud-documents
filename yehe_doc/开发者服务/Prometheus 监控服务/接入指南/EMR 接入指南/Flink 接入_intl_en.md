## Overview

When using Flink, you need to monitor its task running status to know whether the tasks run normally and troubleshoot faults. TMP integrates Pushgateway to allow Flink to write metrics and provides an out-of-the-box Grafana monitoring dashboard for it.


## Prerequisites

1. The EMR product you purchased includes the Flink component, and a Flink task is running in your instance.
2. You have created a [TKE cluster](https://intl.cloud.tencent.com/document/product/457/30637) in the region and VPC of your TMP instance.


## Directions
### Integrating product

#### Getting Pushgateway access configuration

1. Log in to the **[EMR console](https://console.cloud.tencent.com/emr)**, select the corresponding **instance**, and select **Basic Info** > **Instance Info** to get the Pushgateway address and token.
![](https://qcloudimg.tencent-cloud.cn/raw/24928b24baa24a876d66b85454b9f97a.png)
2. Get the `APPID` on the [Account Info](https://console.cloud.tencent.com/developer) page.


#### Modifying Flink configuration

1. Log in to the **[EMR console](https://console.cloud.tencent.com/emr)**, select the corresponding **instance**, and select **Cluster Service**.
2. Find the **Flink** configuration item and select **Configuration Management** in the **Operation** column on the right to enter the configuration management page.
3. On the right of the page, click **Add Configuration Item** and add the following configuration items one by one:
<table>
<thead>
<tr>
<th>Configuration Item</th>
<th align="center">Default Value</th>
<th align="center">Data Type</th>
<th>Description</th>
<th>Suggestion</th>
</tr>
</thead>
<tbody>
<tr>
<td>metrics.reporter.promgateway.class</td>
<td align="center">None</td>
<td align="center" nowrap="nowrap">String</td>
<td>Name of the Java class for exporting metrics to Pushgateway</td>
<td>-</td>
</tr>
<tr>
<td>metrics.reporter.promgateway.<br>jobName</td>
<td align="center">None</td>
<td align="center">String</td>
<td>Push task name</td>
<td>Specify an easily understandable string</td>
</tr>
<tr>
<td>metrics.reporter.promgateway.<br>randomJobNameSuffix</td>
<td align="center">true</td>
<td align="center">Boolean</td>
<td>Whether to add a random string after the task name</td>
<td>Set it to `true`. If no random string is added, metrics of different Flink tasks will overwrite each other</td>
</tr>
<tr>
<td>metrics.reporter.promgateway.<br>groupingKey</td>
<td align="center">None</td>
<td align="center">String</td>
<td>Global label added to each metric in the format of `k1=v1;k2=v2`</td>
<td>Add the EMR instance ID to distinguish between the data of different instances, such as `instance_id=emr-xxx`</td>
</tr>
<tr>
<td>metrics.reporter.promgateway.<br>interval</td>
<td align="center">None</td>
<td align="center">Time</td>
<td>Time interval for pushing metrics, such as 30s</td>
<td>We recommend you set the value to about 1 minute</td>
</tr>
<tr>
<td>metrics.reporter.promgateway.host</td>
<td align="center">None</td>
<td align="center">String</td>
<td>Pushgateway service address</td>
<td>It is the service address of the TMP instance in the console</td>
</tr>
<tr>
<td>metrics.reporter.promgateway.port</td>
<td align="center">-1</td>
<td align="center">Integer</td>
<td>Pushgateway service port</td>
<td>It is the port of the TMP instance in the console</td>
</tr>
<tr>
<td>metrics.reporter.promgateway.<br>needBasicAuth</td>
<td align="center">false</td>
<td align="center">Boolean</td>
<td>Whether the Pushgateway service requires authentication</td>
<td>Set it to `true`, as the Pushgateway of TMP requires authentication</td>
</tr>
<tr>
<td>metrics.reporter.promgateway.user</td>
<td align="center">None</td>
<td align="center">String</td>
<td>Username for authentication</td>
<td>It is your `<a href="https://console.cloud.tencent.com/developer">APPID</a>`</td>
</tr>
<tr>
<td>metrics.reporter.promgateway.<br>password</td>
<td align="center">None</td>
<td align="center">String</td>
<td>Password for authentication</td>
<td>It is the access token of the TMP instance in the console</td>
</tr>
<tr>
<td>metrics.reporter.promgateway.<br>deleteOnShutdown</td>
<td align="center">true</td>
<td align="center">Boolean</td>
<td>Whether to delete the corresponding metrics on the Pushgateway after the Flink task is completed</td>
<td>Set it to `true`</td>
</tr>
</tbody></table>
Below is a sample configuration:
```plaintext
metrics.reporter.promgateway.class: org.apache.flink.metrics.prometheus.PrometheusPushGatewayReporter
metrics.reporter.promgateway.jobName: climatePredict
metrics.reporter.promgateway.randomJobNameSuffix:true
metrics.reporter.promgateway.interval: 60 SECONDS
metrics.reporter.promgateway.groupingKey:instance_id=emr-xxxx
metrics.reporter.promgateway.host: 172.xx.xx.xx
metrics.reporter.promgateway.port: 9090
metrics.reporter.promgateway.needBasicAuth: true
metrics.reporter.promgateway.user: appid
metrics.reporter.promgateway.password: token
```

#### Installing Flink Pushgateway plugin

The Pushgateway plugin in the official package currently does not support configuring the authentication information, but TMP requires authentication before data can be written. Therefore, we recommend you use the JAR package we provide. We have also submitted a pull request for supporting authentication to the Flink team.
1. To prevent class conflicts, if you have already used the official Flink plugin, run the following command to delete it first:
```plaintext
cd /usr/local/service/flink/lib
rm flink-metrics-prometheus*jar
```2. In the **[EMR console](https://console.cloud.tencent.com/emr)**, select the corresponding **instance**, and select **Cluster Resource** > **Resource Management** > **Master** to view the master node.
3. Click the instance ID to go to the CVM console, log in to the CVM instance, and run the following command to install the plugin:
```plaintext
cd /usr/local/service/flink/lib
wget https://rig-1258344699.cos.ap-guangzhou.myqcloud.com/flink/flink-metrics-prometheus_2.11-auth.jar -O flink-metrics-prometheus_2.11-auth.jar
```



#### Verifying

1. Run the `flink run` command on the master node to submit a new task and view the task log:
```plaintext
grep metrics /usr/local/service/flink/log/flink-hadoop-client-*.log
```
2. If the log contains the following content, the configuration is successfully loaded:
![](https://main.qcloudimg.com/raw/316151abb6369f2e73081dc233b46fcd.png)
>!As tasks previously submitted in the cluster use the old configuration file, their metrics are not reported.


### Viewing monitoring information
1. In **Integration Center** in the target TMP instance, find Flink monitoring, install the corresponding Grafana dashboard, and then you can enable the Flink monitoring dashboard.
2. Enter Grafana and click <img src="https://main.qcloudimg.com/raw/84bd9a98b230d2ebc32bfac82a108a87.png" width="2%"> to expand the Flink monitoring panel.
![](https://main.qcloudimg.com/raw/61741ec36dbbd56a6bb3c9072aa6f23f.png)
3. Click **Flink Job List** to view the monitoring information.
![](https://qcloudimg.tencent-cloud.cn/raw/44f6349cfd103ae208215ccdeb4e3977.png)
3. Click a **job name** or **job ID** in the table to view the job monitoring details.
![](https://qcloudimg.tencent-cloud.cn/raw/16041098ba6bc50b523c7e475d7ddfef.png)
4. Click **Flink Cluster** in the top-right corner to view the Flink cluster monitoring information.
![](https://qcloudimg.tencent-cloud.cn/raw/46afb226bd2dde874f63b7bcfac058b5.png)
5. Click a **task name** in the table to view the task monitoring details.
![](https://qcloudimg.tencent-cloud.cn/raw/9cbfc534913aec38d60a64f69c53d98a.png)




### Integrating with alert feature

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and select the target TMP instance to enter the management page.
2. Click **Alerting Rule** and add the corresponding alerting rules. For more information, please see Creating Alerting Rule.
