

According to the security requirements of Tencent Cloud, APIs that are directly accessed now require CAM authentication for access from April 8, 2022. Please grant access permissions for following APIs in the [CAM console](https://console.cloud.tencent.com/cam/policy) before April 8, 2022 so that you can use them normally.

## Note 
If you use the QcloudDBBRAINFullAccess authentication policy, you don’t need to modify it.

## APIs that require CAM authentication (eight in total)

| API Name                                                     | API Description                           | API Type |
| ------------------------------------------------------------ | ---------------------------------- | -------- |
| [DescribeSlowLogUserHostStats](https://intl.cloud.tencent.com/document/product/1035/41182) | Gets the slow log source address chart       | Resource-level   |
| [DescribeUserSqlAdvice](https://intl.cloud.tencent.com/document/product/1035/41181) | Gets SQL statement optimization suggestions                  | Resource-level   |
| [DescribeMySqlProcessList](https://intl.cloud.tencent.com/document/product/1035/41193) | Gets the real-time thread list                   | Resource-level   |
| [DescribeTopSpaceSchemas](https://intl.cloud.tencent.com/document/product/1035/41189) | Gets the space statistics of top databases           | Resource-level   |
| [DescribeDBDiagEvents](https://intl.cloud.tencent.com/document/product/1035/44292) | Gets the diagnosis event list                   | Operation-level   |
| [DescribeProxySessionKillTasks](https://intl.cloud.tencent.com/document/product/1035/45410) | Queries the status of the session killing task executed by the proxy node  | Resource-level   |
| [DescribeDiagDBInstances](https://intl.cloud.tencent.com/document/product/1035/41195) | Gets the instance list                   | Operation-level   |
| [CreateProxySessionKillTask](https://intl.cloud.tencent.com/document/product/1035/44869) | Creates a task of killing proxy node sessions         | Resource-level   |

