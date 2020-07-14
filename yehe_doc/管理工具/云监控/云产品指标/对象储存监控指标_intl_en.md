
## Namespace

Namespace=QCE/BLOCK_STORAGE

## Monitoring Metrics

### Request metrics

| Parameter | Metric Name | Description | Unit | Dimension |
| ----------------------| ---------------------- | -------------- | ---- | ----------------------|
| StdReadRequests | STANDARD read requests | Number of STANDARD read requests, which is calculated based on the number of sent requests | Times | appid and bucket |
| StdWriteRequests | STANDARD write requests | Number of STANDARD write requests, which is calculated based on the number of sent requests | Times | appid and bucket |
| IaReadRequests | STANDARD_IA read requests | Number of STANDARD_IA read requests, which is calculated based on the number of sent requests | Times | appid and bucket |
| IaWriteRequests | STANDARD_IA write requests | Number of STANDARD_IA write requests, which is calculated based on the number of sent requests | Times | appid and bucket |
| NlReadRequests | Nearline storage read requests | Number of nearline storage read requests, which is calculated based on the number of sent requests | Times | appid and bucket |
| NlWriteRequests | Nearline storage write requests | Number of nearline storage write requests, which is calculated based on the number of sent requests | Times | appid and bucket |

### Storage metrics

| Metric Name | Description | Unit | Dimension |
| ---------------------- | ----------------- | ---- | ---------------------- |
| StdStorage | STANDARD - storage space | MB | appid and bucket |
| SiaStorage | STANDARD_IA - storage space | MB | appid and bucket |
| NelStorage | Nearline storage - storage space | MB | appid and bucket |
| ArcStorage | ARCHIVE - storage space | MB | appid and bucket |
| MazStdStorage | MAZ_STANDARD - storage space | MB | appid and bucket |
| StdObjectNumber | STANDARD - number of objects | Count | appid and bucket |
| MazStdObjectNumber | MAZ_STANDARD - number of objects | Count | appid and bucket |
| IaObjectNumber | STANDARD_IA - number of objects | Count | appid and bucket |
| NlObjectNumber | Nearline storage - number of objects | Count | appid and bucket |


### Traffic metrics

| Parameter | Metric Name | Description | Unit | Dimension |
| ----------------------| ---------------------- | ------------- | ---- | ----------------------|
| InternetTraffic | Public downstream traffic | Traffic of mutual data transmission between the client and COS on the public network | B | appid and bucket |
| InternalTraffic | Private downstream traffic | Traffic of mutual data transmission between the client and COS on the Tencent Cloud private network | B | appid and bucket |
| CdnOriginTraffic | CDN origin-pull traffic | Traffic generated after data is transmitted from COS to the edge servers of the Tencent Cloud CDN | B | appid and bucket |
| InboundTraffic | Total upload traffic of public and private networks | Traffic generated after data is uploaded to COS on the public and private networks | B | appid and bucket |

### Return code metrics

| Parameter | Metric Name | Description | Unit | Dimension |
| ---------------------- | ----------- | --------|---- | ---------------------- |
| 2xxResponse | 2xx status code | Number of 2xx errors in the current bucket | Times | appid and bucket |
| 3xxResponse | 3xx status code | Number of 3xx errors in the current bucket | Times | appid and bucket |
| 4xxResponse | 4xx status code | Number of 4xx errors in the current bucket | Times | appid and bucket |
| 5xxResponse | 5xx status code | Number of 5xx errors in the current bucket | Times | appid and bucket |
>
> 1. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
> 2. The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

### Data retrieval metrics

| Parameter | Metric Name | Description | Unit | Dimension |
| ----------------------| ---------------------- | ------------ | ---- | ----------------------|
| StdRetrieval | Standard data retrieval | Traffic generated due to the retrieval of standard data | B | appid and bucket |
| IaRetrieval | Low-frequency data retrieval | Traffic generated due to the retrieval of low-frequency data | B | appid and bucket |
| NlRetrieval | Nearline data retrieval | Traffic generated due to the retrieval of nearline data | B | appid and bucket |

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------- | -------- | ---------------------- | --------------------------------------------------- |
| &Instances.N.Dimensions.0.Name | appid | Dimension name of the root account APPID | Enter a string-type dimension name, such as appid |
| &Instances.N.Dimensions.0.Value | appid | A specific APPID of the root account | Enter a specific root account APPID, such as 1250000000 |
| &Instances.N.Dimensions.1.Name | bucket | Dimension name of the bucket | Enter a string-type dimension name, such as bucket |
| &Instances.N.Dimensions.1.Value | bucket | A specific bucket name | Enter a specific bucket name, such as examplebucket-1250000000 |

## Input Parameters
To query the monitoring data of a COS bucket, use the following input parameters:
&Namespace=QCE/COS
&Instances.N.Dimensions.0.Name=appid
&Instances.N.Dimensions.0.Value=<APPID of the root account>
&Instances.N.Dimensions.1.Name=bucket
&Instances.N.Dimensions.1.Value=<Bucket name> 
