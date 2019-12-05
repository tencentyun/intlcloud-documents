## Overview
The log management records the detailed access information of the specified source bucket and store the information as log files in the specified bucket to facilitate bucket management.

In the destination bucket, the log path is:

```shell
{Destination bucket}/{Path prefix} {YYYY}/{MM}/{DD}/{time}_{random}_{index}.gz
```

The log is generated every 5 minutes, one record is a row, each record contains multiple fields, and the fields are separated by spaces. It should be noted that a single log file can be up to 256MB. If you generate more than 256MB of logs in these 5 minutes, your log will be split into multiple log files. The currently supported log fields are as follows:

| Field Number | Name | Meaning | Example |
| :--------: | :---------------: | :-----------------------: | ----------------------------------------------------------------------------- |
| 1 | eventVersion | Log version | 1.0 |
| 2 | bucketName | Bucket name | examplebucket-1250000000 |
| 3 | qcsRegion | Request region | ap-beijing |
| 4 | eventTime | Event time (request end time, which is a timestamp in UTC+0 time zone) | 2018-12-01T11:02:33Z |
| 5 | eventSource | Domain name is accessed by the user | examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com |
| 6 | eventName | Event name | UploadPart |
| 7 | remoteIp | Source IP | 192.168.0.1 |
| 8 | userSecretKeyId | User access KeyId | AKIDNYVCdoJQyGJ5brTf |
| 9        | reservedFiled | reserved fields   | reserved fields, shown as `-`。 |
| 10 | reqBytesSent | Request bytes | 83886080 |
| 11 | deltaDataSize | Change in storage made by the request (in bytes) | 808 |
| 12 | reqPath | Requested file path | /folder/text.txt |
| 13 | reqMethod | Request method | put |
| 14 | userAgent | User UA | cos-go-sdk-v5.2.9 |
| 15 | resHttpCode | HTTP return code | 404 |
| 16 | resErrorCode | Error code | NoSuchKey |
| 17 | resErrorMsg | Error message | The specified key does not exist. |
| 18 | resBytesSent | Bytes returned | 197 |
| 19 | resTotalTime | Total time used by the request (in milliseconds, i.e., the time between the last byte of the response and the first byte of the request) | 4295 |
| 20 | logSourceType | Log source type | USER（User access request），CDN（CDN Origin-pull request） |
| 21 | storageClass | Storage class | STANDARD, STANDARD_IA, ARCHIVE |
| 22 | accountId | Bucket owner ID | 100000000001 |
| 23 | resTurnAroundTime | Time used by the request server (in milliseconds, i.e., the time between the first byte of the response and the last byte of the request) | 4295 |
| 24 | requester | Visitor | Primary account id: sub-account id, if it is anonymous access, shown as `-`.  |
| 25 | requestId | Request ID | NWQ1ZjY4MTBfMjZiMjU4NjRfOWI1N180NDBiYTY=  |
| 26 | objectSize | Object size in bytes | 808, if you use Multipart Upload, the objectSize field will only be displayed when the upload is completed. This field displays `-` during each Multipart Upload. |
| 27 | versionId | Object version ID | Random string |
| 29 | targetStorageClass | Destination storage class, recorded for replication requests | STANDARD, STANDARD_IA, ARCHIVE |
| 30 | referer | Origin server address | `*.example.com` or 111.111.111.1 |
| 31       | requestUri    | Request URI             | "GET /fdgfdgsf%20/%E6%B5%AE%E7%82%B9%E6%95%B0 HTTP/1.1"       |

> - The log management feature is currently only available in four regions including Beijing, Shanghai, Guangzhou, Chengdu and Toronto. 
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
Call the API to enable the log management feature. For specific API information, see [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054), where the destination bucket storing the logs is required to be in the same region as the source bucket.

