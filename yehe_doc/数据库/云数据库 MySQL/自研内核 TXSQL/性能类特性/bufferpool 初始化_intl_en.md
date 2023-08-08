## Overview
This feature speeds up the initialization of the buffer pool, reducing the startup time of the database instance.

### Supported versions
- Kernel version: MySQL 5.6 20200915 and above.
- Kernel version: MySQL 5.7 20200630 and above.

## Use Cases
This feature is used to speed up the startup of the database instance.

## Performance Test Data
Performance test data collected from eight instances:

| buffer_pool_size | Buffer Pool Initialization Time (Before Optimization) | Buffer Pool Initialization Time (After Optimization) | Increase (%) |
| :--------------: | :----------------------------- | :----------------------------- | :------: |
|       50 GB        | 2.55 s                          | 0.13 s                          |  1,962%   |
|       200 GB       | 10.28 s                         | 0.52 s                          |  1,977%   |
|       500 GB       | 25.72 s                         | 1.32 s                          |  1,948%   |

## Instructions
This feature is enabled in the kernel by default.
