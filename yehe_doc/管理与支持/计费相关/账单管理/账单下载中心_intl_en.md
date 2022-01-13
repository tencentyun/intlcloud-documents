### Overview

Bill Download Center is a new console feature we rolled out in January 2022. It is currently in beta testing and is expected to be available to all users in mid-February. You can download your bill data since Bills 3.0 (released in July 2021). Specifically, you can:

1. Download bill packages, PDF bills (L0), bill summary (L1), bills by instance (L2), and bill details (L3)

2. Download bill data for multiple months

3. Download bill data for an account and selected sub-accounts

4. Download aggregated bill data (the data of hourly/daily billed products can be aggregated by month before download to reduce the number of bill entries)

### Directions

### PDF bills (L0)

Use case: L0 bills are in PDF format and can be used for payment requesting or archiving. You can download the L0 bills of multiple months at a time.

1. Download the L0 bills of the current account:

![img](https://qcloudimg.tencent-cloud.cn/raw/71452889cf76603d785ed3a7f6c5002a.png)

2. Download the L0 bills of the current account and selected sub-accounts:

![img](https://qcloudimg.tencent-cloud.cn/raw/3e52fe437197825906de706353e48dd7.png)

#### Bill summary (L1)

Use case: L1 bills offer bill data by product, project, region, tag, etc., allowing you to view bill information by different metrics. You can download the bill summary of multiple months in one file and can specify whether to aggregate the data of different accounts. For example, you can download the bill summary of an account in the past 6 months by product.

1. Download the L1 bills of the current account:

![img](https://qcloudimg.tencent-cloud.cn/raw/3894fe076950876c3e65a41c449f8dd5.png)

2. Download the L1 bills of the current account and selected sub-accounts:

![img](https://qcloudimg.tencent-cloud.cn/raw/4d46e3de292620cc06c11dbb53bccdd4.png)

#### Bills by instance (L2)

Use case: L2 bills offer bill data by instance (resource) ID. You can download the L2 bills of multiple months in one file and can specify whether to aggregate the data of different accounts.

1. Download the L2 bills of the current account:

![img](https://qcloudimg.tencent-cloud.cn/raw/1f71da394bfc46ca94e2716a769a55c2.png)

2. Download the L2 bills of the current account and selected sub-accounts:

![img](https://qcloudimg.tencent-cloud.cn/raw/f6ba98ec51478747cc7d6388cb1824b5.png)

#### Bill details (L3)

Use case: L3 bills offer bill data at the component level. You can download the L3 bills of multiple months at a time and can specify whether to aggregate the data by month.

1. Download the L3 bills of the current account and specify whether to aggregate the data by month:

![img](https://qcloudimg.tencent-cloud.cn/raw/005e511aa7bddbc5aede2864c36243fc.png)

2. Download the L3 bills of the current account and selected sub-accounts and specify whether to aggregate the data by month:

![img](https://qcloudimg.tencent-cloud.cn/raw/4733193e1f557d26a5dd2044e210588b.png)

### References

#### How aggregation by month works for L3 bills

##### Products billed by resource used

For components (e.g., those with “bandwidth” in their names) billed by the amount of resources used during a fixed billing period, aggregation by month aggregates the usages and costs of the same instance ID in a month into one bill entry.

1. Data is aggregated only for transactions whose type is `Hourly settlement`, `Daily settlement`, `Spot`, `Hourly RI fee`, or `Hourly Savings Plan fee`.

2. Components with “traffic”, “bandwidth”, “storage”, and “times” in their names are billed by the amount of resources used, but depending on the situation, some of these components may also be switched to billing by time used.

3. Data is aggregated by the following dimensions:

Billing month, billing mode, transaction type, product, subproduct, component type, component name, instance ID, region, discount, component list price, component unit price, usage duration, and tax rate

4. Aggregation logic for different fields:

- `Component Usage`, `Original Cost`, `Total Amount After Discount (Excluding Tax)`, `Voucher Deduction`, `Amount Before Tax`, `Tax Amount`, `Total Cost (Including Tax)`: add up the values of all aggregated entries
- `Usage Start Time`: display the earliest usage start time of the aggregated entries
- `Usage End Time`: display the latest usage end time of the aggregated entries
- `Order ID`, `Transaction ID`, `Transaction Time`: display `-`
- Other fields: display the same as in bill details

##### Products billed by time used

For components (e.g., those with “CVM” in their names) billed by the period of time a fixed amount of resources is used, aggregation by month aggregates the usage durations and costs of the same instance ID in a month into one bill entry.

1. Data is aggregated only for transactions whose type is `Hourly settlement`, `Daily settlement`, `Spot`, `Hourly RI fee`, or `Hourly Savings Plan fee`.

2. Components not billed by the amount of resources used are billed by time used.

3. Data is aggregated by the following dimensions:

Billing month, billing mode, transaction type, product, subproduct, component type, component name, instance ID, region, discount, component list price, component unit price, usage, and tax rate

4. Aggregation logic for different fields:

- `Usage Duration`, `Original Cost`, `Total Amount After Discount (Excluding Tax)`, `Voucher Deduction`, `Amount Before Tax`, `Tax Amount`, `Total Cost (Including Tax)`: add up the values of all aggregated entries
- `Usage Start Time`: display the earliest usage start time of the aggregated entries
- `Usage End Time`: display the latest usage end time of the aggregated entries
- `Order ID`, `Transaction ID`, `Transaction Time`: display `-`
- Other fields: display the same as in bill details

##### Data not aggregated

Data is not aggregated for transactions whose type is not `Hourly settlement`, `Daily settlement`, `Spot`, `Hourly RI fee`, or `Hourly Savings Plan fee` and such data is displayed the same as in bill details.