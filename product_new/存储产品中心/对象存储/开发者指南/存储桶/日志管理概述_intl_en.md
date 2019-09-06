## Overview
The log management records the detailed access information of the specified source bucket and store the information as log files in the specified bucket to facilitate bucket management.

In the destination bucket, the log path is:

```shell
destination bucket/path prefix{YYYY}/{MM}/{DD}/{time}_{random}_{index}.gz
```

Logs are generated once every 5 minutes, one record per line. Each record contains multiple fields separated by `\t`. The current log fields include:

| Field Number | Name | Meaning | Example |
| :--------: | :---------------: | :-----------------------: | ----------------------------------------------------------------------------- |
| 1 | eventVersion | Log version | 1.00 |
| 2 | bucketName | Bucket name | examplebucket-1250000000 |
| 3 | qcsRegion | Request region | ap-beijing |
| 4 | eventTime | Event time (request end time, which is a timestamp in UTC+0 time zone) | 2018-12-01T11:02:33Z |
| 5 | eventSource | Domain name corresponding to the bucket | examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com |
| 6 | eventName | Event name | UploadPart |
| 7 | remoteIp | Source IP | 192.168.0.1 |
| 8 | userSecretKeyId | User access KeyId | AKIDNYVCdoJQyGJ5brTf |
| 9 | reqQcsSource | QCS source information of the request | qcs::cos:ap-beijing:uin/100000000001:examplebucket-1250000000/folder/text.txt |
| 10 | reqBytesSent | Request bytes | 83886080 |
| 11 | deltaDataSize | Change in storage made by the request (in bytes) | 12345678 |
| 12 | reqPath | Requested file path | /folder/text.txt |
| 13 | reqMethod | Request method | put |
| 14 | userAgent | User UA | cos-go-sdk-v5.2.9 |
| 15 | resHttpCode | HTTP return code | 200 OK |
| 16 | resErrorCode | Error code | No content. This field is currently not supported, which is recorded as '-' |
| 17 | resErrorMsg | Error message | SUCCESS |
| 18 | resBytesSent | Bytes returned | 197 |
| 19 | resTotalTime | Total time used by the request (in milliseconds, i.e., the time between the last byte of the response and the first byte of the request) | 4295 |
| 20 | logSourceType | Log source type | COS |
| 21 | storageClass | Storage class | STANDARD, STANDARD_IA, ARCHIVE |
| 22 | accountid | Bucket owner ID | 100000000001 |
| 23 | resTurnAroundTime | Time used by the request server (in milliseconds, i.e., the time between the first byte of the response and the last byte of the request) | 4295 |
| 24 | Requester | Requester | Requester account nickname |
| 25 | requestID | Request ID | Unique ID of this request |
| 26 | objectSize | Object size in bytes | Account |
| 27 | versionid | Object version ID | Random string |
| 29 | targetStorageClass | Destination storage class, recorded for replication requests | STANDARD, STANDARD_IA, ARCHIVE |
| 30 | syncRequest | Whether this is a Tencent Cloud CDN origin-pull request | True |
| 31 | referer | Origin server address | \*.example.com or 111.111.111.1 |

>- The log management feature is currently only available in four regions including Beijing, Shanghai, Guangzhou, and Chengdu.
> - The log management feature requires the source bucket and destination bucket to be in the same region.
> - The destination bucket for storing the logs can be the source bucket itself, but this is not recommended.
> - Currently, logs will be generated only when the bucket is accessed through XML APIs and XML API-based SDKs or tools, not via JSON APIs or JSON API-based SDKs or tools.
> - Depending on customer needs and business development, COS may add new fields to the access logs. Please be sure to prepare for this when parsing the logs.

## Enabling Log Management
### Using the Console
You can quickly enable the log management feature in the console. For instructions, see the Console Guide - [Setting Log Management](https://intl.cloud.tencent.com/document/product/436/17040).

### Using the API 
To enable the log management feature for the specified bucket using API, follow the steps below:
1. Create a log role.
2. Grant the log role permissions.
3. Enable log management.

#### 1. Create a log role
Create a log role. For more information, see [CreateRole](https://intl.cloud.tencent.com/document/product/598/13886).
Here, roleName must be CLS_QcsRole.
policyDocument must be:

```
{
	"version": "2.0",
	"statement": [{
		"action": "name/sts:AssumeRole",
		"effect": "allow",
		"principal": {
			"service": "cls.cloud.tencent.com"
		}
	}]
}
```
#### 2. Grant the log role permissions
Grant the log role permissions. For specific API information, see [AttachRolePolicy](https://intl.cloud.tencent.com/document/product/598/13889).
Here, the policyName is QcloudCOSAccessForCLSRole; the roleName is CLS_QcsRole as in step 1, or, the roleID returned upon the creation of roleName, for this regard.   

#### 3. Enable log management
Call the API to enable the log management feature. For specific API information, see [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/31483), where the destination bucket storing the logs is required to be in the same region as the source bucket.

