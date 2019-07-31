Tencent Cloud Monitor provides the following monitoring metrics for CKafka instances:

| Metric name | Metric | Meaning | Unit | Dimension |
| ------------- | -------------- | ---------------------------------------- | ---- | -------------- |
| Execution duration | duration | The execution duration at the function level, which refers to the length of time from the start to the end of function code execution, averaged by granularity (1 minute or 5 minutes).                | Milliseconds | Function |
| Number of calls | invocation | The number of requests at the function level, summed by granularity (1 minute or 5 minutes).               | Times | Function |
| Number of errors | error | The number of errors generated after the function is executed, which currently include your errors and the platform errors, summed by granularity (1 minute or 5 minutes).               | Times | Function |
| Number of restricted requests | throttle | The number of requests that are restricted at the function level after the function concurrency limit is reached, summed by granularity (1 minute or 5 minutes).              | Times | Function |


