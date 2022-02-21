

The shipping feature of CLS helps connect the downstream segments of your product ecosystem. It allows you to ship log data to Cloud Object Storage (COS) or other Tencent Cloud products to make better use of your logs. Shipping is an asynchronous process. With simple configuration in the CLS console, you can ship any log data collected by CLS to other Tencent Cloud products for storage or analysis.

## Shipping to COS

CLS allows you to ship data in a log topic to COS for purposes including:

- Archiving log data for the long term by managing the lifecycles of COS buckets
- Processing logs in COS through offline computing or using other computing programs

| Shipping Method                                                 | Description                                |
| ------------------------------------------------------------ | --------------------------------------- |
| [CSV Shipping](https://intl.cloud.tencent.com/document/product/614/31582) | Log data is shipped to COS in the CSV format.  |
| [JSON Shipping](https://intl.cloud.tencent.com/document/product/614/31583) | Log data is shipped to COS in the JSON format. |
| [Source Format Shipping](https://intl.cloud.tencent.com/document/product/614/31584) | Log data is shipped to COS in the source format.   |

>!
>- After logs are shipped to COS, you will be charged for storing data with COS. For more information about the billing of COS, see [Billing Overview](https://cloud.tencent.com/document/product/436/16871).
>- To cleanse log data before shipping to COS, please see [CLS Dump to COS](https://intl.cloud.tencent.com/document/product/614/38886).

