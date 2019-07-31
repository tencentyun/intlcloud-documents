SCF has certain quota limits for each user account.


## Quota Limits

The quota limits for a user account are as follows:

| Item | Default quota limit |
| --- | --- |
| Maximum number of functions per region | 20 |
| Maximum number of concurrent executions per function | 20 |
| Maximum number of triggers per function | 4, where the maximum quantity is 2 for timer triggers, COS triggers, CMQ triggers, and Ckafka triggers, respectively |

The limits for the function runtime environment are as follows:

| Item | Quota limit |
| --- | --- |
| Memory allocation | 128-1,536 MB, in increments of 128 MB |
| Temporary cache space, i.e., size of the /tmp directory | 512 MB |
| Function execution duration | 1-300 seconds |
| Number of file descriptors | 1,024 |
| Total processes and threads | 1,024 |
| Sync request event size | 6 MB |
| Sync request response size | 6 MB |
| Async request event size | 128 KB |

## Increasing Limits

Currently, limits that can be increased include:

* Maximum number of functions per region
* Maximum number of concurrent executions per function
* Maximum number of triggers per function

To increase the limits, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1) and state the desired items and quantities.
