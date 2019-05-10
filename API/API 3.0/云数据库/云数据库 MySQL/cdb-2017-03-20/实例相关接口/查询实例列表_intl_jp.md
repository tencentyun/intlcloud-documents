## 1. API説明

APIリクエストドメイン名： cdb.tencentcloudapi.com 。

このAPI（DescribeDBInstances）はデータベースインスタンスリストを照合するために使用されます。プロジェクトID、インスタンスID、アクセスアドレス、インスタンスステータスなどのフィルタリング条件によるインスタンスの選別をサポートします。マスタインスタンス、ディザスタリカバリインスタンス、読み取り専用インスタンス情報リストの照合をサポートします。

デフォルトのAPIリクエスト頻度制限：100回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：cdb.ap-shanghai-fsi.tencentcloudapi.com 。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/236/15833)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：DescribeDBInstances |
| Version | はい | String | 共通パラメータ、該当APIの値：2017/03/20 |
| Region | はい | String | 共通パラメータ。詳細について製品がサポートする[地域リスト](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| ProjectId | いいえ | Integer | プロジェクトID。[プロジェクトリストの照合](https://cloud.tencent.com/document/product/378/4400) APIでプロジェクトIDを照合できます |
| InstanceTypes.N | いいえ | Array of Integer | インスタンスタイプ。可能な値：1-マスタインスタンス、2-ディザスタリカバリインスタンス、3-読み取り専用インスタンス |
| Vips.N | いいえ | Array of String | インスタンスのプライベートネットワークIPアドレス |
| Status.N | いいえ | Array of Integer | インスタンスのステータス。可能な値：0-作成中、1-実行中、4-隔離中、5-隔離済 |
| Offset | いいえ | Integer | オフセット。デフォルト値は0 |
| Limit | いいえ | Integer | 単回リクエストによって返された数量。デフォルト値は20、最大値は2000 |
| SecurityGroupId | いいえ | String | セキュリティグループID |
| PayTypes.N | いいえ | Array of Integer | 支払タイプ。可能な値：0-年額/月額、1-時間別課金 |
| InstanceNames.N | いいえ | Array of String | インスタンス名 |
| TaskStatus.N | いいえ | Array of Integer | インスタンスタスクのステータス。可能な値：<br>0-タスクなし<br>1-アップグレード中<br>2-データインポート中<br>3-スレーブ開放中<br>4-パブリックネットワークアクセスオン<br>5-一括操作実行中<br>6-ロールバック中<br>7-パブリックネットワークアクセスオフ<br>8-パスワード変更中<br>9-インスタンス名変更中<br>10-再起動中<br>12-自作移行中<br>13-データベーステーブル削除中<br>14-ディザスタリカバリインスタンス同期作成中<br>15-アップグレード切り替え待ち<br>16-アップグレード切り替え中<br>17-アップグレード切り替え完了 |
| EngineVersions.N | いいえ | Array of String | インスタンスデータベースエンジンバージョン。可能な値：5.1、5.5、5.6と5.7 |
| VpcIds.N | いいえ | Array of Integer | VPCのID |
| ZoneIds.N | いいえ | Array of Integer | Availability ZoneのID |
| SubnetIds.N | いいえ | Array of Integer | サブネットID |
| CdbErrors.N | いいえ | Array of Integer | フラグがロックされるかどうか |
| OrderBy | いいえ | String | 返された結果セットで並び替えたフィールド。現時点でサポートするフィールド："InstanceId"、"InstanceName"、"CreateTime"、"DeadlineTime" |
| OrderDirection | いいえ | String | 返された結果セットの並び替え方式。現時点でサポートする方式："ASC"または"DESC" |
| WithSecurityGroup | いいえ | Integer | セキュリティグループの詳細情報が含まれるかどうか。可能な値：0-含まない、1-含む |
| WithExCluster | いいえ | Integer | 専有クラスタの詳細情報が含まれるかどうか。可能な値：0-含まない、1-含む |
| ExClusterId | いいえ | String | 専有クラスタID |
| InstanceIds.N | いいえ | Array of String | インスタンスID |
| InitFlag | いいえ | Integer | 初期化フラグ。可能な値：0-非初期化、1-初期化 |
| WithDr | いいえ | Integer | ディザスタリカバリインスタンスが含まれるかどうか。可能な値：0-含まない、1-含む |
| WithRo | いいえ | Integer | 読み取り専用インスタンスが含まれるかどうか。可能な値：0-含まない、1-含む |
| WithMaster | いいえ | Integer | マスタインスタンスが含まれるかどうか。可能な値：0-含まない、1-含む |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| TotalCount | Integer | 照合条件を満たすインスタンス総数|
| Items | Array of [InstanceInfo](/document/api/236/15878#InstanceInfo) | インスタンスの詳細情報|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 インスタンスリストの照合

#### 入力例

```
https://cdb.tencentcloudapi.com/?Action=DescribeDBInstances
&InstanceIds.0=cdb-70zdmgg1
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response":{
        "TotalCount": 1,
	"RequestId": "756bb037-a44a-4b4f-abe0-6efd34a6c792",
	"Items": [{
			"WanStatus": 0,
			"Zone": "ap-chengdu-1",
			"InitFlag": 1,
			"Memory": 1000,
			"Status": 1,
			"VpcId": 511512,
			"SlaveInfo": {
				"First": {
					"Vip": "",
					"Region": "ap-chengdu",
					"Vport": 0,
					"Zone": "ap-chengdu-1"
				}
			},
			"InstanceId": "cdb-70zdmgg1",
			"Volume": 50,
			"AutoRenew": 0,
			"ProtectMode": 0,
			"RoGroups": [{
					"RoInstances": [{
							"Status": 1,
							"VpcId": 511512,
							"InstanceType": 3,
							"Zone": "ap-chengdu-1",
							"Qps": 1000,
							"InstanceId": "cdbro-3i70uj0k",
							"Region": "ap-chengdu",
							"DeadlineTime": "0000-00-00 00:00:00",
							"PayType": 1,
							"TaskStatus": 0,
							"Volume": 50,
							"EngineVersion": "5.6",
							"DeviceType": "CUSTOM",
							"Memory": 1000,
							"SubnetId": 115839,
							"Vip": "172.16.0.11",
							"Vport": 3306,
							"InstanceName": "cdb_ro_103608",
							"HourFeeStatus": 1
						}
					],
					"MinRoInGroup": 1,
					"Vip": "172.16.0.11",
					"RoGroupName": "ro_group_103608",
					"Vport": 3306,
					"WeightMode": "system",
					"RoGroupId": "cdbrg-3i70uj0k",
					"RoMaxDelayTime": 1
				}, {
					"RoInstances": [{
							"Status": 1,
							"VpcId": 511512,
							"InstanceType": 3,
							"Zone": "ap-chengdu-1",
							"Qps": 1000,
							"InstanceId": "cdbro-6scijza8",
							"Region": "ap-chengdu",
							"DeadlineTime": "0000-00-00 00:00:00",
							"PayType": 1,
							"TaskStatus": 0,
							"Volume": 25,
							"EngineVersion": "5.6",
							"DeviceType": "CUSTOM",
							"Memory": 1000,
							"SubnetId": 115839,
							"Vip": "172.16.0.25",
							"Vport": 3306,
							"InstanceName": "cdb_ro_103610",
							"HourFeeStatus": 1
						}
					],
					"MinRoInGroup": 1,
					"Vip": "172.16.0.25",
					"RoGroupName": "ro_group_103610",
					"Vport": 3306,
					"WeightMode": "system",
					"RoGroupId": "cdbrg-6scijza8",
					"RoMaxDelayTime": 1
				}
			],
			"SubnetId": 115839,
			"InstanceType": 1,
			"ProjectId": 0,
			"Region": "ap-chengdu",
			"DeadlineTime": "0000-00-00 00:00:00",
			"DeployMode": 0,
			"TaskStatus": 0,
			"DeviceType": "CUSTOM",
			"EngineVersion": "5.6",
			"InstanceName": "jersey_test",
			"DrInfo": [],
			"UniqVpcId": "vpc-5v8wn9mg",
			"WanDomain": "",
			"WanPort": 0,
			"PayType": 1,
			"CreateTime": "2018-05-03 14:53:23",
			"Vip": "172.16.0.16",
			"UniqSubnetId": "subnet-1typ0s7d",
			"Vport": 3306,
			"CdbError": 0
		}
	]
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeDBInstances)

### SDK

クラウドAPI 3.0は、API呼び出しを容易にするために複数のプログラミング言語をサポートする、関連開発ツールセット（SDK）を提供します。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. エラーコード

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](/document/api/236/15835#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| CdbError | バックエンドエラーまたはプロセスエラー。 |
| InternalError.DatabaseAccessError | データベース内部エラー。 |
| InternalError.DesError | システム内部エラー。 |
| InvalidParameter | パラメータエラー。 |
| InvalidParameter.InstanceNotFound | インスタンスが存在しません。 |
| OperationDenied.WrongStatus | バックエンドタスクのステータスが不正です。 |

