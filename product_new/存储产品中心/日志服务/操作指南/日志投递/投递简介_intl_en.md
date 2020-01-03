

Cloud Log Service (CLS) connects to downstream linkages of the product ecosystem, and ships logs to Cloud Object Storage (COS) and other Tencent Cloud products, which further meets log scenario requirements and extracts further value from logs. Logs are shipped asynchronously. All logs collected in CLS can be configured to ship to other cloud products for storage and analysis. It only requires simple configuration in the CLS Console to ship the logs.

## Shipping a log to COS

CLS allows you to ship data in a log topic to COS to meet the requirements of other application scenarios, for example:

- Setting COS lifecycle to keep logs in archive storage class for long periods.
- Processing logs in COS through offline computing or other computing programs.

| Data Shipping Format                                                 | Description                                |
| ------------------------------------------------------------ | --------------------------------------- |
| [CSV Shipping](https://intl.cloud.tencent.com/document/product/614/31582) | Logs are shipped to COS in the CSV format.  |
| [JSON Shipping](https://intl.cloud.tencent.com/document/product/614/31583) | Logs are shipped to COS in the JSON format. |
| [Source Format Shipping](https://intl.cloud.tencent.com/document/product/614/31584) | Logs are shipped to COS in the source format.   |

>After logs are shipped to COS, storage costs are generated on the COS side. For more information about billing, see the COS [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871).
