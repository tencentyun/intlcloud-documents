## 第 4 回リリース

リリース日時：2018-12-20 19:18:40

今回のリリースには以下の内容を含みます。

既存のドキュメントを改善しました。

追加したインターフェースは次の通りです。

* [ModifyInstance](https://cloud.tencent.com/document/api/239/31785)

## 第 3 回リリース

リリース日時：2018-11-29 15:50:12

今回のリリースには以下の内容を含みます。

既存のドキュメントを改善しました。

修正したインターフェースは次の通りです。

* [CreateInstances](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20026)
	* パラメータインプットの追加：RedisShardNum, RedisReplicasNum, ReplicasReadonly
* [DescribeInstances](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20018)
	* パラメータインプットの追加：UniqVpcIds, UniqSubnetIds
* [UpgradeInstance](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20013)
	* パラメータインプットの追加：RedisShardNum, RedisReplicasNum

## 第 2 回リリース

リリース日時：2018-11-22 19:23:49

今回のリリースには以下の内容を含みます。

既存のドキュメントを改善しました。

追加したインターフェースは次の通りです。

* [DescribeInstanceDealDetail](https://cloud.tencent.com/document/api/239/30602)
* [DescribeProductInfo](https://cloud.tencent.com/document/api/239/30600)
* [DescribeTaskInfo](https://cloud.tencent.com/document/api/239/30601)

追加したデータ構造：

* [ProductConf](https://cloud.tencent.com/document/api/239/20022#ProductConf)
* [RegionConf](https://cloud.tencent.com/document/api/239/20022#RegionConf)
* [TradeDealDetail](https://cloud.tencent.com/document/api/239/20022#TradeDealDetail)
* [ZoneCapacityConf](https://cloud.tencent.com/document/api/239/20022#ZoneCapacityConf)

修正したデータ構造：

* [InstanceSet](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20022#InstanceSet)
	* 追加メンバー：Engine, ProductType, UniqVpcId, UniqSubnetId, BillingMode

## 第 1 回リリース

リリース日時：2018-09-21 11:22:59

今回のリリースには以下の内容を含みます。

既存のドキュメントを改善しました。

追加したインターフェースは次の通りです。

* [ClearInstance](https://cloud.tencent.com/document/api/239/20021)
* [CreateInstances](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20026)
* [DescribeAutoBackupConfig](https://cloud.tencent.com/document/api/239/20019)
* [DescribeInstanceBackups](https://cloud.tencent.com/document/api/239/20011)
* [DescribeInstances](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20018)
* [ManualBackupInstance](https://cloud.tencent.com/document/api/239/20010)
* [ModfiyInstancePassword](https://cloud.tencent.com/document/api/239/20025)
* [ModifyAutoBackupConfig](https://cloud.tencent.com/document/api/239/20016)
* [RenewInstance](https://cloud.tencent.com/document/api/239/20015)
* [ResetPassword](https://cloud.tencent.com/document/api/239/20014)
* [UpgradeInstance](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20013)

追加したデータ構造：

* [InstanceSet](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20022#InstanceSet)
* [RedisBackupSet](https://cloud.tencent.com/document/api/239/20022#RedisBackupSet)


