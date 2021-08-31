
This document describes how to use APIs to pull the monitoring data of Tencent Cloud services.


## API Overview


#### Cloud Monitor provides the following two types of APIs for querying metric monitoring data


| API | Operation | Description |
|---------|---------|---------|
| [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) | Queries the details of basic monitoring metric | This API is used to query the types of basic monitoring metrics under the corresponding namespace |
| [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/33881) | Pulls metric monitoring data | This API is used to get the corresponding monitoring data of a metric in the object dimension |



#### API limits

- The `GetMonitorData` API supports getting the monitoring data of a certain metric for all instances under an account in batches.
- The `GetMonitorData` API can be called 20 times per second (1,200 times/minute) by default. A single request can get the data of up to 10 instances and up to 1,440 data points.
- The retention period of monitoring data varies by monitoring granularity as detailed below:
	<table>
<thead>
<tr>
<th>Monitoring Granularity</th>
<th>Retention Period</th>
</tr>
</thead>
<tbody><tr>
<td>1 second</td>
<td>1 day</td>
</tr>
<tr>
<td>1 minute</td>
<td>15 days</td>
</tr>
<tr>
<td>5 minutes</td>
<td>31 days</td>
</tr>
<tr>
<td>1 hour</td>
<td>93 days</td>
</tr>
<tr>
<td>1 day</td>
<td>186 days</td>
</tr>
</tbody></table>

>?The monitoring data of 1-minute metrics related to CPU, memory, and network for CVM is retained for 31 days.






## Preparations


### Preparing personal key[](id:step1)

1. Go to [Manage API Key](https://console.cloud.tencent.com/cam/capi).
2. If no key has been created, you need to click **Create Key** to create a key. If you have already created a key, you can click **Display** after `SecretKey` to get the key.
![](https://main.qcloudimg.com/raw/dfc5cf24f6d04bcf87a64ec325b6e915.png)


### Preparing Tencent Cloud service metric information[](id:step2)


This document takes the CVM CPU utilization metric as an example.

1. 	Go to [CVM Monitoring Metrics](https://intl.cloud.tencent.com/document/product/248/6843).
2. 	Find the CPU utilization metric to view the CPU utilization metric name, dimension, statistical period, and other related information.
![](https://main.qcloudimg.com/raw/0140541d15e09a5ae4b41394f4f529e4.png)


## Directions

This demo describes how to use the [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/33881) API to query the CPU utilization of a CVM instance.

1. Log in to [API Explorer](https://console.cloud.tencent.com/api/explorer?Product=monitor&Version=2018-07-24&Action=GetMonitorData&SignVersion=).
2. Copy the [prepared personal key](#step1) into the corresponding **SecretId** and **SecretKey** text boxes.
3. Find **Region** in the **Input Parameters** section and select the relevant region.
4. Enter the [prepared Tencent Cloud service information](#step2) in the corresponding text boxes in the **Input Parameters** section.
 - **Namespace**: enter QCE/CVM.
 - **MetricName**: enter the name of the CPU utilization metric, i.e., **CPUUsage**.
 - **Dimensions.N-Name**: enter the supported dimension name, i.e., **InstanceId**.
 - **Dimensions.N-Value**: enter the corresponding **InstanceId** value (CVM instance ID), such as **ins—12345678**, which can be obtained through the [DescribeInstances](https://intl.cloud.tencent.com/document/product/213/33258) API of CVM.
 - **Period**: enter a statistical period supported by the metric, such as 300.
 - **StartTime**: enter the query start time in the format of `2020-12-20T19:51:23+08:00` (in the `datetime_iso` type).
 - **EndTime**: enter the query end time in the format of `2020-12-20T20:51:23+08:00` (in the `datetime_iso` type). **EndTime** cannot be earlier than **StartTime**.
![](https://main.qcloudimg.com/raw/ad04f8261b114d1482a03abef2eaa658.png)
5. After completing the above information, you can copy the code in the corresponding language on the **Code Generation** tab to integrate the relevant monitoring data into your self-built monitoring system. You can also use **Online Call** to send a request to query the monitoring data online.
