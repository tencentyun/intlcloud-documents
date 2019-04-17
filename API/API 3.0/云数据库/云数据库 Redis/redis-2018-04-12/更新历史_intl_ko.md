## 제4차 릴리스

런칭 시간: 2018-12-20 오후 7:18:40

이 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

기존 문서를 개선했습니다.

새로 추가한 API:

* [ModifyInstance](/document/api/239/31785)

## 제3차 릴리스

릴리스 시간: 2018-11-29 오후 3:50:12

이 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

기존 문서를 개선했습니다.

수정된 API:

* [CreateInstances](/document/api/239/20026)
	* 새로 추가된 입력 매개변수: RedisShardNum, RedisReplicasNum, ReplicasReadonly
* [DescribeInstances](/document/api/239/20018)
	* 새로 추가된 입력 매개변수: UniqVpcIds, UniqSubnetIds
* [UpgradeInstance](/document/api/239/20013)
	* 새로 추가된 입력 매개변수: RedisShardNum, RedisReplicasNum

## 제2차 릴리스

릴리스 시간: 2018-11-22 오후 7:23:49

이 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

기존 문서를 개선했습니다.

새로 추가한 API:

* [DescribeInstanceDealDetail](/document/api/239/30602)
* [DescribeProductInfo](/document/api/239/30600)
* [DescribeTaskInfo](/document/api/239/30601)

새로 추가한 데이터 아키텍처:

* [ProductConf](/document/api/239/20022#ProductConf)
* [RegionConf](/document/api/239/20022#RegionConf)
* [TradeDealDetail](/document/api/239/20022#TradeDealDetail)
* [ZoneCapacityConf](/document/api/239/20022#ZoneCapacityConf)

데이터 아키텍처 수정:

* [InstanceSet](/document/api/239/20022#InstanceSet)
	* 새로 추가한 멤버: Engine, ProductType, UniqVpcId, UniqSubnetId, BillingMode

## 제1차 릴리스

릴리스 시간: 2018-09-21 오전 11:22:59

이 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

기존 문서를 개선했습니다.

새로 추가한 API:

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

새로 추가한 데이터 아키텍처:

* [InstanceSet](/document/api/239/20022#InstanceSet)
* [RedisBackupSet](/document/api/239/20022#RedisBackupSet)


