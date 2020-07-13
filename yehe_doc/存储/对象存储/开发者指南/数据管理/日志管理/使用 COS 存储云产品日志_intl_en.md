## Overview

The use of Tencent Cloud products generates a massive number of logs, which can help you analyze and make decisions for your business. You can store these logs persistently in COS, and then easily access them for analysis from COS using APIs, SDKs or tools.

This solution offers benefits as follows:

- **Persistent storage**: COS provides stable, persistent storage that allows you to put your logs in COS at a very low cost. You can access your logs over any period anytime anywhere for business analysis or decision-making.
- **COS Select**: this feature allows simple extraction of logs stored on COS. You can extract logs based on log fields to reduce data download traffic.
- **Data analysis**: you can analyze one or more COS logs for decision-making using Sparkling.

## Shipping Logs

You can ship your Tencent Cloud product logs to COS in one of the following 2 ways:

- Directly use the log shipping feature of Tencent Cloud product such as COS, CLB and CA.
- Use CLS to ship logs from there to COS.

The table below shows how Tencent Cloud products support log shipping:

| Product          | Shipping to COS | Shipping to CLS     |
| ------------------- | ---------------------- | ---------------------- |
| CA           | Yes                     | No                     |
| CLB        | Yes                     | Yes                     |
| CKafka     | Yes                     | No                     |
| APIGateway | No                     | Yes                     |
| SCF      | No                     | Yes                     |
| TKE        | No                     | Yes                     |
| LVB          | No                     | Yes                     |
| TCB          | No                     | Yes (do not support shipping to COS through CLS) |
| COS        | Yes                     | No          |

### Shipping logs to COS

Tencent Cloud products below allow you to ship logs directly to COS by setting log shipping rules as instructed in the product-specific documents.

| Product &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      | Document                                                 | Shipping Interval&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;        | Shipping Path                                                |
| --------------- | ------------------------------------------------------------ | -------------------- | ------------------------------------------------------------ |
|CA |[View](https://intl.cloud.tencent.com/document/product/1021/30338) | 10-15 min |  cloudaudit/customprefix/timestamp|
| CLB    | [View](https://intl.cloud.tencent.com/document/product/214/10329) | 60 min               | lb-id/timestamp                                              |
| CKafka | [View](https://intl.cloud.tencent.com/document/product/597/32552) | 5-60 min<br>Can be user-defined | instance id/topic id/timestamp                           |
| COS    | [View](https://intl.cloud.tencent.com/document/product/436/17040) | 5 min                | The path prefix can be user-defined. It’s recommended to specify an identifiable path, e.g. `cos_bucketname_access_log/timestamp`. |

>?CKafka supports shipping message data it generates. However, to get logs on certain actions such as creation of CKafka instances, you need to ship CloudAudit logs.

### Using CLS to ship logs to COS

Tencent Cloud products below allow you to ship logs directly to CLS for search and analysis. With CLS, you can further ship the logs to COS for persistent storage at lower costs and offline analysis.

| Product           | Document                                                 |
| -------------------- | ------------------------------------------------------------ |
| API Gateway | [View](https://intl.cloud.tencent.com/document/product/628/34636) |
| TKE         | [View](https://intl.cloud.tencent.com/document/product/457/32419) |
| LVB           | - |

CLS ships the following 3 types of logs to COS:

- CSV-formatted logs: logs in the format of comma-separated values. For more information, see [Shipping CSV-Formatted Logs](https://intl.cloud.tencent.com/document/product/614/31582).
- JSON-formatted logs: logs in the JSON format. For more information, see [Shipping JSON-Formatted Logs](https://intl.cloud.tencent.com/document/product/614/31583).
- Original logs: logs in original format, including full text in a single line, full text in multi-lines, and CSV (for certain products). For more information, see [Shipping Original Logs](https://intl.cloud.tencent.com/document/product/614/31584).

To ship logs from CLS to COS, you need to do the following:

1. Choose a Tencent Cloud product as needed, and configure a logset and log topic as instructed in the preceding log shipping document to connect your business data to CLS.
2. Select a log type as needed to ship to COS. We recommend that you use the product name as path prefix to differentiate product logs, for example, TKE logs named `TKE_tkeid_log/timestamp`.
3. Once the shipping rule is configured, you can additionally configure COS event notifications for file uploads by calling the SCF service. You can further operate on logs shipped to COS based on these event notifications. For more information, see [Event Notifications](https://intl.cloud.tencent.com/document/product/436/31648).

## Log Analysis

### Downloading logs locally for offline analysis

You can download logs locally by using the Tencent Cloud console, SDKs, APIs or tools. To do so, follow the instructions in one of the following documents and replace every file path in your code with your log storage path:

| Download Method       | Document                                                     |
| -------------- | ------------------------------------------------------------ |
| Console         | [View](https://intl.cloud.tencent.com/document/product/436/13322) |
| cosbrowser     | [View](https://intl.cloud.tencent.com/document/product/436/32565) |
| coscmd         | [View](https://intl.cloud.tencent.com/document/product/436/10976) |
| Android SDK    | [View](https://intl.cloud.tencent.com/document/product/436/31514) |
| C SDK          | [View](https://intl.cloud.tencent.com/document/product/436/31518) |
| C++ SDK        | [View](https://intl.cloud.tencent.com/document/product/436/31522) |
| .NET SDK       | [View](https://intl.cloud.tencent.com/document/product/436/30596) |
| Go SDK         | [View](https://intl.cloud.tencent.com/document/product/436/31526) |
| iOS SDK        | [View](https://intl.cloud.tencent.com/document/product/436/11280) |
| Java SDK       | [View](https://intl.cloud.tencent.com/document/product/436/31534) |
| JavaScript SDK | [View](https://intl.cloud.tencent.com/document/product/436/31538) |
| Node.js SDK    | [View](https://intl.cloud.tencent.com/document/product/436/31710) |
| PHP SDK        | [View](https://intl.cloud.tencent.com/document/product/436/31542) |
| Python SDK     | [View](https://intl.cloud.tencent.com/document/product/436/31546) |
| Wechat Mini Program SDK     | [View](https://intl.cloud.tencent.com/document/product/436/32457) |
| API            | [View](https://intl.cloud.tencent.com/document/product/436/7753) |

### Analyzing logs using COS Select

You can optionally extract and analyze COS logs stored in CSV or JSON format directly by using the COS Select feature. It enables you to query desired log fields, which largely reduces the number of logs transferred by COS for lower usage costs and faster data access. For more information about COS Select, see [Select Overview](https://intl.cloud.tencent.com/document/product/436/32472).

Currently, you can access COS Select by using the console or APIs.

| Method | Instructions                                                     |
| -------- | ------------------------------------------------------------ |
| Console     | [View](https://intl.cloud.tencent.com/document/product/436/32538) |
| API      | [View](https://intl.cloud.tencent.com/document/product/436/32360) |


