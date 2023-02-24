COS offers the [file processing feature](https://www.tencentcloud.com/document/product/1045/52071) based on CI, which allows you to perform on-cloud file processing operations such as hash calculation in diverse online processing scenarios.

## File Processing Fees

File processing fees consist of **file hash calculation fees, file decompression fees, and multi-file zipping fees** as detailed below.

| Billable Item               | Description                                                   | Billing Cycle | Applicable Billing Mode                                         |
| -------------- | ------------------------------------------------------------ | -------- | -------------- |
| File hash calculation | Fees incurred by using the file hash calculation service. Such fees are charged by **the file size**. | Monthly | Pay-as-you-go       |
| File decompression       | Fees incurred by using the file decompression service. Such fees are charged by **the size of extracted files**. | Monthly | Pay-as-you-go       |
| Multi-file zipping | Fees incurred by using the multi-file zipping service. Such fees are charged by **the size of files to be zipped**. | Monthly | Pay-as-you-go       |

## File Processing Pricing

| Billable Item | Price |
| ------------ | ---------- |
| File hash calculation | 0.0075 USD/GB |
| File decompression | 0.0075 USD/GB |
| Multi-file zipping | 0.0075 USD/GB |

## Billing Example

Suppose you upload 200 files of 10 GB in total to a bucket and use the hash calculation and multi-file zipping features to process the files.

The fees incurred are as follows:

| Item | Unit Price | Billable Usage | Fees (Unit Price * Billable Usage) |
| ---------- | ---------- | ------- | ------------------- |
| File hash calculation | 0.0075 USD/GB | 10 GB  | 0.075 USD |
| Multi-file zipping | 0.0075 USD/GB | 10 GB | 0.075 USD   |
| **Monthly fees** |          -  |    -     | **0.15 USD**      |


>?Storage fees are charged by COS. 
