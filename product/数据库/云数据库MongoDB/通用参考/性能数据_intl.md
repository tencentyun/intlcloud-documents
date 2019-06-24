### Test tool
[Yahoo! Cloud Serving Benchmark](https://github.com/brianfrankcooper/YCSB).

### Test method
1. A single data entry is 1 KB.
2. Import up to 80% of the instance capacity. For example, if instance capacity is 100 GB, import 80 GB of data to the instance.
3. Split the operation into 50% read and 50% update to get QPS (Queries Per Second) data.
4. Since performance varies across use cases, specify the performance of the instance based on the test to address your business needs.

## High IO Instances Performance Information

| CPU | MEM | QPS |
|:--:|:--:|:--:|
| 1 core | 2 G | 3000 |
| 2 core | 4 G | 5000 |
| 2 core | 6 G | 6000 |
| 4 core | 8 G | 9000 |
| 4 cores | 12 G | 14000 |
| 6 cores | 16 G | 20000 |
| 10 cores | 24 G | 25000 |
| 12 cores | 32 G | 27000 |
| 18 cores | 48 G | 30000 |
| 24 cores | 64 G | 33000 |

## High IO (10GB) Instances Performance Information

| CPU | MEM | Number of Sets | Number of Documents in a Single Set | Test Data Set (GB) | Runtime (S) | Data Sampling Interval (S) | Average QPS (Rounded) |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| 2 cores | 4 G | 2 | 100 million | 79 | 1800 | 10 | 5000 |
| 4 cores | 8 G | 3 | 100 million | 118 | 1800 | 10 | 9000 |
| 6 cores | 16 G | 6 | 100 million | 237 | 1800 | 10 | 20000 |
| 12 cores | 32 G | 6 | 200 million | 426 | 1800 | 10 | 27000 |
| 24 cores | 64 G | 15 | 200 million | 1161 | 1800 | 10 | 33000 |
| 24 cores | 128 G | 30 | 200 million | 2317 | 1800 | 10 | 36000 |
| 32 cores | 240 G | 40 | 200 million | 3031 | 1800 | 10 | 39000 |

