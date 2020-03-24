## Overview

Tencent Cloud products will generate a large number of logs during operations, which record your business situation for future analysis to facilitate your business development and decision-making. You can leverage the storage capabilities of COS to persistently store Tencent Cloud product logs. Specifically, you can use methods such as APIs, SDKs, and tools to easily and quickly get logs from COS and analyze them.

Storing Tencent Cloud product logs in COS helps meet your following needs:

- **Persistent storage**: COS provides stable and persistent storage services. You can persistently store your logs in COS at very low costs. When log-based analysis or decision-making is required for your business, you can get the logs for any time period from COS anywhere, anytime.
- **Data retrieval**: COS supports SELECT statements that provide simple retrieval and extraction features for logs stored in COS. You can retrieve desired information only by entering log fields, which can reduce the data download traffic.
- **Data analysis**: you can select one or multiple log files stored in COS, use Sparkling to analyze them, and make decisions based on the analysis results.

## Log Shipping Methods

You can use either of the following two methods to store Tencent Cloud product logs to COS:

- Using the log shipping feature built in Tencent Cloud products; for example, for products such as COS, CLB, and CA, you can directly ship their logs to COS.
- Using the shipping feature of CLS: Tencent Cloud product logs that are shipped to CLS can be further shipped to COS through CLS for persistent storage.

Currently, the support of Tencent Cloud products for the two methods is as follows:

| Tencent Cloud Product Name          | Directly Shipped to COS | Shipped to CLS     |
| ------------------- | ---------------------- | ---------------------- |
| CloudAudit (CA)           | Yes                     | No                     |
| Cloud Load Balancer (CLB)        | Yes                     | Yes                     |
| Cloud Kafka (CKafka)     | Yes                     | No                     |
| API Gateway | No                     | Yes                     |
| Serverless Cloud Function (SCF)      | No                     | Yes                     |
| Tencent Kubernetes Engine (TKE)        | No                     | Yes                     |
| Live Video Broadcasting (LVB)          | No                     | Yes                     |
| Tencent Cloud Base (TCB)          | No                     | Yes; however, shipping from CLS to COS is not supported |
| Cloud Object Storage (COS)        | Yes                     | No          |

### Directly shipping logs to COS

The following Tencent Cloud products support directly shipping logs to COS. You can configure log shipping rules as instructed in the product documentation to ship logs to COS.

