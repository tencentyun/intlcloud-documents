## Namespace

Namespace=QCE/COS

## Monitoring Metrics

> ?Because COS uses a generic region, no matter where a bucket is located, please always select "Guangzhou" as `Region` when pulling COS monitoring metric data.
> - Please always select "North China (Guangzhou)" for the `Region` field when pulling data by using [API Explorer](https://console.cloud.tencent.com/api/explorer?Product=monitor&Version=2018-07-24&Action=DescribeBaseMetrics).
> - Please always enter "ap-guangzhou" in the `Region` field when pulling data by using an SDK.

### Requests

| Parameter | Metric | Description | Unit | Dimension |
| -------------------- | ------------------------ | ------------------------------------------------------------ | ---- | ------------- |
| StdReadRequests | STANDARD read requests | Number of STANDARD read requests, which is calculated based on the number of sent requests | - | appid, bucket |
| StdWriteRequests | STANDARD write requests | Number of STANDARD write requests, which is calculated based on the number of sent requests | - | appid, bucket |
| MazStdReadRequests | MAZ_STANDARD read requests | Number of MAZ_STANDARD read requests, which is calculated based on the number of sent requests | - | appid, bucket |
| MazStdWriteRequests | MAZ_STANDARD write requests | Number of MAZ_STANDARD write requests, which is calculated based on the number of sent requests | - | appid, bucket |
| IaReadRequests | STANDARD_IA read requests | Number of STANDARD_IA read requests, which is calculated based on the number of sent requests | - | appid, bucket |
| IaWriteRequests | STANDARD_IA write requests | Number of STANDARD_IA write requests, which is calculated based on the number of sent requests | - | appid, bucket |
| MazIaReadRequests | MAZ_STANDARD_IA read requests | Number of MAZ_STANDARD_IA read requests, which is calculated based on the number of sent requests | - | appid, bucket |
| MazIaWriteRequests | MAZ_STANDARD_IA write requests | Number of MAZ_STANDARD_IA write requests, which is calculated based on the number of sent requests | - | appid, bucket |
| DeepArcReadRequests | DEEP_ARCHIVE read requests | Number of DEEP_ARCHIVE read requests, which is calculated based on the number of sent requests | - | appid, bucket |
| DeepArcWriteRequests | DEEP_ARCHIVE write requests | Number of DEEP_ARCHIVE write requests, which is calculated based on the number of sent requests | - | appid, bucket |
| ItReadRequests | INTELLIGENT_TIERING read requests | Number of INTELLIGENT_TIERING read requests, which is calculated based on the number of sent requests | - | appid, bucket |
| ItWriteRequests | INTELLIGENT_TIERING write requests | Number of INTELLIGENT_TIERING write requests, which is calculated based on the number of sent requests | - | appid, bucket |
| MazItReadRequests | MAZ_INTELLIGENT_TIERING read requests | Number of MAZ_INTELLIGENT_TIERING read requests, which is calculated based on the number of sent requests | - | appid, bucket |
| MazItWriteRequests | MAZ_INTELLIGENT_TIERING write requests | Number of MAZ_INTELLIGENT_TIERING write requests, which is calculated based on the number of sent requests | - | appid, bucket |
| TotalRequests | Total requests | Total number of read and write requests in all storage classes, which is calculated based on the number of sent requests | - | appid, bucket |
| GetRequests | Total GET requests | Total number of GET requests in all storage classes, which is calculated based on the number of sent requests | - | appid, bucket |
| PutRequests | Total PUT requests | Total number of PUT requests in all storage classes, which is calculated based on the number of sent requests | - | appid, bucket |

### Storage

| Parameter | Metric | Unit | Dimension |
| ---------------------------- | --------------------------------- | ---- | ------------- |
| StdStorage | STANDARD - storage space | MB | appid, bucket |
| MazStdStorage | MAZ_STANDARD - storage space | MB | appid, bucket |
| SiaStorage | STANDARD_IA - storage space | MB | appid, bucket |
| MazIaStorage                 | MAZ_STANDARD_IA - storage space      | MB   | appid, bucket |
| ItFreqStorage                | INTELLIGENT_TIERING - frequent storage space       | MB   | appid, bucket |
| ItInfreqStorage              | INTELLIGENT_TIERING - infrequent storage space       | MB   | appid, bucket |
| MazItFreqStorage             | MAZ_INTELLIGENT_TIERING - frequent storage space | MB   | appid, bucket |
| MazItInfreqStorage           | MAZ_INTELLIGENT_TIERING - infrequent storage space | MB   | appid, bucket |
| ArcStorage                   | ARCHIVE - storage space                 | MB   | appid, bucket |
| DeepArcStorage               | DEEP_ARCHIVE - storage space             | MB   | appid, bucket |
| StdObjectNumber | STANDARD - number of objects | - | appid, bucket |
| MazStdObjectNumber | MAZ_STANDARD - number of objects | - | appid, bucket |
| IaObjectNumber | STANDARD_IA - number of objects | - | appid, bucket |
| MazIaObjectNumber            | MAZ_STANDARD_IA - number of objects      | -   | appid, bucket |
| ItFreqObjectNumber           | INTELLIGENT_TIERING - number of frequent objects       | -   | appid, bucket |
| ItInfreqObjectNumber         | INTELLIGENT_TIERING - number of infrequent objects       | -   | appid, bucket |
| MazItFreqObjectNumber        | MAZ_INTELLIGENT_TIERING - number of frequent objects       | -   | appid, bucket |
| MazItInfreqObjectNumber      | MAZ_INTELLIGENT_TIERING - number of infrequent objects       | -   | appid, bucket |
| ArcObjectNumber              | ARCHIVE - number of objects                  | -   | appid, bucket |
| DeepArcObjectNumber          | DEEP_ARCHIVE - number of objects              | -   | appid, bucket |
| StdMultipartNumber           | STANDARD - incomplete multipart uploads           | -   | appid, bucket |
| MazStdMultipartNumber        | MAZ_STANDARD - incomplete multipart uploads     | -   | appid, bucket |
| IaMultipartNumber            | STANDARD_IA - incomplete multipart uploads           | -   | appid, bucket |
| MazIaMultipartNumber         | MAZ_STANDARD_IA - incomplete multipart uploads     | -   | appid, bucket |
| ItFrequentMultipartNumber    | INTELLIGENT_TIERING - incomplete multipart uploads       | -   | appid, bucket |
| MazItFrequentMultipartNumber | MAZ_INTELLIGENT_TIERING - incomplete multipart uploads  | -   | appid, bucket |
| ArcMultipartNumber           | ARCHIVE - incomplete multipart uploads           | -   | appid, bucket |
| DeepArcMultipartNumber       | DEEP_ARCHIVE - incomplete multipart uploads           | -   | appid, bucket |

### Traffic

| Parameter | Metric | Description | Unit | Dimension |
| ----------------------------- | -------------------- | -------------------------------------------------------- | ---- | ------------- |
| InternetTraffic           | Public network downstream traffic         | Traffic generated by data download from COS to client over the internet              | B    | appid, bucket |
| InternetTrafficUp             | Public network upstream traffic         | Traffic generated by data upload from client to COS over the internet              | B    | appid, bucket |
| InternalTraffic           | Private network downstream traffic         | Traffic generated by data download from COS to client over the Tencent Cloud private network          | B    | appid, bucket |
| InternalTrafficUp             | Private network upstream traffic         | Traffic generated by data upload from client to COS over the Tencent Cloud private network          | B    | appid, bucket |
| CdnOriginTraffic | CDN origin-pull traffic | Traffic generated by data transfer from COS to Tencent Cloud CDN edge server | B | appid, bucket |
| InboundTraffic | Total public and private network upload traffic | Traffic generated by data upload from client to COS over the internet and Tencent Cloud private network | B | appid, bucket |
| CrossRegionReplicationTraffic | Cross-region replication traffic       | Traffic generated by replication of data in a bucket in one region to another bucket in another region | B    | appid, bucket |

### Return codes

| Parameter | Metric | Description | Unit | Dimension |
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
> 1. For more information on the 3xx, 4xx, and 5xx status codes, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
> 2. The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

### Data retrieval metrics

| Parameter | Metric | Description | Unit | Dimension |
| ------------ | -------------- | ------------------------------------------------------------ | ---- | ------------- |
| StdRetrieval | STANDARD data retrieval | Traffic generated by the retrieval of STANDARD data, which is the sum of the public network downstream traffic, private network downstream traffic, and CDN origin-pull traffic in the STANDARD storage class | B | appid, bucket |
| IaRetrieval | STANDARD_IA data retrieval | Traffic generated by the retrieval of STANDARD_IA data, which is the sum of the public network downstream traffic, private network downstream traffic, and CDN origin-pull traffic in the STANDARD_IA storage class | B | appid, bucket |

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------- | -------- | ----------------------- | -------------------------------------------------- |
| &Instances.N.Dimensions.0.Name  | appid    | Root account APPID dimension name | Enter a String-type dimension name: appid                     |
| &Instances.N.Dimensions.0.Value | appid    | Specific root account APPID      | Enter a root account APPID, such as 1250000000                 |
| &Instances.N.Dimensions.1.Name  | bucket   | Bucket dimension name          | Enter a String-type dimension name: bucket                    |
| &Instances.N.Dimensions.1.Value | bucket   | Specific bucket name          | Enter a specific bucket name, such as examplebucket-1250000000 |

## Input Parameter Description

**To query the monitoring data of COS, use the following input parameters:**
&Namespace=QCE/COS
&Instances.N.Dimensions.0.Name=appid
&Instances.N.Dimensions.0.Value=Root account APPID
&Instances.N.Dimensions.1.Name=bucket
&Instances.N.Dimensions.1.Value=Bucket name 
