## 第 4 回リリース

リリース日時：2018-12-20 19:18:40

今回のリリースには以下の内容を含みます。

既存のドキュメントを改善しました。

追加したインターフェースは次の通りです。

* [ModifyInstance](/document/api/239/31785)

## 第 3 回リリース

リリース日時：2018-11-29 15:50:12

今回のリリースには以下の内容を含みます。

既存のドキュメントを改善しました。

修正したインターフェースは次の通りです。

* [CreateInstances](/document/api/239/20026)
	* パラメータインプットの追加：RedisShardNum, RedisReplicasNum, ReplicasReadonly
* [DescribeInstances](/document/api/239/20018)
	* パラメータインプットの追加：UniqVpcIds, UniqSubnetIds
* [UpgradeInstance](/document/api/239/20013)
	* パラメータインプットの追加：RedisShardNum, RedisReplicasNum

## 第 2 回リリース

リリース日時：2018-11-22 19:23:49

今回のリリースには以下の内容を含みます。

既存のドキュメントを改善しました。

追加したインターフェースは次の通りです。

* [DescribeInstanceDealDetail](/document/api/239/30602)
* [DescribeProductInfo](/document/api/239/30600)
* [DescribeTaskInfo](/document/api/239/30601)

追加したデータ構造：

* [ProductConf](/document/api/239/20022#ProductConf)
* [RegionConf](/document/api/239/20022#RegionConf)
* [TradeDealDetail](/document/api/239/20022#TradeDealDetail)
* [ZoneCapacityConf](/document/api/239/20022#ZoneCapacityConf)

修正したデータ構造：

* [InstanceSet](/document/api/239/20022#InstanceSet)
	* 追加メンバー：Engine, ProductType, UniqVpcId, UniqSubnetId, BillingMode

## 第 1 回リリース

リリース日時：2018-09-21 11:22:59

今回のリリースには以下の内容を含みます。

既存のドキュメントを改善しました。

追加したインターフェースは次の通りです。

* [ClearInstance](/document/api/239/20021)
* [CreateInstances](/document/api/239/20026)
* [DescribeAutoBackupConfig](/document/api/239/20019)
* [DescribeInstanceBackups](/document/api/239/20011)
* [DescribeInstances](/document/api/239/20018)
* [ManualBackupInstance](/document/api/239/20010)
* [ModfiyInstancePassword](/document/api/239/20025)
* [ModifyAutoBackupConfig](/document/api/239/20016)
* [RenewInstance](/document/api/239/20015)
* [ResetPassword](/document/api/239/20014)
* [UpgradeInstance](/document/api/239/20013)

追加したデータ構造：

* [InstanceSet](/document/api/239/20022#InstanceSet)
* [RedisBackupSet](/document/api/239/20022#RedisBackupSet)


