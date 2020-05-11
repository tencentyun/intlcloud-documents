## Testing Tool
[Yahoo! Cloud Serving Benchmark](https://github.com/brianfrankcooper/YCSB).

## Testing Method
1. A single data entry is 1 KB in size.
2. Import up to 80% of the instance capacity. For example, if the instance capacity is 100 GB, import 80 GB of data into the instance.
3. Perform 50% read and 50% update operations to get the QPS (queries per second) data.
4. As performance varies by scenario, please select instances with appropriate specifications according to your business requirements and the test data.

## Performance Data of High IO Instances

| CPU | MEM | QPS |
|:--:|:--:|:--:|
|1 core | 2 GB | 3,000 |
| 2 cores | 4 GB | 5,000 |
| 2 cores | 6 GB | 6,000 |
| 4 cores | 8 GB | 9,000 |
| 4 cores | 12 GB | 14,000 |
| 6 cores | 16 GB | 20,000 |
| 10 cores |24 GB | 25,000 |
| 12 cores | 32 GB | 27,000 |
| 18 cores | 48 GB | 30,000 |
| 24 cores | 64 GB | 33,000 |

## Performance Data of Ten-Gigabit High IO Instances 

| CPU | MEM | Number of Collections | Number of Documents per Collection | Test Dataset (GB) | Runtime (s) | Data Sampling Interval (s) | Average QPS (Rounded) |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| 2 cores | 4 GB | 2 | 100 million | 79 | 1,800 | 10 | 5,000 |
| 4 cores | 8 GB | 3 | 100 million | 118 | 1,800 | 10 | 9,000 |
| 6 cores | 16 GB | 6 | 100 million | 237 | 1,800 | 10 | 20,000 |
| 12 cores | 32 GB | 6 | 200 million | 426 | 1,800 | 10 | 27,000 |
| 24 cores | 64 GB | 15 | 200 million | 1,161 | 1,800 | 10 | 33,000 |
| 24 cores | 128 GB | 30 | 200 million | 2,317 | 1,800 | 10 | 36,000 |
| 32 cores | 240 GB | 40 | 200 million | 3,031 | 1,800 | 10 | 39,000 |
