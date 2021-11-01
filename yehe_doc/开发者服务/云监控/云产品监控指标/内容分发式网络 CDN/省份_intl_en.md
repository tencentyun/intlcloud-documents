## Namespace

Namespace=QCE/CDN_LOG_DATA

## Monitoring Metrics

| Parameter | Metric | Unit | Dimension |
| ------------- | -------------- | ---- | ----------------------------- |
| Bandwidth     | Bandwidth           | Mbps | domain, isp, projectid, province |
| Traffic       | Traffic           | MB   | domain, isp, projectid, province |
| HitTraffic    | Cache-hitting traffic | MB   | domain, isp, projectid, province |
| RequestTotal  | Total number of requests     | -   | domain, isp, projectid, province |
| HttpStatus2xx | 2xx status code      | -   | domain, isp, projectid, province |
| HttpStatus3xx | 3xx status code      | -   | domain, isp, projectid, province |
| HttpStatus4xx | 4xx status code      | -   | domain, isp, projectid, province |
| HttpStatus5xx | 5xx status code      | -   | domain, isp, projectid, province |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | --------- | ---------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.Name  | province  | Province dimension name     | Enter a String-type dimension name: province                            |
| Instances.N.Dimensions.0.Value | province  | Province             | Enter a province, such as `Guangdong`                                         |
| Instances.N.Dimensions.1.Name  | isp       | ISP dimension name   | Enter a String-type dimension name: isp                                 |
| Instances.N.Dimensions.1.Value | isp       | Specific ISP name   | Enter a specific ISP name |
| Instances.N.Dimensions.2.Name  | projectId | Project dimension name     | Enter a String-type dimension name: projectId                           |
| Instances.N.Dimensions.2.Value | projectId | Specific project ID       | Enter a specific project ID, such as `1`                                     |
| Instances.N.Dimensions.3.Name  | domain    | Overseas domain dimension name | Enter a String-type dimension name: domain                              |
| Instances.N.Dimensions.3.Value | domain    | Specific domain         | Enter a specific domain              |

## Input Parameter Description

**To query the monitoring data of a CDN instance, set the following input parameters:**
&Namespace=QCE/CDN_LOG_DATA
&Instances.N.Dimensions.0.Name=province
&Instances.N.Dimensions.0.Value=province name
&Instances.N.Dimensions.1.Name=isp
&Instances.N.Dimensions.1.Value=specific ISP name
&Instances.N.Dimensions.2.Name=projectId
&Instances.N.Dimensions.2.Value=project ID
&Instances.N.Dimensions.3.Name=domain
&Instances.N.Dimensions.3.Value=domain name 

