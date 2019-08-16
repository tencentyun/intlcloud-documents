## Overview

COS statistics such as read and write requests and traffic are collected and displayed based on [Cloud Monitor](https://intl.cloud.tencent.com/doc/product/248). You can view detailed monitoring data of COS in the Cloud Monitor Console.

> This document mainly describes how statistics are displayed in the COS Console. For more information on how to use Cloud Monitor APIs to get more detailed information, see [Cloud Monitoring product documentation](https://intl.cloud.tencent.com/document/product/248).

## Basic Features

Cloud Monitor provides the following entries for COS to implement monitoring and alarming.

| Module | Capabilities | Main Features |
| ---------- | ---------------------------------------- | ------------------------------------------------------------ |
| Monitoring overview | Displays the current status of the product | Provides product overview, alarm overview, and overall monitoring information |
| Alarm management | Supports alarm management and configuration | Supports creating COS alarm policies, customizing messages, and configuring trigger templates |
| Monitoring platform | Monitors traffic and displays data of user-defined monitoring metrics | Displays your overall bandwidth information and allows you to pre-define monitoring metrics and reported data |
| Cloud product monitoring | Displays the COS bucket monitoring view | Queries the current monitoring views and data such as read and write requests and traffic in each bucket |

## Use Cases

- **Daily management**: The running status of COS can be viewed in real time by logging in to the Cloud Monitor Console.
- **Troubleshooting**: Alarm notifications will be sent when a monitoring metric reaches the alarm threshold, allowing you to quickly receive notifications for exceptions, analyze their causes, and fix them in a timely manner.

## Viewing in the Console

You can view the monitoring data of COS by logging in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/product/COS).

## Calling Through APIs

You can view the monitoring data of COS by calling the corresponding APIs. 

### Storage

| Metric Name | Meaning | Unit |
| ---------------------- | ----------------- | ---- |
| std_storage | Standard storage - storage capacity | MB |
| sia_storage | Standard_IA storage - storage capacity | MB |
| nel_storage | Nearline Storage - storage capacity | MB |
| arc_storage | Archive storage - storage capacity | MB |

### Traffic

| Metric Name | Meaning | Unit |
| ---------------------- | ------------ | ---- |
| internet_traffic | Public network traffic | B |
| internal_traffic | Private network traffic | B |
| cdn_origin_traffic | CDN origin-pull traffic | B |
| inbound_traffic | Upload traffic | B |

### Data Reads

| Metric Name | Meaning | Unit |
| ---------------------- | ------------ | ---- |
| std_retrieval | Standard data reads | B |
| sia_retrieval | Standard_IA data reads | B |
| nel_retrieval | Nearline data reads | B |

### Requests

| Metric Name | Meaning | Unit |
| ---------------------- | -------------- | ---- |
| std_read_requests | Standard storage read requests | / |
| std_write_requests | Standard storage write requests | / |
| ia_read_requests | Standard_IA storage read requests | / |
| ia_write_requests | Standard_IA storage write requests | / |
| nl_read_requests | Nearline storage read requests | / |
| nl_write_requests | Nearline storage write requests | / |

### Return Codes

| Metric Name | Meaning | Unit |
| ---------------------- | ---------- | ---- |
| 2xx_response | 2xx status codes | / |
| 3xx_response | 3xx status codes | / |
| 4xx_response | 4xx status codes | / |
| 5xx_response | 5xx status codes | / |

## Monitoring Descriptions

- **Monitoring interval**: Cloud Monitor supports multiple statistical intervals for data monitoring, such as real time, past 24 hours, past 7 days, and custom data range, with time granularities of 1 minute or 5 minutes.
- **Data retention**: Monitoring data with 1-minute, 5-minute, and 1-hour granularity is retained for 31 days, while monitoring data with 1-day granularity is retained for half a year.
- **Alarm display**: Cloud Monitor integrates the monitoring data of COS and displays the data entries in intuitive graphs, making it easier for you to stay informed of the overall operations.
- **Alarm setting**: Metric thresholds can be set, so that when a monitoring metric triggers an alarm, Cloud Monitor can send alarm notifications to concerned groups in a timely manner. For more information, see [Creating an Alarm](https://intl.cloud.tencent.com/doc/product/248/6126).
