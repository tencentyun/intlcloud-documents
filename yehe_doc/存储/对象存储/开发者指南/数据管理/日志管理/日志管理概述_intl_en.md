## Overview
The logging feature allows you to record the access information of a source bucket and save it to a destination bucket as logs.

In the destination bucket, the log path is:

```shell
destination bucket/path prefix{YYYY}/{MM}/{DD}/{time}_{random}_{index}
```

Logs are generated every 5 minutes (one record per line). Each record contains multiple fields, and fields are separated by a space. The file size for a log file is up to 256 MB. If the log file reaches the file size limit in 5 minutes, a new log file will be created. The logging fields supported are as follows:

| No. | Field | Description | Example |
| :--------: | :---------------: | :-----------------------: | ----------------------------------------------------------------------------- |
| 1 | eventVersion | Log version | 1.0 |
| 2 | bucketName | Bucket name | examplebucket-1250000000 |
| 3 | qcsRegion | Request region | ap-beijing |
| 4 | eventTime | Event time (request end time, which is a timestamp in UTC+0 time zone) | 2018-12-01T11:02:33Z |
| 5        | eventSource     | Access domain name | examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com                        |
| 6 | eventName | Event name | UploadPart |
| 7 | remoteIp | Source IP | 192.168.0.1 |
| 8        | userSecretKeyId | User access `KeyId`        | AKIDNYVCdoJQyGJ5b1234                                                       |
| 9        | reservedFiled | Reserved field  | Displayed as `-` |
| 10 | reqBytesSent | Request bytes | 83886080 |
| 11 | deltaDataSize | Change in storage made by the request (in bytes) | 808 |
| 12 | reqPath | Requested file path | /folder/text.txt |
| 13 | reqMethod | Request method | put |
| 14 | userAgent | User UA | cos-go-sdk-v5.2.9 |
| 15 | resHttpCode | HTTP response status code | 404  |
| 16       | resErrorCode    | Error code       | NoSuchKey                               |
| 17       | resErrorMsg     | Error message       | The specified key does not exist.                                      |
| 18 | resBytesSent | Bytes returned | 197 |
| 19 | resTotalTime | Total time used by the request (in milliseconds, i.e., the time between the last byte of the response and the first byte of the request) | 4295 |
| 20       | logSourceType   | Source type of the log    | `USER` (user access requests), `CDN` (CDN origin-pull requests)  |
| 21 | storageClass | Storage class | STANDARD, STANDARD_IA, ARCHIVE |
| 22       | accountId          | Bucket owner ID                                               | 100000000001                                                 |
| 23 | resTurnAroundTime | Time used by the request server (in milliseconds, i.e., the time between the first byte of the response and the last byte of the request) | 4295 |
| 24       | requester    | Requester account. <br>If the requester is a root account, this parameter is in the format of `root account UIN:root account UIN`.<br>If the requester is a sub-account, this parameter is in the format of `root account UIN:sub-account UIN`.<br>If the requester is a [service account](https://intl.cloud.tencent.com/document/product/598/19421), this parameter is in the format of `authorized root account UIN:role ID`.<br>If the requester is anonymous, this parameter is displayed as `-`.             |    100000000001:100000000001          |
| 25       | requestId    | Request ID             | NWQ1ZjY4MTBfMjZiMjU4NjRfOWI1N180NDBiYTY=      |
| 26       | objectSize    | Object size, in bytes      | 808. If you use multipart upload, `objectSize` will only be displayed when the upload is complete, and will be `-` during the multipart upload process |
| 27 | versionId | Object version ID | Random string |
| 28  | targetStorageClass | Destination storage class, recorded for replication requests | STANDARD, STANDARD_IA, ARCHIVE |
| 29       | referer            | HTTP referer of the request                                          | `*.example.com` or 111.111.111.1                             |
| 30       | requestUri    | Request URI             | "GET /fdgfdgsf%20/%E6%B5%AE%E7%82%B9%E6%95%B0 HTTP/1.1"       |
| 31       | vpcId    | VPC request ID            | "0" (non-VPC)/"12345" (VPC, a non-"0" string)       |

>!
> - Currently, COS offers the logging feature only in the Beijing, Shanghai, Guangzhou, Nanjing, Chongqing, Chengdu, Hong Kong (China), Singapore, Seoul, Toronto, Silicon Valley, and Mumbai regions.
> - The destination bucket and source bucket must reside in the same region.
> - The destination bucket that stores logs can be the source bucket itself (not recommended).
> - Currently, logs will be generated only when the bucket is accessed through XML APIs and XML API-based SDKs or tools, not via JSON APIs or JSON API-based SDKs or tools.
> - Depending on customer needs and business development, COS may add new fields to the access logs. Be sure to prepare for this when parsing the logs.
> 

## Enabling Logging
### Using the Console
You can quickly enable logging in the console. For detailed directions, see [Setting Logging](https://intl.cloud.tencent.com/document/product/436/17040).

### Using APIs 
To enable logging for a bucket using APIs, follow the steps below:
1. Create a log role.
2. Grant the log role permissions.
3. Enable logging.

#### 1. Create a log role
Create a log role. For more information, see [CreateRole](https://intl.cloud.tencent.com/document/product/598/33561).
Here, `roleName` must be `CLS_QcsRole`.
`policyDocument` must be:
```
{
	"version": "2.0",
	"statement": [{
		"action": "name/sts:AssumeRole",
		"effect": "allow",
		"principal":{
			"service": "cls.cloud.tencent.com"
		}
	}]
}
```
#### 2. Grant the log role permissions
Grant the log role permissions. For more information about the API, see [AttachRolePolicy](https://intl.cloud.tencent.com/document/product/598/33562).
Here, `policyName` is set to `QcloudCOSAccessForCLSRole`, `roleName` is the `CLS_QcsRole` in step 1, or the `roleID` returned when `roleName` was created.

#### 3. Enable logging
Call the API to enable logging. For more information about the API, see [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054). Note that the destination bucket to store the logs should be in the same region as the source bucket.
