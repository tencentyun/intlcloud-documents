Dear user,
TencentDB for Redis will discontinue API [DescribeInstanceMonitorBigKey] (https://www.tencentcloud.com/document/product/239/35207) for querying the big key of an instance on October 31, 2022, but this feature will continue to serve through the API `DescribeRedisTopBigKeys` of DBbrain. 

TencentDB for DBbrain (DBbrain) is an intelligent database diagnosis and optimization product that provides real-time performance diagnosis and security protection services. It troubleshoots efficiently, offers solutions to database exceptions, and helps you prevent exceptions at the source. It can also help improve the overall database performance with its AI-powered parameter tuning capabilities.

`DescribeRedisTopBigKeys` of DBbrain can specify the sorting field and type of the `Key` to quickly query of big key information of an instance, including expiration time, memory size, element quantity, and the max element length.

## List of deprecated APIs
`DescribeInstanceMonitorBigKey` API and its associated APIs. `escribeInstanceMonitorBigKeySizeDist`·and `DescribeInstanceMonitorBigKeyTypeDist` will be deprecated simultaneously.

| API Name | Description |
| :----------------------------------------------------------- | :-------------------- |
| [DescribeInstanceMonitorBigKey](www.tencentcloud.com/document/product/239/35207) | Queries the big key of an instance |
| [DescribeInstanceMonitorBigKeySizeDist](www.tencentcloud.com/document/product/239/35206) | Queries the big key size distribution of an instance |
| [DescribeInstanceMonitorBigKeyTypeDist](www.tencentcloud.com/document/product/239/35205) | Queries the big key type distribution of an instance |

