## Overview

COS statistics such as read and write requests and traffic are collected and displayed by [Cloud Monitor](https://cloud.tencent.com/doc/product/248). You can view detailed monitoring data in the Cloud Monitor Console.

>! This document describes how to get statistics in the COS Console. For more information on how to use Cloud Monitor APIs to get more detailed data, see [Cloud Monitoring product documentation](https://cloud.tencent.com/document/product/248).

## Basic Features

Cloud Monitor provides the following entries for COS to implement monitoring and alarming.

| Module | Capabilities | Main Features |
| ---------- | ---------------------------------------- | ------------------------------------------------------------ |
| Monitoring overview | Displays the current status of the product | Provides general overview, alarm overview, and overall monitoring information |
| Alarm management | Supports alarm management and configuration | Supports creating new COS alarming policies, custom messages, and trigger templates |
| Monitoring platform | Monitors traffic and displays data of user-defined monitoring metrics | Displays your overall bandwidth information and allows you to customize monitoring metrics and data to be reported |
| Cloud product monitoring | Displays the COS bucket monitoring view | Allows you to query the current monitoring views and data such as read and write requests and traffic for each bucket |

## Use Cases

- **Daily management**: you can log in to the Cloud Monitor Console to view the running status of COS in real time.
- **Troubleshooting**: you will receive alarm notifications when a monitoring metric reaches the alarming threshold, allowing you to quickly get notifications for exceptions, check the causes, and fix them in a timely manner.

## Viewing in the Console

You can log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/product/COS) to view the monitoring data for COS.

## Calling APIs

You can view the monitoring data for COS by calling the corresponding APIs. For more information, see [COS Monitoring APIs](https://cloud.tencent.com/document/product/248/13655). Below are the monitoring metrics for COS.

### Storage 

| Metric Name | Description | Unit |
| ---------------------- | ----------------- | ---- |
| std_storage | Standard storage - storage capacity | MB |
| sia_storage | Standard_IA storage - storage capacity | MB |
| nel_storage | Nearline Storage - storage capacity | MB |
| arc_storage | Archive storage - storage capacity | MB |

### Traffic

| Metric Name | Description | Unit |
| ---------------------- | ------------ | ---- |
| internet_traffic | Public network traffic | B |
| internal_traffic | Private network traffic | B |
| cdn_origin_traffic | CDN origin-pull traffic | B |
| inbound_traffic | Upload traffic | B |

### Data Retrieval

| Metric Name | Description | Unit |
| ---------------------- | ------------ | ---- |
| std_retrieval | Standard data retrieval | B |
| sia_retrieval | Standard_IA data retrieval | B |
| nel_retrieval | Nearline data retrieval | B |

### Requests

| Metric Name | Description | Unit |
| ---------------------- | -------------- | ---- |
| std_read_requests | Standard storage read requests | / |
| std_write_requests | Standard storage write requests | / |
| ia_read_requests | Standard_IA storage read requests | / |
| ia_write_requests | Standard_IA storage write requests | / |
| nl_read_requests | Nearline storage read requests | / |
| nl_write_requests | Nearline storage write requests | / |

### Return Codes

| Metric Name | Description | Unit |
| ---------------------- | ---------- | ---- |
| 2xx_response | 2xx status codes | / |
| 3xx_response | 3xx status codes | / |
| 4xx_response | 4xx status codes | / |
| 5xx_response | 5xx status codes | / |

## Monitoring Descriptions

- **Monitoring interval**: Cloud Monitor supports multiple types of monitoring intervals, including monitoring data in real time, in the past 24 hours, in the past 7 days, and in user-specified period, with time granularity of 1 minute or 5 minutes.
- **Data retention**: monitoring data with 1-minute, 5-minute, and 1-hour granularity will be retained for 31 days; monitoring data with 1-day granularity will be retained for half a year.
- **Alarm display**: Cloud Monitor integrates the monitoring data of COS and displays the data entries in intuitive graphs, making it easier for you to stay informed of the overall status.
- **Alarm setting**: you can set alarm-triggering thresholds for the metrics. Cloud Monitor will send notifications to specified recipients when the alarm is triggered. For more information, see [Creating an Alarm](https://cloud.tencent.com/doc/product/248/6126).
