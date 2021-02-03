## Namespace

Namespace=QCE/CDN

## Monitoring Metrics

### Access

| Parameter | Metric | Unit | Dimension |
| ----------- | ---------- | ---- | ----------------- |
| Bandwidth   | Bandwidth       | Mbps | projectId, domain |
| Flux        | Traffic       | GB   | projectId, domain |
| FluxHitRate | Traffic hit rate | %    | projectId, domain |

### Access requests

| Parameter | Metric | Unit | Dimension |
| --------------- | ------------ | ---- | ----------------- |
| Requests        | Number of requests       | -   | projectId, domain |
| RequestsHitRate | Request hit rate | %    | projectId, domain |

### Origin-pull usage

| Parameter | Metric | Unit | Dimension |
| ------------------- | ---------- | ---- | ----------------- |
| BackOriginBandwidth | Origin-pull bandwidth | Mbps | projectId, domain |
| BackOriginFailRate | Origin-pull failure rate | % | projectId, domain |
| BackOriginSpeed     | Origin-pull rate   | KB/s | projectId, domain |
| BackOriginFlux | Origin-pull traffic | GB | projectId, domain |

### Origin-pull requests

| Parameter | Metric | Unit | Dimension |
| ------------------ | ---------- | ---- | ----------------- |
| BackOriginRequests | Origin-pull requests | -   | projectId, domain |

### Access status codes

| Parameter | Metric | Unit | Dimension |
| ------------------- | ------------------------- | ---- | ----------------- |
| HttpStatus0         | Status code (0)               | -   | projectId, domain |
| HttpStatus0Rate     | Proportion of 0 status code               | %    | projectId, domain |
| HttpStatus200       | Status code (200)             | -   | projectId, domain |
| HttpStatus206       | Status code (206)             | -   | projectId, domain |
| HttpStatus2xx       | Status code (2xx)             | -   | projectId, domain |
| HttpStatus302       | Status code (302)             | -   | projectId, domain |
| HttpStatus304       | Status code (304)             | -   | projectId, domain |
| HttpStatus3xx       | Status code (3xx)             | -   | projectId, domain |
| HttpStatus401       | Status code (401)             | -   | projectId, domain |
| HttpStatus403       | Status code (403)             | -   | projectId, domain |
| HttpStatus403Rate   | Proportion of 403 status code             | %    | projectId, domain |
| HttpStatus404       | Status code (404)             | -   | projectId, domain |
| HttpStatus404Rate   | Proportion of 404 status code             | %    | projectId, domain |
| HttpStatus405       | Status code (405)             | -   | projectId, domain |
| HttpStatus416       | Status code (416)              | -   | projectId, domain |
| HttpStatus4xx       | Status code (4xx)              | -   | projectId, domain |
| HttpStatus4xxRate   | Proportion of 4xx status code             | %    | projectId, domain |
| HttpStatus500       | Status code (500)             | -   | projectId, domain |
| HttpStatus502       | Status code (502)             | -   | projectId, domain |
| HttpStatus5xx       | Status code (5xx)             | -   | projectId, domain |
| HttpStatus5xxRate   | Proportion of 5xx status code             | %   | projectId, domain |
| HttpStatusErrorRate | Proportion of error status codes (4xx + 5xx) | %   | projectId, domain |
| BackOriginHttp200   | Origin-pull status code 200             | -   | projectId, domain |
| BackOriginHttp206   | Origin-pull status code 206             | -   | projectId, domain |
| BackOriginHttp2xx   | Origin-pull status code 2xx             | -   | projectId, domain |
| BackOriginHttp302   | Origin-pull status code 302             | -   | projectId, domain |
| BackOriginHttp304   | Origin-pull status code 304             | -   | projectId, domain |
| BackOriginHttp3xx   | Origin-pull status code 3xx             | -   | projectId, domain |
| BackOriginHttp401   | Origin-pull status code 401             | -   | projectId, domain |
| BackOriginHttp403   | Origin-pull status code 403             | -   | projectId, domain |
| BackOriginHttp404   | Origin-pull status code 404             | -   | projectId, domain |
| BackOriginHttp4xx   | Origin-pull status code 4xx             | -   | projectId, domain |
| BackOriginHttp500   | Origin-pull status code 500             | -   | projectId, domain |
| BackOriginHttp502   | Origin-pull status code 502             | -   | projectId, domain |
| BackOriginHttp5xx   | Origin-pull status code 5xx             | -   | projectId, domain |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | --------- | ------------ | ----------------------------------- |
| Instances.N.Dimensions.0.Name  | projectId | Project dimension name     | Enter a String-type dimension name: projectId |
| Instances.N.Dimensions.0.Value | projectId | Specific project ID      | Enter a specific project ID, such as `1`            |
| Instances.N.Dimensions.0.Name  | domain    | Domain dimension name | Enter a String-type dimension name: domain    |
| Instances.N.Dimensions.0.Value | domain    | Specific domain         | Enter a specific domain                        |

## Input Parameter Description

**To query the monitoring data of a CDN instance, set the following input parameters:**
&Namespace=QCE/CDN
&Instances.N.Dimensions.0.Name=projectId
&Instances.N.Dimensions.0.Value=project ID
&Instances.N.Dimensions.1.Name=domain
&Instances.N.Dimensions.1.Value=domain 
