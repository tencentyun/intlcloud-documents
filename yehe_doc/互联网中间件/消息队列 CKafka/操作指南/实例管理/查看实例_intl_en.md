## Overview
This document describes how to view the configuration information and status of an instance in the CKafka console.


## Directions
1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter its **Basic Information** page, where you can view various information of the instance such as the status, configuration information, access mode, message retention period, and automatic topic creation. 
![](https://main.qcloudimg.com/raw/9a5c540c585cba47ff5db2c1c8efda40.png)
> ?
>- The private IP and port (such as `10.6.206.110:9092`) in **Configuration Info** represents the communication address used to get the backend service. There may be multiple ports in a real access address. If access control is configured on your server, open ports 9092–9192 to the internet on it (the broker may be automatically scaled up, and more ports will need to be opened after the scale-up; therefore, you should reserve a sufficient number of ports).
> - Once you enable the automatic topic creation feature for the server, when you use or access metadata of a topic that does not exist, it will be automatically created with the configured number of replicas and partitions.
>- The total number of topics that can be automatically created varies by instance specification. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/597/11745).

## Status Description
CKafka runs an inspection program for each instance, which checks for metrics such as the number of connections to the instance, disk usage percentage, production peak bandwidth, and consumption peak bandwidth. The instance status varies based on these metric values. When one of the metric values exceeds a certain threshold, the instance status will change as detailed below:
<table>
<tr><th>Metric</th><th>Threshold (N)</th><th>Status Description</th></tr>
<tr><td rowspan="3">Number of connections (default maximum value: 5000)</td><td>N ≤ 80%</td><td>Healthy</td></tr>
<tr><td>80% < N ≤ 95%</td><td>Warning</td></tr>
<tr><td>N > 95%</td><td>Exception</td></tr>
<tr><td rowspan="3">Disk usage percentage</td><td>N ≤ 80%</td><td>Healthy</td></tr>
<tr><td>80% < N ≤ 95%</td><td>Warning</td></tr>
<tr><td>N > 95%</td><td>Exception</td></tr>
<tr><td rowspan="3">Production peak bandwidth (excluding replica bandwidth)</td><td>N ≤ 80%</td><td>Healthy</td></tr>
<tr><td>80% < N ≤ 100%</td><td>Warning</td></tr>
<tr><td>N > 100%</td><td>Exception</td></tr>
<tr><td rowspan="3">Consumption peak bandwidth</td><td>N ≤ 80%</td><td>Healthy</td></tr>
<tr><td>80% < N ≤ 100%</td><td>Warning</td></tr>
<tr><td>N > 100%</td><td>Exception</td></tr>
</table>

>!The maximum number of allowed connections to an instance is 5000 by default. The system determines thresholds based on this number. If the number of connections has reached the maximum value, clients cannot build new connections with the instance. If this default maximum number does not meet your business requirements, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=%E6%B6%88%E6%81%AF%E6%9C%8D%E5%8A%A1%20CKafKa&level3_id=955&radio_title=%E9%85%8D%E9%A2%9D%E6%8F%90%E5%8D%87%E7%94%B3%E8%AF%B7&queue=81&scene_code=18356&step=2) to set it to a larger number.



