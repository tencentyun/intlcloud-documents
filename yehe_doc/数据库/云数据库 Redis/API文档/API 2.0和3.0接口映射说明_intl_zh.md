Redis API 2.0 版本接口将于2020年5月26日下线，调用 API V2 版接口届时将不可用，请尽快迁移至相对应的 API 3.0 接口。

### 接口映射关系

| Action(V2)          | 接口名(V2)            | Action(V3)                | 接口名(V3)                      |
| :--------------------- | :------------------ | :------------------------ | :------------------------------- |
| DescribeRedis             | 查询实例列表          | DescribeInstances         | [查询 Redis 实例列表](https://intl.cloud.tencent.com/document/product/239/32065) |
| DescribeRedisProduct      | 查询可创建实例规格    | DescribeProductInfo       | [查询产品售卖规格](https://intl.cloud.tencent.com/document/product/239/32077) |
| DescribeRedisZones        | 查询售卖可用区        | DescribeProductInfo       | [查询产品售卖规格](https://intl.cloud.tencent.com/document/product/239/32077) |
| GetBackupDownloadUrl      | 查询备份 Rdb下载地址   | DescribeBackupUrl         | [查询备份 Rdb 下载地址](https://intl.cloud.tencent.com/document/product/239/32075) |
| GetRedisBackupList        | 查询 Redis 实例备份列表 | DescribeInstanceBackups   | [查询 Redis 实例备份列表](https://intl.cloud.tencent.com/document/product/239/32074) |

