## Scenario
This document describes how to perform initialization operations on a Linux CVM data disk, such as formatting, partitioning, and creating a file system.

## Notes

- Before formatting, ensure that no data is stored on the data disk or important data has been backed up. After formatting, all data on the data disk will be cleared.
- To prevent service exceptions, ensure that the CVM has stopped providing external services before formatting.

## Directions

Follow the appropriate operation guide based on the disk capacity.
- If the disk capacity is less than 2 TB, follow [initializing CBS Cloud Disks (Linux)](https://intl.cloud.tencent.com/document/product/362/31597).
- If the disk capacity is 2 TB or more, follow [initializing CBS Cloud Disks (Linux)](https://intl.cloud.tencent.com/document/product/362/31598).

