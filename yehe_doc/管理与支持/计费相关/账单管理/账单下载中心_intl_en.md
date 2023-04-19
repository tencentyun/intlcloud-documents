## Overview

Bill Download became available in the **Billing Center** in January 2022. You can download your bill data generated after Bills 3.0 (released in July 2021). Specifically, you can:

1. Download bill packs, PDF bills (L0), bill summary (L1), bills by instance (L2), and bill details (L3).

2. Download bill data for multiple months.

3. Download bill data for an account and selected sub-accounts.

4. Download aggregated bill data (the data of hourly/daily billed products can be aggregated by month before download to reduce the number of bill entries).

## Directions

### PDF bills (L0)

L0 bills are in PDF format and can be used for your financial records or for sending to other departments to request payment. You can download the L0 bills of a multiple months at a time.

1. Download the L0 bills of your account:

![img](https://qcloudimg.tencent-cloud.cn/raw/456df0a32dfd695c80dce416df97b36b.png)

2. Download the L0 bills of your account and selected sub-accounts:

![img](https://qcloudimg.tencent-cloud.cn/raw/4d92d9d07c09c028861b7d950364e29a.png)

### Bill summary (L1)

L1 bills offer bill data by product, project, region, tag, etc., allowing you to view bill information by different metrics. You can download the bill summary of multiple months in one file and can specify whether to aggregate the data of different accounts.

1. Download the L1 bills of your account:

![img](https://qcloudimg.tencent-cloud.cn/raw/b32bca3a44e022d29dac80cde456bafd.png)

2. Download the L1 bills of your account and selected sub-accounts:

![img](https://qcloudimg.tencent-cloud.cn/raw/6896cdb672d6d9b1ea57b95fe2c70999.png)

### Bills by instance (L2)

L2 bills offer bill data by resource ID (instance). You can download the L2 bills of multiple months in one file and can specify whether to aggregate the data of different accounts.

1. Download the L2 bills of your account:

![img](https://qcloudimg.tencent-cloud.cn/raw/0296b5734363f02bca554e382b089745.png)

2. Download the L2 bills of your account and selected sub-accounts:

![img](https://qcloudimg.tencent-cloud.cn/raw/e4a895c497204096fe54e889627df1d3.png)

### Bill details (L3)

L3 bills offer bill data at the component level. You can download the L3 bills of multiple months at a time and can specify whether to aggregate the data by month.

1. Download the L3 bills of your account and specify whether to aggregate the data by month:

![img](https://qcloudimg.tencent-cloud.cn/raw/77478baccf07af13d3bc153c3953deca.png)

2. Download the L3 bills of your account and selected sub-accounts and specify whether to aggregate the data by month:

![img](https://qcloudimg.tencent-cloud.cn/raw/c572cdd87c750b113dc25540958197c6.png)

## References

### How aggregation by month works for L3 bills

#### Products billed by resource used

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

#### Products billed by time used

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

#### Data not aggregated

Data is not aggregated for transactions whose type is not `Hourly settlement`, `Daily settlement`, `Spot`, `Hourly RI fee`, or `Hourly Savings Plan fee` and such data is displayed the same as in bill details.
