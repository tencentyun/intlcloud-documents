SCF has certain quota limits for each user account.


## Quota Limits

The quota limits for a user account are as follows:

| Item | Default quota limit |
| --- | --- |
| Maximum number of functions per region | 50 |
| Maximum number of concurrent executions per function | 300 |
| Maximum number of triggers per function | 10 |
| Triggers of the same type | 10 |

>SCF currently supports 10,000-level concurrence, which can effectively support scenarios with high concurrence demand such as e-commerce promotions and parallel processing of medical and biological data.
>For purposes of usage demand and security, the default maximum number of concurrent executions per function is set to 300. To request an increase in quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1).

The limits for the function runtime environment are as follows:

| Item | Quota limit |
| --- | --- |
| Memory assigned | Minimum: 128 MB, maximum: 1536 MB, increased by 128 MB |
| Temporary cache space, i.e., size of the `/tmp` directory | 512 MB |
| Timeout interval | Minimum: 1 second, maximum: 900 seconds |
| Number of file descriptors | 1024 |
| Total processes and threads | 1024 |
| Sync request event size | 6 MB |
| Sync request response size | 6 MB |
| Async request event size | 128 KB |

## Increasing Limits

Currently, limits that can be increased include:

* Maximum number of functions
* Maximum number of concurrent executions per function
* Maximum number of triggers per function

To increase the limits, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1) and state the desired items and quantities.
