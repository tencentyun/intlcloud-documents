# Overview

COS data (such as traffic and the number of read/write requests) is collected and displayed according to [Basic Cloud Monitor](https://intl.cloud.tencent.com/document/product/248). Therefore, you can go to the COS or Cloud Monitor console to view COS monitoring data in detail.

>?This document describes how to obtain statistics in the COS console. You can call Cloud Monitor APIs to obtain more detailed data. For more information, please see [Documentation of Cloud Monitor](https://intl.cloud.tencent.com/document/product/248).

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

You can create an alarm policy for COS in the [Cloud Monitor console](https://console.cloud.tencent.com/monitor). If the data of a monitoring metric reaches the specified threshold, you will receive an alarm notification. For detailed directions, please see [Setting Monitoring Alarms](https://intl.cloud.tencent.com/document/product/436/39104).

You can go to **Cloud Product Monitoring** > [Cloud Object Storage](https://console.cloud.tencent.com/monitor/product/COS) to view the COS monitoring data (including the monitoring data of all buckets, health status, number of alarm policies, and more). Alternatively, you can go to the COS console to view the data. For detailed directions, please see [Viewing Data Overview](https://intl.cloud.tencent.com/document/product/436/36542) and [Querying Monitoring Data](https://intl.cloud.tencent.com/document/product/436/31634).

## Querying Monitoring Data via APIs

You can call APIs to view the COS monitoring data. The following table describes the COS monitoring metrics:

#### Storage metrics

| Metric Name | Description | Unit |
| ---------------------- | ----------------- | ---- |
| std_storage | STANDARD storage - storage capacity | MB |
| sia_storage | STANDARD_IA storage - storage capacity | MB |
| nel_storage | Nearline Storage - storage capacity | MB |
| arc_storage | ARCHIVE storage - storage capacity | MB |

#### Traffic metrics

| Metric Name | Description | Unit |
| ---------------------- | ------------ | ---- |
| internet_traffic | Public network traffic | B |
| internal_traffic | Private network traffic | B |
| cdn_origin_traffic | CDN origin-pull traffic | B |
| inbound_traffic | Upload traffic | B |

#### Data retrieval metrics

| Metric Name | Description | Unit |
| ---------------------- | ------------ | ---- |
| std_retrieval | STANDARD data retrieval | B |
| sia_retrieval | STANDARD_IA data retrieval | B |
| nel_retrieval | Nearline data retrieval | B |

#### Request metrics

| Metric Name | Description | Unit |
| ---------------------- | -------------- | ---- |
| std_read_requests | STANDARD storage read requests | times |
| std_write_requests | STANDARD storage write requests | times |
| ia_read_requests | STANDARD_IA storage read requests | times |
| ia_write_requests | STANDARD_IA storage write requests | times |
| nl_read_requests | Nearline storage read requests | times |
| nl_write_requests | Nearline storage write requests | times |

#### Return code metrics

| Metric Name | Description | Unit |
| ---------------------- | ---------- | ---- |
| 2xx_response | 2xx status codes | times |
| 3xx_response | 3xx status codes | times |
| 4xx_response | 4xx status codes | times |
| 5xx_response | 5xx status codes | times |

## Monitoring Description

- **Monitoring interval**: Cloud Monitor supports multiple monitoring intervals, including monitoring data in real time, in the past 24 hours, in the past 7 days, and in the user-specified period, with time granularity of 1 minute, 5 minutes, 1 hour, and 1 day.
- **Data storage**: 1-minute monitoring data can be stored for 15 days, 5-minute monitoring data for 31 days, 1-hour data for 93 days, and 1-day monitoring data for 186 days.
- **Alarm display**: Cloud Monitor integrates the monitoring data of COS and displays the data in graphs. Alarm notifications can be sent to you according to the predefined alarm metrics of your product. In this way, you can stay informed of the overall running status.
- **Alarm settings**: You can set the threshold for the monitoring metrics. When the monitoring data meets the alarm condition that is set, Cloud Monitor will send the alarm notifications to the specified users. For more information, please see [Cloud Monitor Overview](https://intl.cloud.tencent.com/document/product/248/38910) and [Setting Monitoring Alarms](https://intl.cloud.tencent.com/document/product/436/39104).

