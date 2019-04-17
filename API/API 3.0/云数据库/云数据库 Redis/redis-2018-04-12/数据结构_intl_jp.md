## InstanceSet

インスタンスの詳細情報リスト

次のインターフェースに引用されます：DescribeInstances。

| 名称 | タイプ |  説明 |
|------|------|-------|
| InstanceName | String | インスタンス名 |
| InstanceId | String | インスタンスId |
| Appid | Integer | ユーザーのAppid |
| ProjectId | Integer | プロジェクトId |
| RegionId | Integer | リージョンid 1--広州 4--上海 5-- 中国香港 6--トロント 7--上海金融 8--北京 9-- シンガポール 11--深圳金融 15--米国西部（シリコンバレー）16--成都 17--ドイツ 18--韓国 19--重慶 21--インド 22--米国東部（ヴァージニア）23--タイ 24--ロシア 25--日本 |
| ZoneId | Integer | エリアid |
| VpcId | Integer | 75101 のようなvpcネットワークid |
| SubnetId | Integer | 46315 のような vpcネットワークのサブネットワークid |
| Status | Integer | インスタンスの現在の状態は次の通りです。0：初期化中、1：インスタンスのプロセス中、2：インスタンス実行中、-2：インスタンス隔離済み、-3：インスタンス削除待ち |
| WanIp | String | インスタンスvip |
| Port | Integer | インスタンスポート番号 |
| Createtime | String | インスタンス作成時間 |
| Size | Float | インスタンスの容量サイズ。単位はMB |
| SizeUsed | Float | インスタンスが現在使用済みの容量。単位はMB |
| Type | Integer | インスタンスのタイプ。1：Redis2.8クラスタ版、2：Redis2.8マスタースレーブ版、3：CKVマスタースレーブ版（Redis3.2）、4：CKVクラスタ版（Redis3.2）、5：Redis2.8スタンドアロン版、7：Redis4.0クラスタ版 |
| AutoRenewFlag | Integer | インスタンスが自動更新識別を設定しているか。1：自動更新を設定している、0：自動更新を設定していない |
| DeadlineTime | String | インスタンスの期限切れ日時 |
| Engine | String | エンジン。コミュニティ版Redis、Tencent Cloud CKV |
| ProductType | String | 製品タイプ。Redis2.8クラスタ版、Redis2.8マスタースレーブ版、Redis3.2マスタースレーブ版（CKVマスタースレーブ版）、Redis3.2クラスタ版（CKVクラスタ版）、Redis2.8スタンドアロン版、Redis4.0クラスタ版 |
| UniqVpcId | String | pc-fk33jsf43kgv のようなvpcネットワークid |
| UniqSubnetId | String | subnet-fd3j6l35mm0 のようなvpcネットワークのサブネットワークid |
| BillingMode | Integer | 計算モデル：0-従量課金、1-年払い（月払い） |

## ProductConf

製品情報

次のインターフェースに引用されます：DescribeProductInfo。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Type | Integer | 製品タイプ。2-Redisマスタースレーブ版、3-CKVマスタースレーブ版、4-CKVクラスタ版、5-Redisスタンドアロン版、7-Redisクラスタ版 |
| TypeName | String | 製品名。Redisマスタースレーブ版、CKVマスタースレーブ版、CKVクラスタ版、Redisスタンドアロン版、Redisクラスタ版 |
| MinBuyNum | Integer | 購入時の最小数 |
| MaxBuyNum | Integer | 購入時の最大数 |
| Saleout | Boolean | 製品が完売しているか |
| Engine | String | 製品エンジン。Tencent Cloud CKV またはコミュニティ版 Redis |
| Version | String | 互換性があるバージョン。Redis-2.8、Redis-3.2、Redis-4.0 |
| TotalSize | Array of String | 仕様の合計サイズ。単位はG |
| ShardSize | Array of String | 各シャードのサイズ。単位はG |
| ReplicaNum | Array of String | コピー数 |
| ShardNum | Array of String | シャード数 |
| PayMode | String | サポートする課金モデル。1-年払い（月払い）、0-従量課金 |
| EnableRepicaReadOnly | Boolean | コピーの読み取り専用をサポートしているか |

## RedisBackupSet

インスタンスのバックアップ配列

次のインターフェースに引用されます：DescribeInstanceBackups。

| 名称 | タイプ |  説明 |
|------|------|-------|
| StartTime | String | バックアップの開始時間 |
| BackupId | String | バックアップID |
| BackupType | String | バックアップのタイプ。manualBackupInstance：ユーザーが起動する手動バックアップ、 systemBackupInstance：未明にシステムが起動するバックアップ |
| Status | Integer | バックアップの状態。  1:"バックアップはその他のプロセスにロックされています"、2:"バックアップは正常です。その他のプロセスにロックされていません"、  -1:"バックアップの期限が過ぎています"、3:"バックアップのエクスポート中です"、 4:"バックアップのエクスポートに成功しました" |
| Remark | String | バックアップの備考情報 |
| Locked | Integer | バックアップがロックされているか。0：ロックされていません、1：ロックされています |

## RegionConf

リージョン情報

次のインターフェースに引用されます：DescribeProductInfo。

| 名称 | タイプ |  説明 |
|------|------|-------|
| RegionId | String | リージョンID |
| RegionName | String | リージョン名 |
| RegionShortName | String | リージョン略称 |
| Area | String | リージョンがあるエリア名 |
| ZoneSet | Array of [ZoneCapacityConf](#ZoneCapacityConf) | アベイラビリティゾーン情報 |

## TradeDealDetail

発注トランザクション情報

次のインターフェースに引用されます：DescribeInstanceDealDetail。

| 名称 | タイプ |  説明 |
|------|------|-------|
| DealId | String | 発注番号IDは、クラウドAPI呼び出し時にこのIDを使用 |
| DealName | String | 長期発注ID は、発注の問題を公式カスタマーサービスが使用するこの ID にフィードバックします |
| ZoneId | Integer | アベイラビリティゾーンid |
| GoodsNum | Integer | 発注関連のインスタンス数 |
| Creater | String | ユーザーuinの作成 |
| CreatTime | String | 発注作成時間 |
| OverdueTime | String | 発注タイムアウト時間 |
| EndTime | String | 発注完了時間 |
| Status | Integer | 発注ステータス 1：未払い 2:支払い済み、未発送 3:発送中 4:発送成功 5:発送失敗 6:返金済み 7:発注クローズ済み 8:発注期限切れ 9:発注失効 10:製品失効 11:立て替え拒否 12:支払い中 |
| Description | String | 発注ステータスの説明 |
| Price | Integer | 発注の実際の総額。単位：ポイント |
| InstanceIds | Array of String | インスタンスID |

## ZoneCapacityConf

アベイラビリティゾーン内の製品情報

次のインターフェースに引用されます：DescribeProductInfo。

| 名称 | タイプ |  説明 |
|------|------|-------|
| ZoneId | String | ap-guangzhou-3 などのアベイラビリティゾーンID |
| ZoneName | String | アベイラビリティゾーン名 |
| IsSaleout | Boolean | アベイラビリティゾーンが完売しているか |
| IsDefault | Boolean | デフォルトのアベイラビリティゾーンか否か |
| NetWorkType | Array of String | ネットワークタイプ：basenet -- 基本ネットワーク、vpcnet -- VPCネットワーク |
| ProductSet | Array of [ProductConf](#ProductConf) | アベイラビリティゾーン内の製品仕様などの情報 |
| OldZoneId | Integer | 100003などのアベイラビリティゾーンID |


