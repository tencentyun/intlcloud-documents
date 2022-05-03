## Overview

COS data (such as traffic and the number of read/write requests) is collected and displayed according to [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248). Therefore, you can go to the COS or [Cloud Monitor console](https://console.cloud.tencent.com/monitor) to view COS monitoring data in detail.

>?This document describes how to obtain statistics in the COS console. You can call Cloud Monitor APIs to obtain more detailed data. For more information, see [Documentation of Cloud Monitor](https://intl.cloud.tencent.com/document/product/248).

## Basic Features

Cloud Monitor provides the following modules for COS to implement monitoring and alarming.

| Module | Capability | Main Feature |
| ---------- | ---------------------------------------- | ------------------------------------------------------------ |
| Monitoring overview | Displays the current status of the product | Provides general overview, alarm overview, and overall monitoring information |
| Alarm management | Supports alarm management and configuration | Supports creating new COS alarm policies, custom messages, and trigger templates |
| Monitoring platform | Monitors traffic and displays data of user-defined monitoring metrics | Displays your overall bandwidth information and allows you to customize monitoring metrics and data to be reported |
| Cloud product monitoring | Displays the COS bucket monitoring view | Allows you to query the current monitoring views and data such as read/write requests and traffic for each bucket |

## Use Cases

- **Daily management**: You can log in to the Cloud Monitor console to view the running status of COS in real time.
- **Troubleshooting**: You can receive alarm notifications when the data of a monitoring metric reaches the threshold. It allows you to quickly notify the exceptions, find out the causes, and fix the issues.

## Setting and Querying via Console

You can create an alarm policy for COS in the [Cloud Monitor console](https://console.cloud.tencent.com/monitor). If the data of a monitoring metric reaches the specified threshold, you will receive an alarm notification. For detailed directions, see [Setting Monitoring Alarms](https://intl.cloud.tencent.com/document/product/436/39104).

You can go to **Cloud Product Monitoring > [Cloud Object Storage](https://console.cloud.tencent.com/monitor/product/COS)** to view the COS monitoring data (including the monitoring data of all buckets, health status, number of alarm policies, and more). Alternatively, you can go to the COS console to view the data. For detailed directions, see [Viewing Data Overview](https://intl.cloud.tencent.com/document/product/436/36542) and [Querying Monitoring Data](https://intl.cloud.tencent.com/document/product/436/31634).

## Querying Monitoring Data via APIs

You can call the corresponding APIs to view the COS monitoring data. The monitoring metrics are described below. For more information about the monitoring APIs, see [COS Monitoring Metrics](https://intl.cloud.tencent.com/document/product/248/37269).

## Monitoring Metrics

> ?COS uses a generic region. Therefore, select "Guangzhou" for `Region` when you pull COS monitoring metric data, regardless of where the bucket resides.
> - When pulling data using [API Explorer](https://console.cloud.tencent.com/api/explorer?Product=monitor&Version=2018-07-24&Action=DescribeBaseMetrics), select "ap-guangzhou" for the `Region` field.
> - When pulling data using an SDK, enter "ap-guangzhou" for the `Region` field.

### Request metrics

| Metric | Meaning | Description | Unit | Dimension |
| -------------------- | ------------------------ | ------------------------------------------------------------ | ---- | ------------- |
| StdReadRequests | STANDARD read requests | Number of STANDARD read requests, which is calculated based on the number of requests sent | - | appid, bucket |
| StdWriteRequests | STANDARD write requests | Number of STANDARD write requests, which is calculated based on the number of requests sent | - | appid, bucket |
| IaReadRequests | STANDARD_IA read requests | Number of STANDARD_IA read requests, which is calculated based on the number of requests sent | - | appid, bucket |
| IaWriteRequests | STANDARD_IA write requests | Number of STANDARD_IA write requests, which is calculated based on the number of requests sent | - | appid, bucket |
|  DeepArcReadRequests | DEEP ARCHIVE read requests | Number of DEEP ARCHIVE read requests, which is calculated based on the number of requests sent | - | appid, bucket |
| DeepArcWriteRequests | DEEP ARCHIVE write requests | Number of DEEP ARCHIVE write requests, which is calculated based on the number of requests sent | - | appid, bucket |
| ItReadRequests | INTELLIGENT TIERING read requests | Number of INTELLIGENT TIERING read requests, which is calculated based on the number of requests sent | - | appid, bucket |
| ItWriteRequests | INTELLIGENT TIERING write requests | Number of INTELLIGENT TIERING write requests, which is calculated based on the number of requests sent | - | appid, bucket |
| TotalRequests | Total requests | Total number of read and write requests in all storage classes, which is calculated based on the number of requests sent | - | appid, bucket |
| GetRequests | Total GET requests | Total number of GET requests in all storage classes, which is calculated based on the number of requests sent | - | appid, bucket |
| PutRequests | Total PUT requests | Total number of PUT requests in all storage classes, which is calculated based on the number of requests sent | - | appid, bucket |

### Storage metrics

| Metric | Description | Unit | Dimension |
| ---------------------------- | --------------------------------- | ---- | ------------- |
| StdStorage | STANDARD - storage capacity | MB | appid, bucket |
| SiaStorage | STANDARD_IA - storage capacity | MB | appid, bucket |
| ItFreqStorage                | INTELLIGENT_TIERING - frequent storage space       | MB   | appid, bucket |
| ItInfreqStorage              | INTELLIGENT_TIERING - infrequent storage space       | MB   | appid, bucket |
| ArcStorage | ARCHIVE - storage capacity | MB | appid, bucket |
| DeepArcStorage | DEEP ARCHIVE - storage capacity | MB | appid, bucket |
| StdObjectNumber | STANDARD - number of objects | - | appid, bucket |
| IaObjectNumber | STANDARD_IA - number of objects | - | appid, bucket |
| ItFreqObjectNumber           | INTELLIGENT TIERING - number of frequently accessed objects | - | appid, bucket |
| ItInfreqObjectNumber         | INTELLIGENT TIERING - number of infrequently accessed objects | - | appid, bucket |
| ArcObjectNumber | ARCHIVE - number of objects | - | appid, bucket |
| DeepArcObjectNumber          | DEEP_ARCHIVE - number of objects              | -   | appid, bucket |
| StdMultipartNumber | STANDARD - number of incomplete multipart uploads | - | appid, bucket |
| IaMultipartNumber | STANDARD_IA - number of incomplete multipart uploads | - | appid, bucket |
| ItFrequentMultipartNumber | INTELLIGENT TIERING (frequent access tier) - number of incomplete multipart uploads | - | appid, bucket |
| ArcMultipartNumber | ARCHIVE - number of incomplete multipart uploads | - | appid, bucket |
| DeepArcMultipartNumber | DEEP ARCHIVE - number of incomplete multipart uploads | - | appid, bucket |

### Traffic metrics

| Metric | Meaning | Description | Unit | Dimension |
| ----------------------------- | -------------------- | -------------------------------------------------------- | ---- | ------------- |
| InternetTraffic | Public network downstream traffic  | Traffic generated by downloading data from COS to a client over the Internet | Byte | appid, bucket |
| InternetTrafficUp | Public network upstream traffic | Traffic generated by uploading data from a client to COS over the Internet | Byte | appid, bucket |
| InternalTraffic | Private network downstream traffic | Traffic generated by downloading data from COS to a client over a Tencent Cloud private network | Byte | appid, bucket |
| InternalTrafficUp | Private network upstream traffic | Traffic generated by uploading data from a client to COS over a Tencent Cloud private network | Byte | appid, bucket |
| CdnOriginTraffic | CDN origin-pull traffic | Traffic generated by transferring data from COS to Tencent Cloud CDN edge node | Byte | appid, bucket |
| InboundTraffic | Total upload traffic over public and private networks | Traffic generated by uploading data from a client to COS over a Tencent Cloud private network or the Internet | Byte | appid, bucket |
| CrossRegionReplicationTraffic | Cross-region replication traffic | Traffic generated by replicating data to a bucket in another region | Byte | appid, bucket |

### Return code metrics

| Metric | Meaning | Description | Unit | Dimension |
| --------------- | -------------- | ----------------------------------------------- | ---- | ------------- |
| 2xxResponse | 2xx status code | Number of requests with a 2xx status code returned | - | appid, bucket |
| 3xxResponse | 3xx status code | Number of requests with a 3xx status code returned | - | appid, bucket |
| 4xxResponse | 4xx status code | Number of requests with a 4xx status code returned | - | appid, bucket |
| 5xxResponse | 5xx status code | Number of requests with a 5xx status code returned | - | appid, bucket |
| 2xxResponseRate | Proportion of 2xx status code | Proportion of the requests with a 2xx status code returned in the total requests | % | appid, bucket |
| 3xxResponseRate | Proportion of 3xx status code | Proportion of the requests with a 3xx status code returned in the total requests | % | appid, bucket |
| 4xxResponseRate | Proportion of 4xx status code | Proportion of the requests with a 4xx status code returned in the total requests | % | appid, bucket |
| 5xxResponseRate | Proportion of 5xx status code | Proportion of the requests with a 5xx status code returned in the total requests | % | appid, bucket |
| 400Response | 400 status code | Number of requests with a 400 status code returned | - | appid, bucket |
| 403Response | 403 status code | Number of requests with a 403 status code returned | - | appid, bucket |
| 404Response | 404 status code | Number of requests with a 404 status code returned | - | appid, bucket |
| 400ResponseRate | Proportion of 400 status code | Proportion of the requests with a 400 status code returned in the total requests | % | appid, bucket |
| 403ResponseRate | Proportion of 403 status code | Proportion of the requests with a 403 status code returned in the total requests | % | appid, bucket |
| 404ResponseRate | Proportion of 404 status code | Proportion of the requests with a 404 status code returned in the total requests | % | appid, bucket |
| 500ResponseRate | Proportion of 500 status code | Proportion of the requests with a 500 status code returned in the total requests | % | appid, bucket |
| 501ResponseRate | Proportion of 501 status code | Proportion of the requests with a 501 status code returned in the total requests | % | appid, bucket |
| 502ResponseRate | Proportion of 502 status code | Proportion of the requests with a 502 status code returned in the total requests | % | appid, bucket |
| 503ResponseRate | Proportion of 503 status code | Proportion of the requests with a 503 status code returned in the total requests | % | appid, bucket |

> ?
> 1. For more information about 3xx, 4xx, and 5xx status codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
> 2. The statistical granularity (`period`) may vary by metric. You can call the [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API to obtain the `period` supported by each metric.

### Data retrieval metrics

| Metric | Meaning | Description | Unit | Dimension |
| ------------ | -------------- | ------------------------------------------------------------ | ---- | ------------- |
| StdRetrieval | STANDARD data retrieval | Traffic generated by the retrieval of STANDARD data, which is the sum of the public network downstream traffic, private network downstream traffic, and CDN origin-pull traffic in the  STANDARD storage class | B | appid, bucket |
| IaRetrieval | STANDARD_IA data retrieval | Traffic generated by the retrieval of STANDARD_IA data, which is the sum of the public network downstream traffic, private network downstream traffic, and CDN origin-pull traffic in the  STANDARD_IA storage class | B | appid, bucket |


### Data processing metrics

You can call the corresponding APIs to view the CI monitoring data. For more information on monitoring APIs, see [CI Monitoring Metrics].



## Dimensions and Parameters

| Parameter | Dimension | Description | Format |
| ------------------------------- | -------- | ----------------------- | -------------------------------------------------- |
| &Instances.N.Dimensions.0.Name | appid | Dimension name of the root account `APPID` | Enter a string-type dimension name, such as appid |
| &Instances.N.Dimensions.0.Value | appid    | Specific root account APPID      | Enter a root account APPID, such as `1250000000`                 |
| &Instances.N.Dimensions.1.Name | bucket | Dimension name of the bucket | Enter a string-type dimension name, such as bucket |
| &Instances.N.Dimensions.1.Value | bucket   | Specific bucket name          | Enter a specific bucket name, such as `examplebucket-1250000000` |



## Input Parameters

To query COS monitoring data, the values of the input parameters are as follows:

&Namespace=QCE/COS
&Instances.N.Dimensions.0.Name=appid
&Instances.N.Dimensions.0.Value=root account APPID
&Instances.N.Dimensions.1.Name=bucket
&Instances.N.Dimensions.1.Value=bucket name 


## Monitoring Description

- **Monitoring interval**: Cloud Monitor supports multiple monitoring intervals, including monitoring data in real time, in the past 24 hours, in the past 7 days, and in the user-specified period, with time granularity of 1 minute, 5 minutes, 1 hour, and 1 day.
- **Data storage**: 1-minute monitoring data can be stored for 15 days, 5-minute monitoring data for 31 days, 1-hour data for 93 days, and 1-day monitoring data for 186 days.
- **Alarm display**: Cloud Monitor integrates the monitoring data of COS and displays the data in graphs. Alarm notifications can be sent to you according to the predefined alarm metrics of your product. In this way, you can stay informed of the overall running status.
- **Alarm settings**: You can set the threshold for the monitoring metrics. When the monitoring data meets the alarm condition that is set, Cloud Monitor will send the alarm notifications to the specified users. For more information, see [Cloud Monitor Overview](https://intl.cloud.tencent.com/document/product/248/6126) and [Setting Monitoring Alarms](https://intl.cloud.tencent.com/document/product/436/39104).