| Tencent Cloud Product Name | Log Shipping Document | Log Shipping Interval | Log Shipping Path |
| --------------- | ------------------------------------------------------------ | -------------------- | ------------------------------------------------------------ |
| CA |[Click here](https://intl.cloud.tencent.com/document/product/1021/30338) | 10–15 minutes |  cloudaudit/customprefix/timestamp|
| CLB    | [Click here](https://cloud.tencent.com/document/product/214/10329) | 60 minutes               | lb-id/timestamp                                              |
| CKafka | [Click here](https://cloud.tencent.com/document/product/597/17273) | 5–60 minutes<br>, which can be specified | instance id/topic id/timestamp                           |
| COS    | [Click here](https://intl.cloud.tencent.com/document/product/436/17040) | 5 minutes                | The path prefix can be specified. You are recommended to set a meaningful path, such as cos_bucketname_access_log/timestamp |

>Message data generated in CKafka can be shipped. If you want to get logs of operations such as CKafka instance creation, you can choose to ship CA logs.

### Shipping logs to COS through CLS

Certain Tencent Cloud products support log shipping to CLS for log retrieval and analysis. CLS can also ship logs to COS for persistent storage. For such products, you can enable log shipping to COS in the CLS Console to persistently store your log data. This reduces your storage costs and facilitates further offline analysis. Currently, the following products support log shipping to CLS:

| Tencent Cloud Product Name           | Log Shipping Document                                                 |
| -------------------- | ------------------------------------------------------------ |
| API Gateway | [Click here](https://cloud.tencent.com/document/product/628/19552) |                               
| TKE         | [Click here](https://intl.cloud.tencent.com/document/product/457/13659) |
| LVB           | [Click here](https://cloud.tencent.com/document/product/267/33996) |

Logs in CLS can be shipped to COS by using any of the following three formats:

- Delimited format: you can ship log data in delimited format to COS. For more information, please see [Shipping in Delimited Format](https://cloud.tencent.com/document/product/614/33814).
- JSON format: you can ship log data in JSON format to COS. For more information, please see [Shipping in JSON Format](https://cloud.tencent.com/document/product/614/33815).
- Source format: you can ship log data in the source format to COS. Single-line and multi-line full text shipping is supported, and some source text can be shipped in CSV format. For more information, please see [Shipping in Source Format](https://cloud.tencent.com/document/product/614/33816).

You need to perform the following steps to ship logs to COS through CLS:

1. Select the product based on your business needs. Then, configure the logset and log topic as instructed in the product log shipping documentation provided above to import the log data generated by your business to CLS.
2. Select an appropriate format to ship data to COS based on your business needs. When shipping logs, you are recommended to enter the product name as the path prefix in order to differentiate between logs of different products. For example, you can name TKE logs as `TKE_tkeid_log/timestamp`.
3. After configuring a shipping rule, you can configure an event notification for file upload in SCF, so that you can perform further operations based on the event notification after logs are shipped to COS. For more information, please see [Event Notifications](https://intl.cloud.tencent.com/document/product/436/31648).

## Log Analysis

### Downloading logs to local file system for offline analysis

You can download logs to your local file system in various methods such as console, SDKs, APIs, or tools. Documentation for all download methods is provided below for your reference. You can replace the file path in the code with your actual log storage path to download logs.

| Download Method       | Description                                                     |
| -------------- | ------------------------------------------------------------ |
| Console         | [Click here](https://intl.cloud.tencent.com/document/product/436/13322) |
| COSBrowser     | [Click here](https://cloud.tencent.com/document/product/436/38103#download) |
| COSCMD         | [Click here](https://intl.cloud.tencent.com/document/product/436/10976) |
| SDK for Android    | [Click here](https://intl.cloud.tencent.com/document/product/436/30596) |
| SDK for C          | [Click here](https://intl.cloud.tencent.com/document/product/436/30596) |
| SDK for C++        | [Click here](https://intl.cloud.tencent.com/document/product/436/30596) |
| SDK for .NET       | [Click here](https://intl.cloud.tencent.com/document/product/436/30596) |
| SDK for Go         | [Click here](https://intl.cloud.tencent.com/document/product/436/30596) |
| SDK for iOS        | [Click here](https://cloud.tencent.com/document/product/436/11280#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1) |
| SDK for Java       | [Click here](https://intl.cloud.tencent.com/document/product/436/30596) |
| SDK for JavaScript | [Click here](https://intl.cloud.tencent.com/document/product/436/30596) |
| SDK for Node.js    | [Click here](https://cloud.tencent.com/document/product/436/36119#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1) |
| SDK for PHP        | [Click here](https://intl.cloud.tencent.com/document/product/436/30596) |
| SDK for Python     | [Click here](https://cloud.tencent.com/document/product/436/35151) |
| SDK for WeChat Mini Program     | [Click here](https://intl.cloud.tencent.com/document/product/436/30596) |
| API            | [Click here](https://cloud.tencent.com/document/product/436/7753) |

### Analyzing logs with COS Select

You can use the COS Select feature to directly retrieve and analyze log files in CSV or JSON format stored in COS. With COS Select, you can filter desired log fields, which greatly reduces the data volume of logs transferred by COS and thus reduces your use costs and improves the data acquisition efficiency. For more information on COS Select, please see [Select Overview](https://cloud.tencent.com/document/product/436/37635).

Currently, you can use COS Select through the console or API.

| Method | Description                                                     |
| -------- | ------------------------------------------------------------ |
| Console   | [Click here](https://cloud.tencent.com/document/product/436/37642) |
| API      | [Click here](https://cloud.tencent.com/document/product/436/37641) |

### Analyzing logs with Sparkling

If you want to collect and aggregate the logs of all Tencent Cloud products for big data analysis, you are commended to use Tencent Sparkling Data Warehouse Suite (Sparkling). Based on the industry-leading Apache Spark framework, Sparkling offers a rich set of fully-managed, easy-to-use, and high-performance cloud data warehousing services. It provides a one-stop solution for big data development and data computing. By leveraging its cross-data source conjoint analysis feature, you can analyze aggregated logs of different Tencent Cloud products and tap into the value of log data.

For more information on how to use Sparkling, please see the [Sparkling](https://cloud.tencent.com/document/product/1002) product documentation or [Analyze COS Server Access Logs with Sparkling](https://cloud.tencent.com/document/product/436/37419).
