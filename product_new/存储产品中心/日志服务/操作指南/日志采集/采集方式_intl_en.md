## Collection methods

CLS provides multiple collection methods:

| Collection method          | Description                  |
| :------------- | -------------------------------- |
| Collect logs via API           | You can upload structured logs to CLS by calling [CLS API](https://intl.cloud.tencent.com/document/product/614/12445). For more information, see [Uploading Structured Logs](https://intl.cloud.tencent.com/document/product/614/16873).|
| Collect logs via SDK           | Collecting via SDK is not supported at this time.                                                |
| Collect logs via LogListener client | LogListener is a log collection client provided by CLS. You can quickly access CLS by simply configuring LogListener on the console. For more information, see [LogListener Use Process](https://intl.cloud.tencent.com/document/product/614/31578). |

A comparison of the collection methods is as follows:

| Category name  | Collection by LogListener                   | Collection via API                   |
| -------- | ---------------------------------- | ------------------------------ |
| Code modification | Provides a non-intrusive collection method for applications, without code modification. | Reports logs only after modifying application code. |
| Resumable upload | Supports resumable upload of logs.                   | Automatically implemented by code.                   |
| Retransmission upon failure | Provides an inherent retry mechanism.                       | Automatically implemented by code.                   |
| Local cache | Supports local cache, ensuring data integrity during peak hours. | Automatically implemented by code.                   |
| Resource occupation | Occupies resources such as memory and CPU.                | Occupies no additional resources.                 |

## Accessing log sources

You can access different log sources in different ways. For more information, see the following tables:

**Log source category**

| Log source category   | Recommended access method |
| ------------ | ------------ |
| Direct program output | API          |
| Local log file | LogListener  |

**Log source environment**

| System environment    | Recommended access method                      |
| ----------- | --------------------------------- |
| Linux/Unix  | LogListener                       |
| Windows     | API (Currently, LogListener does not support Windows.) |
| iOS/Android | API (Currently, no iOS/Android SDK is available.)       |

**Cloud product logs**

| Cloud product name      | Recommended access method   |
| --------------- | ---------- |
| Cloud Virtual Machine (CVM) | Install and configure LogListener |
| API Gateway | Console (For more information, see the [access guide](https://cloud.tencent.com/document/product/614/38126).) |
| Live Video Broadcasting (LVB) | Console (For more information, see the [access guide](https://cloud.tencent.com/document/product/614/37703).) |
| Serverless Cloud Function (SCF) | Console (For more information, see the [access instructions](https://cloud.tencent.com/document/product/614/37702).) |
| Tencent Kubernetes Engines (TKE) | Console (For more information, see the [access guide](https://cloud.tencent.com/document/product/614/37701).) |
| Flow Logs (FLs) | Console |


