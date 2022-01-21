## Error Description
- Symptom 1: the execution latency was high.
![](https://qcloudimg.tencent-cloud.cn/raw/54be4ba25f7a821e9686972690a942cb.png)
- Symptom 2: the business was affected.

## Common Causes
- The total number of requests was too high.
- The traffic and connections were restricted.
- There were complex commands such as KEYS \* and MGET.

## Solution
You can check whether the above problems exist based on the monitoring data in the console and your own business logic and make targeted optimizations.

## Troubleshooting Procedure
1. If the total number of requests is high, see [High Number of Total Requests](https://intl.cloud.tencent.com/document/product/239/44295).
2. If the traffic is restricted, see [High Outbound Traffic](https://intl.cloud.tencent.com/document/product/239/41812). If the number of connections is restricted, see [High Connection Utilization](https://intl.cloud.tencent.com/document/product/239/44296).
3. Optimize complex commands. If there is a KEYS \*command, you can consider using the SCAN command to traverse in batches instead of using KEYS with a higher time complexity. If there is an MGET command, you can consider splitting it into n operations to get n keys.


>?If the problem persists, [contact us](https://cloud.tencent.com/online-service?from=connect-us).
