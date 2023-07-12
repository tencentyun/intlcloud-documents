## Overview

The process of using Tencent Cloud products generates a massive number of logs, which can be used to help you analyze and make decisions for your business. For your convenience, you can store these logs persistently in COS, and then easily access them for analysis by using various APIs, SDKs or tools.

COS log storage offers the following benefits:

- **Persistent storage**: COS provides stable, persistent storage that allows you to store logs in COS at a very low cost. You can access your logs anytime, anywhere for business analysis or decision-making.
- **COS Select**: This feature allows for the simple extraction of logs stored on COS. You can combine log fields to make it easier to extract the information you need and reduce data download traffic.
- **Data analysis**: You can analyze one or more COS logs using Sparkling, which then can be used to facilitate and provide a basis for important business decisions.

## Shipping Logs

You can ship your Tencent Cloud product logs to COS in one of the following two ways:

- Use the Tencent Cloud log shipping feature in which logs are directly shipped to COS. Products such as COS and CloudAudit (CA) support directly shipping logs to COS.
- Use the CLS log shipping feature in which logs are first shipped to CLS and then transferred to COS for persistent storage.

The table below shows the particular log shipping method or methods currently supported by various Tencent Cloud products:

| Product          | Supports Direct Shipping to COS | Supports Shipping to CLS     |
| ------------------- | ---------------------- | ---------------------- |
| CA           | Yes                     | No                     |
| CLB        | No                     | Yes                     |
| CKafka     | Yes                     | No                     |
| API Gateway | No                     | Yes                     |
| SCF      | No                     | Yes                     |
| TKE        | No                     | Yes                     |
| CSS          | No                     | Yes                     |
| TCB          | No                     | Yes (however, TCB does not support shipping logs to COS through CLS) |
| COS        | Yes                     |  Yes for accounts on the allowlist. You can [contact us](https://intl.cloud.tencent.com/contact-sales) to add your account to the allowlist.        |

### Directly shipping logs to COS

The Tencent Cloud products outlined below allow you to ship logs directly to COS by setting log shipping rules as instructed in the product-specific documentation.

| Product      | Log Shipping Document                                                 | Log Shipping Interval        | Log Shipping Path                                                 |
| --------------- | ------------------------------------------------------------ | -------------------- | ------------------------------------------------------------ |
| CA | [Click here to view](https://intl.cloud.tencent.com/document/product/1021/30338) | 10-15 min |  cloudaudit/customprefix/timestamp|
| CKafka | [Click here to view](https://intl.cloud.tencent.com/document/product/597) | 5-60 min<br>You can specify the interval | instance id/topic id/timestamp                           |
| COS    | [Click here to view](https://intl.cloud.tencent.com/document/product/436/17040) | 5 min                | You can specify the path prefix. We recommend specifying an identifiable path, e.g. `cos_bucketname_access_log/timestamp`. |

>?CKafka supports shipping the message data that it generates. However, to get logs on certain actions such as the creation of CKafka instances, you need to ship the CA logs.

### Using CLS to ship logs to COS

The Tencent Cloud products outlined below allow you to ship logs directly to CLS for search and analysis. With CLS, you can further ship the logs to COS for persistent storage, thus reducing your costs and allowing for convenient offline analysis.

| Product           | Documentation                                                 |
| -------------------- | ------------------------------------------------------------ |
| API Gateway | [Click here to view](https://intl.cloud.tencent.com/document/product/628/34636) |
| TKE         | [Click here to view](https://intl.cloud.tencent.com/document/product/457/32419) |
| CSS           | Click here to view|

CLS can ship the following three types of logs to COS:

- CSV-formatted logs: Logs formatted with comma-separated values. For more information, see [Shipping CSV-Formatted Logs](https://intl.cloud.tencent.com/document/product/614/31582).
- JSON-formatted logs: Logs in JSON format. For more information, see [Shipping JSON-Formatted Logs](https://intl.cloud.tencent.com/document/product/614/31583).
- Original logs: Logs in their original format, including those with full text in a single line, full text in multi-lines, and comma-separated values (for certain products). For more information, see [Shipping Original Logs](https://intl.cloud.tencent.com/document/product/614/31584).

To ship logs from CLS to COS, you need to do the following:

1. Choose a Tencent Cloud product that meets your business needs and configure a logset and log topic as instructed in the log shipping documentation provided above to connect your business data to CLS.
2. With your particular business needs in mind, select the most suitable log type to ship to COS. We recommend that you use the product name as the path prefix to differentiate product logs, for example, you could use the following name for TKE logs: `TKE_tkeid_log/timestamp`.
3. Once the shipping rule is configured, you can configure COS event notifications for file uploads through SCF. You can perform further operations on logs shipped to COS based on these event notifications. For more information, see [Event Notifications](https://intl.cloud.tencent.com/document/product/436/31648).

## Log Analysis

### Downloading logs locally for offline analysis

You can download logs to the local file system through the Tencent Cloud console, or by using various SDKs, APIs, and tools. To do so, follow the instructions in one of the following documents and replace each file path in the code with your log storage path:

| Download Method       | Document                                                     |
| -------------- | ------------------------------------------------------------ |
| Console         | [Click here to view](https://intl.cloud.tencent.com/document/product/436/13322) |
| COSBrowser     | [Click here to view](https://intl.cloud.tencent.com/document/product/436/32565) |
| COSCMD         | [Click here to view](https://intl.cloud.tencent.com/document/product/436/10976) |
| Android SDK    | [Click here to view](https://intl.cloud.tencent.com/document/product/436/37675) |
| C SDK          | [Click here to view](https://intl.cloud.tencent.com/document/product/436/31518) |
| C++ SDK        | [Click here to view](https://intl.cloud.tencent.com/document/product/436/31522) |
| .NET SDK       | [Click here to view](https://intl.cloud.tencent.com/document/product/436/30594) |
| Go SDK         | [Click here to view](https://intl.cloud.tencent.com/document/product/436/31526) |
| iOS SDK        | [Click here to view](https://intl.cloud.tencent.com/document/product/436/37684) |
| Java SDK       | [Click here to view](https://intl.cloud.tencent.com/document/product/436/31534) |
| JavaScript SDK | [Click here to view](https://intl.cloud.tencent.com/document/product/436/31538) |
| Node.js SDK    | [Click here to view](https://intl.cloud.tencent.com/document/product/436/31710) |
| PHP SDK        | [Click here to view](https://intl.cloud.tencent.com/document/product/436/31542) |
| Python SDK     | [Click here to view](https://intl.cloud.tencent.com/document/product/436/31546) |
| WeChat Mini Program SDK     | [Click here to view](https://intl.cloud.tencent.com/document/product/436/32457) |
| API            | [Click here to view](https://intl.cloud.tencent.com/document/product/436/7753) |

### Analyzing logs using COS Select

You have the option to extract and analyze COS logs stored in CSV or JSON format directly by using the COS Select feature. It enables you to query desired log fields, which largely reduces the number of logs transferred by COS, thus lowering usage costs and improving data access speed. For more information on COS Select, see [Select Overview](https://intl.cloud.tencent.com/document/product/436/32472).

Currently, you can access COS Select using the console or APIs.

| Method | Instructions                                                     |
| -------- | ------------------------------------------------------------ |
| Console     | [Click here to view](https://intl.cloud.tencent.com/document/product/436/32538) |
| API      | [Click here to view](https://intl.cloud.tencent.com/document/product/436/32360) |


