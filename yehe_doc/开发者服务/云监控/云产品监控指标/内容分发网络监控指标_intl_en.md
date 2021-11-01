## Namespace
Namespace=QCE/CDN

## Monitoring Metrics

| Parameter | Metric Name | Unit | Dimension |
| ---------------- | ---- | ---- |  ---- |
| Bandwidth | Bandwidth | Mbps | projectId and domain |
| Requests | Requests | Times | projectId and domain |
| BackOriginBandwidth | Origin-pull bandwidth | Mbps | projectId and domain |
| BackOriginFailRate | Origin-pull failure rate | % | projectId and domain |
| BackOriginFlux | Origin-pull traffic | GB | projectId and domain |
| BackOriginSpeed | Origin-pull rate | KB/s | projectId and domain |
| Flux | Traffic | GB | projectId and domain |
| RequestsHitRate | Request hit rate | % | projectId and domain |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | --------- | ---- | ---------------------- |
| Instances.N.Dimensions.0.Name | projectId | Project dimension name | Enter a string-type dimension name, such as projectId |
| Instances.N.Dimensions.0.Value | projectId | A specific project ID | Enter a specific project ID, such as 1 |
| Instances.N.Dimensions.0.Name | domain | Dimension name of the domain name | Enter a string-type dimension name, such as domain |
| Instances.N.Dimensions.0.Value | domain | A specific domain name | Enter a specific domain name, such as `www.qq.com` |

## Input Parameters

To query the monitoring data of a CDN instance, use the following input parameter values:
&Namespace= QCE/CDN
&Instances.N.Dimensions.0.Name=projectId
&Instances.N.Dimensions.0.Value=<Project ID>
&Instances.N.Dimensions.1.Name=domain
&Instances.N.Dimensions.1.Value=<Domain name> 



