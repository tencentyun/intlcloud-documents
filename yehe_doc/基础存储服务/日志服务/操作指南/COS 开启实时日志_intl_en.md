## Overview

You can log in to the Cloud Object Storage (COS) console to enable the real-time log feature of CLS for buckets. CLS provides powerful features for request logs related to **bucket object operations**, including per-minute log reporting, real-time log search, visualization, and alarms. The real-time log feature can help you better analyze the access statistics of the current bucket and quickly locate problems when access exceptions occur.


## Prerequisites
Currently, you need to enable an allowlist when enabling the COS real-time log feature. <a href="https://intl.cloud.tencent.com/contact-sales">Contact us</a> to apply for the real-time log feature.
Before enabling the real-time log feature for a COS bucket, you need to <a href="https://intl.cloud.tencent.com/product/cls">activate CLS</a> first.






## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the bucket for which you want to enable the real-time log feature.
4. On the left sidebar, choose **Log Management** > **Log Search**.
5. When the message indicating that the real-time log feature is not enabled for the current bucket is displayed, click **Activate Now** to enable the real-time log feature.

6. After the real-time log feature is enabled, access logs of the bucket will be shipped to the log topic named **cos-log-store** in the same region in CLS.
7. Choose **Log Management** > **Log Search**. On the page displayed, enter the search and analysis syntax, select a time range, and click **Search and Analysis**. Then you can obtain the access logs that the bucket reports to CLS. For more information on the search and analysis statements of CLS, please see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439).

8. Analyze the bucket access logs obtained. For more information on the analysis method, please see [COS Access Log Analysis](https://intl.cloud.tencent.com/document/product/614/42749).
9. If you want to configure visualization and alarming for bucket access logs, go to the [CLS console](https://console.cloud.tencent.com/cls).

## Log Format and Variable Description

Bucket access logs record information such as the source bucket, user ID, and request method.

| No. | Field              | Description                                                        | Example                                                         |
| :------- | :----------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 1        | eventVersion       | Log version                                                     | 1.0                                                          |
| 2        | bucketName         | Bucket name                                                   | examplebucket-1250000000                                     |
| 3        | qcsRegion          | Request region                                                     | ap-beijing                                                   |
| 4 | eventTime | Event time (request end time, which is a timestamp in UTC+0 time zone) | 2018-12-01T11:02:33Z |
| 5        | eventSource     | Access domain name | examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com                        |
| 6        | eventName          | Event name                                                     | UploadPart                                                   |
| 7        | remoteIp           | Source IP                                                      | 192.168.0.1                                                  |
| 8        | userSecretKeyId    | User access KeyId                                               | AKIDNYVCdoJQyGJ5brTf                                         |
| 9        | reservedField      | Reserved field                                                     | Displayed as `-`                                        |
| 10       | reqBytesSent       | Request bytes                                          | 83886080                                                     |
| 11       | deltaDataSize      | Change in storage made by the request (in bytes)                                  | 808                                                          |
| 12       | reqPath            | Requested file path                                               | /folder/text.txt                                             |
| 13       | reqMethod          | Request method                                                     | put                                                          |
| 14       | userAgent          | User agent (UA)                                                      | cos-go-sdk-v5.2.9                                            |
| 15       | resHttpCode        | HTTP return code                                                  | 404                                                          |
| 16       | resErrorCode       | Error code                                                       | NoSuchKey                                                    |
| 17       | resErrorMsg        | Error message                                                     | The specified key does not exist.                            |
| 18       | resBytesSent       | Bytes returned                                          | 197                                                          |
| 19 | resTotalTime | Total time used by the request (in milliseconds, i.e., the time between the last byte of the response and the first byte of the request) | 4295 |
| 20       | logSourceType      | Source type of the log                                                   | `USER` (user access requests), `CDN` (CDN origin-pull requests)                    |
| 21       | storageClass       | Storage class                                                     | STANDARD, STANDARD_IA, ARCHIVE                               |
| 22       | accountId          | Bucket owner ID                                               | 100000000001                                                 |
| 23       | resTurnAroundTime  | Time used by the request server (in milliseconds, i.e., the time between the first byte of the response and the last byte of the request) | 4295                                                         |
| 24       | requester          | Requester                                                       | Root account ID, sub-account ID, or `-` (anonymous access)              |
| 25       | requestId          | Request ID                                                      | NWQ1ZjY4MTBfMjZiMjU4NjRfOWI1N180NXXXX=                     |
| 26       | objectSize    | Object size, in bytes      | 808. If you use multipart upload, `objectSize` will only be displayed when the upload is complete, and will be `-` during the multipart upload process |
| 27       | versionId          | Object version ID                                                  | Random string                                                   |
| 28  | targetStorageClass | Destination storage class, recorded for replication requests | STANDARD, STANDARD_IA, ARCHIVE |
| 29       | referer            | HTTP referer of the request                                          | `*.example.com` or 111.111.111.1                             |
| 30       | requestUri         | Request URI                                                     | "GET /fdgfdgsf%20/%E6%B5%AE%E7%82%B9%E6%95%B0 HTTP/1.1"      |
