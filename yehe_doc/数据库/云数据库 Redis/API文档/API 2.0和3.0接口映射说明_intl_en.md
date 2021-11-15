TencentDB for Redis API 2.0 will be deprecated on May 26, 2020. The API 2.0 will no longer be available, so please migrate to API 3.0 as soon as possible.

### Mappings Between the 2.0 and 3.0 APIs

| Action (v2.0)          | API Name (v2.0)            | Action (v3.0)                | API Name (v3.0)                      |
| :--------------------- | :------------------ | :------------------------ | :------------------------------- |
| DescribeRedis             | Queries the list of instances          | DescribeInstances         | [Queries the list of Redis instances](https://intl.cloud.tencent.com/document/product/239/32065) |
| DescribeRedisProduct      | Queries the supported instance specifications    | DescribeProductInfo       | [Queries the purchasable product specifications](https://intl.cloud.tencent.com/document/product/239/32077) |
| DescribeRedisZones        | Queries purchasable AZs        | DescribeProductInfo       | [Queries the purchasable product specifications](https://intl.cloud.tencent.com/document/product/239/32077) |
| GetBackupDownloadUrl      | Queries the download address of an RDB backup   | DescribeBackupUrl         | [Queries the download address of an RDB backup](https://intl.cloud.tencent.com/document/product/239/32075) |
| GetRedisBackupList        | Queries the list of Redis instance backups | DescribeInstanceBackups   | [Queries the list of Redis instance backups](https://intl.cloud.tencent.com/document/product/239/32074) |

