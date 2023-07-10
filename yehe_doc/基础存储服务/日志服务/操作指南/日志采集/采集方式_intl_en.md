## Collection Methods

CLS provides multiple methods for data collection:

| Collection Method               | Description                                                         |
| :--------------------- | ------------------------------------------------------------ |
| API           | You can upload structured logs to CLS by calling [CLS APIs](https://intl.cloud.tencent.com/document/product/614/12445). For more information, please see [Uploading Structured Logs](https://intl.cloud.tencent.com/document/product/614/16873). |
| SDK           | You can use SDKs to upload structured logs to CLS. For more information, please see the SDK collection documentation.                                              |
| LogListener client | LogListener is a log collection client provided by CLS. You can quickly access CLS by simply configuring LogListener on the console. For more information, please see [LogListener Use Process](https://intl.cloud.tencent.com/document/product/614/31578). |

A comparison of the collection methods is as follows:

| Category  | Collection via LogListener                   | Collection via API                   |
| -------- | ---------------------------------- | ------------------------------ |
| Code modification | Provides a non-intrusive collection method for applications, without code modification. | Reports logs only after modifying application code. |
| Resumable upload | Supports resumable upload of logs.                   | Automatically implemented by code.                   |
| Retransmission upon failure | Provides an inherent retry mechanism.                       | Automatically implemented by code.                   |
| Local cache | Supports local cache, ensuring data integrity during peak hours. | Automatically implemented by code.                   |
| Resource occupation | Occupies resources such as memory and CPU resources.                | Occupies no additional resources.                 |

## Accessing Log Sources

You can access different log sources in different ways. For more information, see the following tables:

**Log source category**

| Log Source Category   | Recommended Access Method |
| ------------ | ------------ |
| Direct program output | API          |
| Local log file | LogListener  |

**Log source environment**

| System Environment    | Recommended Access Method                      |
| ----------- | ----------------------------------- |
| Linux/Unix  | LogListener                       |
| Windows     | API (Currently, LogListener does not support Windows.) |
| iOS/Android | SDK         |

**Tencent Cloud service logs**

| Tencent Cloud Service               | Recommended Access Method                                                 |
| ------------------------ | ------------------------------------------------------------ |
| CVM | Install and configure LogListener. For more information, see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414). |
| TKE | Configure log collection in the TKE console. For more information, see [here](https://intl.cloud.tencent.com/document/product/457/32419). |
| CDN | Configure log collection in the CDN console. For more information, see [here](https://intl.cloud.tencent.com/document/product/228/35380). |
| CLB | Configure log collection in the CLB console. For more information, see [here](https://intl.cloud.tencent.com/document/product/214/35063). |
| SCF | Configure log collection in the SCF console For more information, see [here](https://intl.cloud.tencent.com/document/product/583/34876). |
| LVB | Configure log collection in the LVB console For more information, see [here](https://cloud.tencent.com/document/product/267/33996). |
| Flow Logs | Configure log collection in the Flow Logs console. For more information, see [here](https://intl.cloud.tencent.com/document/product/682/18966). |
| TI Platform | Configure log collection in the TI Platform console. For more information, see [here](link). |
| MGOBE | Configure log collection in the MGOBE console. For more information, see [here](link). |

