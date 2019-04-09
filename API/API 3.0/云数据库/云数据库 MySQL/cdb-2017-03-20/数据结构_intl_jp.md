## Account

データベースアカウント情報

次のAPIによって参照されます：CreateAccounts、DeleteAccounts、ModifyAccountDescription、ModifyAccountPassword、ModifyAccountPrivileges。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| User | String | はい | 新アカウントの名称 |
| Host | String | はい | 新アカウントのドメイン名 |

## AccountInfo

アカウント詳細情報

次のAPIによって参照されます：DescribeAccounts。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Notes | String | アカウント備考情報 |
| Host | String | アカウントのドメイン名 |
| User | String | アカウントの名称 |
| ModifyTime | Timestamp | アカウント情報変更時間 |
| ModifyPasswordTime | Timestamp | パスワードの変更時間 |
| CreateTime | Timestamp | アカウントの作成時間 |

## BackupConfig

ECDBの第2スレーブデータベースの構成情報。このフィールドはECDBインスタンスにのみ使用可能です

次のAPIによって参照されます：DescribeDBInstanceConfig。

| 名称 | タイプ |  説明 |
|------|------|-------|
| ReplicationMode | String | 第2スレーブデータベースのレプリケーション方式。可能な戻り値：async-非同期、semisync-準同期 |
| Zone | String | 第2スレーブデータベースAvailability Zoneの正式名称。例えば、ap-shanghai-1 |
| Vip | String | 第2スレーブデータベースのプライベートネットワークIPアドレス |
| Vport | String | 第2スレーブデータベースアクセスポート |

## BackupInfo

バックアップ詳細情報

次のAPIによって参照されます：DescribeBackups。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Name | String | バックアップファイル名 |
| Size | Integer | バックアップファイルのサイズ。単位：Byte |
| Date | String | バックアップのスナップショット時間。時間フォーマット：2016-03-17 02:10:37 |
| IntranetUrl | String | プライベートネットワークのダウンロードアドレス |
| InternetUrl | String | パブリックネットワークのダウンロードアドレス |
| Type | String | ログの具体的なタイプ。可能な値：logic - 論理コールドバックアップ、physical - 物理コールドバックアップ |
| BackupId | Integer | バックアップサブタスクのID。バックアップファイルを削除するときに使用されます |
| Status | String | バックアップタスクステータス |
| FinishTime | String | バックアップタスクの完了時間 |
| Creator | String | バックアップの作成者。可能な値：SYSTEM - システム作成、Uin - 送信者Uin値 |

## BinlogInfo

2進数ログ情報

次のAPIによって参照されます：DescribeBinlogs。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Name | String | バックアップファイル名 |
| Size | Integer | バックアップファイルのサイズ。単位：Byte |
| Date | Timestamp | バックアップのスナップショット時間。時間フォーマット：2016-03-17 02:10:37 |
| IntranetUrl | String | プライベートネットワークのダウンロードアドレス |
| InternetUrl | String | パブリックネットワークのダウンロードアドレス |
| Type | String | ログの具体的なタイプ。可能な値：binlog - 2進数ログ |

## ColumnPrivilege

列権限情報

次のAPIによって参照されます：DescribeAccountPrivileges、ModifyAccountPrivileges。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| Database | String | はい | データベース名 |
| Table | String | はい | データベーステーブル名 |
| Column | String | はい | データベース列名 |
| Privileges | Array of String | はい | 権限情報 |

## DBSwitchInfo

データベース切り替え記録

次のAPIによって参照されます：DescribeDBSwitchRecords。

| 名称 | タイプ |  説明 |
|------|------|-------|
| SwitchTime | Timestamp | 切り替え時間。フォーマット：2017-09-03 01:34:31 |
| SwitchType | String | 切り替えタイプ。可能な戻り値：TRANSFER - データ移行、MASTER2SLAVE - マスタースレーブ切り替え、RECOVERY - マスタースレーブ回復 |

## DatabaseName

データベーステーブル名

次のAPIによって参照されます：DescribeBackupDatabases。

| 名称 | タイプ |  説明 |
|------|------|-------|
| DatabaseName | String | データベーステーブル名 |

## DatabasePrivilege

データベース権限

次のAPIによって参照されます：DescribeAccountPrivileges、ModifyAccountPrivileges。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| Privileges | Array of String | はい | 権限情報 |
| Database | String | はい | データベース名 |

## DeviceCpuInfo

 CPU負荷

次のAPIによって参照されます：DescribeDeviceMonitorInfo。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Rate | Array of [DeviceCpuRateInfo](#DeviceCpuRateInfo) | インスタンスのCPU平均使用率 |
| Load | Array of Integer | インスタンスCPUの監視データ |

## DeviceCpuRateInfo

インスタンスのCPU平均使用率

次のAPIによって参照されます：DescribeDeviceMonitorInfo。

| 名称 | タイプ |  説明 |
|------|------|-------|
| CpuCore | Integer | Cpuのコア番号 |
| Rate | Array of Integer | Cpu使用率 |

## DeviceDiskInfo

インスタンスディスクの監視データ

次のAPIによって参照されます：DescribeDeviceMonitorInfo。

| 名称 | タイプ |  説明 |
|------|------|-------|
| IoRatioPerSec | Array of Integer | 1秒あたりのIO操作時間の割合 |
| IoWaitTime | Array of Integer | 1回デバイスI/O操作の待ち時間*100。単位はミリ秒。例えば：この値は201の場合、1回I/O操作の待ち時間：201/100=2.1ミリ秒 |
| Read | Array of Integer | ディスクの1秒間に完了する読み取り操作回数の和*100。例えば：この値は2002の場合、ディスクの1秒間に完了する読み取り操作：2002/100=20.2回 |
| Write | Array of Integer | ディスクの1秒間に完了する書き込み操作回数の和*100。例えば：この値は30001の場合、ディスクの1秒間に完了する書き込み操作：30001/100=300.01回 |

## DeviceMemInfo

インスタンスの所属物理サーバーのメモリ監視情報

次のAPIによって参照されます：DescribeDeviceMonitorInfo。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Total | Array of Integer | メモリの合計サイズ。freeコマンドのMem：1行totalの値、単位：KB |
| Used | Array of Integer | 使用済みのメモリ。freeコマンドのMem：1行usedの値、単位：KB |

## DeviceNetInfo

インスタンスの所属物理サーバーのネットワーク監視情報

次のAPIによって参照されます：DescribeDeviceMonitorInfo。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Conn | Array of Integer | TCP接続数 |
| PackageIn | Array of Integer | ENIインバウンドパケット数 |
| PackageOut | Array of Integer | ENIアウトバウンドパケット数 |
| FlowIn | Array of Integer | インバウンドトラフィック。単位：KB |
| FlowOut | Array of Integer | アウトバウンドトラフィック。単位：KB |

## DrInfo

ディザスタリカバリインスタンス情報

次のAPIによって参照されます：DescribeDBInstances。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Status | Integer | ディザスタリカバリインスタンスステータス |
| Zone | String | Availability Zone情報 |
| InstanceId | String | インスタンスID |
| Region | String | 地域情報 |
| SyncStatus | Integer | インスタンス同期ステータス |
| InstanceName | String | インスタンス名称 |
| InstanceType | Integer | インスタンスタイプ |

## ImportRecord

インポートタスク記録

次のAPIによって参照されます：DescribeDBImportRecords。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Status | Integer | 状態値 |
| Code | Integer | 状態値 |
| CostTime | Integer | 実行時間 |
| InstanceId | String | インスタンスID |
| WorkId | String | バックエンドタスクID |
| FileName | String | インポートファイル名 |
| Process | Integer | 実行進捗 |
| CreateTime | Timestamp | タスク作成時間 |
| FileSize | String | ファイルのサイズ |
| Message | String | タスク実行情報 |
| JobId | Integer | タスクID |
| DbName | String | インポートデータベーステーブル名 |
| AsyncRequestId | String | 非同期タスクのリクエストID |

## Inbound

セキュリティグループのインバウンド規則

次のAPIによって参照されます：DescribeDBSecurityGroups、DescribeProjectSecurityGroups。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Action | String | ポリシー。ACCEPTまたはDROP |
| CidrIp | String | ソースIPまたはIPアドレス範囲。例えば192.168.0.0/16 |
| PortRange | String | ポート |
| IpProtocol | String | ネットワークプロトコル。UDP、TCPなどに対応します |
| Dir | String | 規則によって限定される方向。インバウンド規則はINPUT |

## InstanceInfo

インスタンス詳細情報

次のAPIによって参照されます：DescribeDBInstances。

| 名称 | タイプ |  説明 |
|------|------|-------|
| WanStatus | Integer | パブリックネットワークのステータス。可能な戻り値：0-パブリックネットワーク未開通、1-パブリックネットワーク開通中、2-パブリックネットワークが無効になっています |
| Zone | String | Availability Zone情報 |
| InitFlag | Integer | 初期化フラグ。可能な戻り値：0-未初期化、1-初期化済 |
| RoVipInfo | [RoVipInfo](#RoVipInfo) | 読み取り専用vip情報。このフィールドは読み取り専用インスタンスアクセスのみを開通する読み取り専用インスタンスにのみ使用可能です |
| Memory | Integer | メモリ容量。単位はMB |
| Status | Integer | インスタンスステータス。可能な戻り値：0-作成中、1-実行中、4-隔離中、5-隔離済 |
| VpcId | Integer | VPC ID。例えば：51102 |
| SlaveInfo | [SlaveInfo](#SlaveInfo) | スレーブ情報 |
| InstanceId | String | インスタンスID |
| Volume | Integer | ディスク容量。単位はGB |
| AutoRenew | Integer | 自動更新フラグ。可能な戻り値：0-自動更新未開通、1-自動更新開通済、2-自動更新が無効になっています |
| ProtectMode | Integer | データレプリケーション方式 |
| RoGroups | Array of [RoGroup](#RoGroup) | 読み取り専用グループ詳細情報 |
| SubnetId | Integer | サブネットID。例えば：2333 |
| InstanceType | Integer | インスタンスタイプ。可能な戻り値：1-マスタインスタンス、2-ディザスタリカバリインスタンス、3-読み取り専用インスタンス |
| ProjectId | Integer | プロジェクトID |
| Region | String | 地域情報 |
| DeadlineTime | Timestamp | インスタンス期限切れ時間 |
| DeployMode | Integer | Availability Zone配置方式 |
| TaskStatus | Integer | インスタンスタスクステータス |
| MasterInfo | [MasterInfo](#MasterInfo) | マスタインスタンス詳細情報 |
| DeviceType | String | インスタンスタイプ。可能な戻り値：「HA」-高可用性バージョン、「BASIC」-基本バージョン |
| EngineVersion | String | カーネルバージョン |
| InstanceName | String | インスタンス名称 |
| DrInfo | Array of [DrInfo](#DrInfo) | ディザスタリカバリインスタンス詳細情報 |
| WanDomain | String | パブリックネットワークドメイン名 |
| WanPort | Integer | パブリックネットワークのポート番号 |
| PayType | Integer | 支払タイプ。可能な戻り値：0-年額/月額、1-従量制課金 |
| CreateTime | String | インスタンス作成時間 |
| Vip | String | インスタンスIP |
| Vport | Integer | ポート番号 |
| CdbError | Integer | ロックフラグであるかどうか |
| UniqVpcId | String | VPC記述子。例えば：“vpc-5v8wn9mg” |
| UniqSubnetId | String | サブネット記述子。例えば：“subnet-1typ0s7d” |
| PhysicalId | String | 物理ID |
| Cpu | Integer | コア数 |
| Qps | Integer | 1秒あたりの照合数量 |
| ZoneName | String | Availability Zone中国語名称 |

## InstanceRebootTime

インスタンスの再起動予定時間

次のAPIによって参照されます：DescribeDBInstanceRebootTime。

| 名称 | タイプ |  説明 |
|------|------|-------|
| InstanceId | String | インスタンスID。フォーマット：cdb-c1nl9rpv。データベースコンソールページで表示されるインスタンスIDと同じ |
| TimeInSeconds | Integer | 再起動予定時間 |

## InstanceRollbackRangeTime

インスタンスのロールバック可能な時間範囲

次のAPIによって参照されます：DescribeRollbackRangeTime。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Code | Integer | データベースエラーコードの照合 |
| Message | String | データベースエラー情報の照合 |
| InstanceId | String | インスタンスIDリスト。単一インスタンスIDのフォーマット：cdb-c1nl9rpv。データベースコンソールページで表示されるインスタンスIDと同じ |
| Times | Array of [RollbackTimeRange](#RollbackTimeRange) | ロールバック可能な時間範囲 |

## MasterInfo

マスタインスタンス情報

次のAPIによって参照されます：DescribeDBInstances。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Region | String | 地域情報 |
| RegionId | Integer | 地域ID |
| ZoneId | Integer | Availability Zone ID |
| Zone | String | Availability Zone情報 |
| InstanceId | String | インスタンスID |
| ResourceId | String | インスタンス長さID |
| Status | Integer | インスタンスステータス |
| InstanceName | String | インスタンス名称 |
| InstanceType | Integer | インスタンスタイプ |
| TaskStatus | Integer | タスクステータス |
| Memory | Integer | メモリ容量 |
| Volume | Integer | ディスク容量 |
| DeviceType | String | インスタンスモデル |
| Qps | Integer | 1秒あたりの照合数 |
| VpcId | Integer | VPC ID |
| SubnetId | Integer | サブネットID |
| ExClusterId | String | 専有クラスタID |
| ExClusterName | String | 専有クラスタ名称 |

## Outbound

セキュリティグループのアウトバウンド規則

次のAPIによって参照されます：DescribeDBSecurityGroups、DescribeProjectSecurityGroups。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Action | String | ポリシー。ACCEPTまたはDROP |
| CidrIp | String | 宛先IPまたはIPアドレス範囲。例えば、172.16.0.0/12 |
| PortRange | String | ポートまたはポート範囲 |
| IpProtocol | String | ネットワークプロトコル。UDP、TCPなどに対応します |
| Dir | String | 規則によって限定された方向。インバウンド規則はOUTPUT |

## ParamInfo

インスタンスパラメータ情報

次のAPIによって参照されます：CreateDBInstance、CreateDBInstanceHour、InitDBInstances。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| Name | String | はい | パラメータ名 |
| Value | String | はい | パラメータ値 |

## ParamRecord

パラメータ変更記録

次のAPIによって参照されます：DescribeInstanceParamRecords。

| 名称 | タイプ |  説明 |
|------|------|-------|
| InstanceId | String | インスタンスID |
| ParamName | String | パラメータ名称 |
| OldValue | String | パラメータ変更前の値 |
| NewValue | String | パラメータ変更後の値 |
| IsSucess | Boolean | パラメータが変更成功するかどうか |
| ModifyTime | String | 変更時間 |

## ParamTemplateInfo

パラメータテンプレート情報

次のAPIによって参照されます：DescribeParamTemplates。

| 名称 | タイプ |  説明 |
|------|------|-------|
| TemplateId | Integer | パラメータテンプレートID |
| Name | String | パラメータテンプレート名称 |
| Description | String | パラメータテンプレートの説明 |
| EngineVersion | String | インスタンスエンジンバージョン |

## Parameter

データベースインスタンスパラメータ

次のAPIによって参照されます：CreateParamTemplate、ModifyInstanceParam、ModifyParamTemplate。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| Name | String | はい | パラメータ名称 |
| CurrentValue | String | はい | パラメータ値 |

## ParameterDetail

インスタンスパラメータの詳細説明

次のAPIによって参照されます：DescribeDefaultParams、DescribeInstanceParams、DescribeParamTemplateInfo。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Name | String | パラメータ名称 |
| ParamType | String | パラメータタイプ |
| Default | String | パラメータのデフォルト値 |
| Description | String | パラメータの説明 |
| CurrentValue | String | パラメータの現在値 |
| NeedReboot | Integer | パラメータ変更後、パラメータを有効にするにはデータベースを再起動する必要があるかどうか。可能な値：0-再起動不要、1-再起動必要 |
| Max | Integer | パラメータの最大許容値 |
| Min | Integer | パラメータの最小許容値 |
| EnumValue | Array of String | パラメータの選択可能な列挙値。非列挙パラメータの場合、空となります |

## RegionSellConf

地域販売設定

次のAPIによって参照されます：DescribeDBZoneConfig。

| 名称 | タイプ |  説明 |
|------|------|-------|
| RegionName | String | 地域の日本語名称 |
| Area | String | 所属区 |
| IsDefaultRegion | Integer | デフォルト地域であるかどうか |
| Region | String | 地域名称 |
| ZonesConf | Array of [ZoneSellConf](#ZoneSellConf) | Availability Zone販売構成 |

## RoGroup

読み取り専用グループパラメータ

次のAPIによって参照されます：CreateDBInstance、CreateDBInstanceHour、DescribeDBInstances。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| RoGroupMode | String | はい | 読み取り専用グループモード。選択可能な値：alone-読み取り専用グループのシステム自動割り当て、allinone-読み取り専用グループの新規作成、join-既存の読み取り専用グループの使用 |
| RoGroupId | String | いいえ | 読み取り専用グループID |
| RoGroupName | String | いいえ | 読み取り専用グループ名称 |
| RoOfflineDelay | Integer | いいえ | 遅延制限超過除去機能をオンにするかどうか。この機能をオンにした後、読み取り専用インスタンスとマスタインスタンスの遅延が遅延しきい値を超えると、読み取り専用インスタンスが隔離されます。選択可能な値：1-オンにする；0-オフにする |
| RoMaxDelayTime | Integer | いいえ | 遅延しきい値 |
| MinRoInGroup | Integer | いいえ | インスタンスの最小保留数。読み取り専用インスタンスの購入数が設定数より小さい場合、除去しません |
| WeightMode | String | いいえ | 読み書き重み付け割り当てモード。選択可能な値：system-システム自動割り当て、custom-カスタマイズ |
| Weight | Integer | いいえ | 重み値 |
| RoInstances | Array of [RoInstanceInfo](#RoInstanceInfo) | いいえ | 読み取り専用グループの読み取り専用インスタンスの詳細 |
| Vip | String | いいえ | 読み取り専用グループのプライベートネットワークIP |
| Vport | Integer | いいえ | 読み取り専用グループのプライベートネットワークポート番号 |

## RoInstanceInfo

ROインスタンスの詳細情報

次のAPIによって参照されます：CreateDBInstance、CreateDBInstanceHour、DescribeDBInstances。

| 名称 | タイプ |  説明 |
|------|------|-------|
| MasterInstanceId | String | ROグループが対応するマスタインスタンスのID |
| RoStatus | String | ROインスタンスのROグループ内でのステータス。可能な値：online-オンライン、offline-オフライン |
| OfflineTime | String | ROインスタンスのROグループ内での前回オフライン時間 |
| Weight | Integer | ROインスタンスのROグループ内での重み付け |
| Region | String | ROインスタンスの所属エリアの名称。例えば、ap-shanghai |
| Zone | String | RO Availability Zoneの正式名称。例えば、ap-shanghai-1 |
| InstanceId | String | ROインスタンスID。フォーマット：cdbro-c1nl9rpv |
| Status | Integer | ROインスタンスステータス。可能な戻り値：0-作成中、1-実行中、4-削除中 |
| InstanceType | Integer | インスタンスタイプ。可能な戻り値：1-マスタインスタンス、2-ディザスタリカバリインスタンス、3-読み取り専用インスタンス |
| InstanceName | String | ROインスタンス名 |
| HourFeeStatus | Integer | 従量制課金ステータス。可能な数値：1-正常、2-料金滞納 |
| TaskStatus | Integer | ROインスタンスタスクのステータス。可能な戻り値：<br>0-タスクなし<br>1-アップグレード中<br>2-データインポート中<br>3-スレーブ開放中<br>4-パブリックネットワークアクセスアクセスオン<br>5-一括操作実行中<br>6-ロールバック中<br>7-パブリックネットワークアクセスオフ<br>8-パスワード変更中<br>9-インスタンス名変更中<br>10-再起動中<br>12-自作移行中<br>13-データベーステーブル削除中<br>14-ディザスタリカバリインスタンスインスタンス作成同期中 |
| Memory | Integer | ROインスタンスメモリのサイズ。単位：MB |
| Volume | Integer | ROインスタンスディスクのサイズ。単位：GB |
| Qps | Integer | 1回あたりの照合数量 |
| Vip | String | ROインスタンスのプライベートネットワークIPアドレス |
| Vport | Integer | ROインスタンスのアクセスポート |
| VpcId | Integer | ROインスタンスのVPC ID |
| SubnetId | Integer | ROインスタンスのVPCサブネットID |
| DeviceType | String | ROインスタンス仕様説明。現時点の数値 CUSTOM |
| EngineVersion | String | ROインスタンスデータベースエンジンバージョン。可能戻り値：5.1、5.5、5.6と5.7 |
| DeadlineTime | String | ROインスタンス期限切れ時間。時間フォーマット：yyyy-mm-dd hh:mm:ss。インスタンスは従量制課金モードの場合、このフィールド値は0000-00-00 00:00:00 |
| PayType | Integer | ROインスタンス課金タイプ。可能な戻り値：0-年額月/額、1-従量制課金、2-後払い月末締め |

## RoVipInfo

読み取り専用vip情報

次のAPIによって参照されます：DescribeDBInstances。

| 名称 | タイプ |  説明 |
|------|------|-------|
| RoVipStatus | Integer | 読み取り専用vipステータス |
| RoSubnetId | Integer | 読み取り専用vipのサブネット |
| RoVpcId | Integer | 読み取り専用vipのVPC |
| RoVport | Integer | 読み取り専用vipのポート番号 |
| RoVip | String | 読み取り専用vip |

## RollbackDBName

ロールバック用データベース名

次のAPIによって参照されます：StartBatchRollback。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| DatabaseName | String | はい | ロールバック前の元のデータベース名 |
| NewDatabaseName | String | はい | ロールバック後の新データベース名 |

## RollbackInstancesInfo

ロールバック用インスタンス詳細

次のAPIによって参照されます：StartBatchRollback。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| InstanceId | String | はい | データベースインスタンスID |
| Strategy | String | はい | ロールバックポリシー。選択可能な値：table、db、full。デフォルト値はfull。table - 急速ロールバックモードで、選択したテーブルレベルのバックアップとbinlogのみをインポートします。テーブル間の操作があり、且つ関連テーブルが同時に選択されていない場合、ロールバックの失敗につながります。このモード下でのパラメータDatabasesは空でなければなりません。db - 快速モードで、選択したデータベースレベルのバックアップとbinlogのみをインポートします。データベース間の操作があり、且つ関連データベースが同時に選択されていない場合、ロールバックの失敗につながります。full - 普通ロールバックモードで、インスタンス全体のバックアップとbinlogをインポートします。速度が低い。 |
| RollbackTime | String | はい | データベースのロールバック時間。時間フォーマット：yyyy-mm-dd hh:mm:ss |
| Databases | Array of [RollbackDBName](#RollbackDBName) | いいえ | ロールバック待ちのデータベース情報。データベース全体のロールバックを示します |
| Tables | Array of [RollbackTables](#RollbackTables) | いいえ | ロールバック待ちのデータベーステーブル情報。テーブルごとのロールバックを示します |

## RollbackTableName

ロールバック用データベーステーブル名

次のAPIによって参照されます：StartBatchRollback。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| TableName | String | はい | ロールバック前の元のデータベーステーブル名 |
| NewTableName | String | はい | ロールバック後の新データベーステーブル名 |

## RollbackTables

ロールバック用データベーステーブル詳細

次のAPIによって参照されます：StartBatchRollback。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| Database | String | はい | データベース名 |
| Table | Array of [RollbackTableName](#RollbackTableName) | はい | データベーステーブル詳細 |

## RollbackTimeRange

ロールバック可能な時間範囲

次のAPIによって参照されます：DescribeRollbackRangeTime。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Begin | String | インスタンスのロールバック可能な開始時間。時間フォーマット：2016-10-29 01:06:04 |
| End | String | インスタンスのロールバック可能な終了時間。時間フォーマット：2016-11-02 11:44:47 |

## SecurityGroup

セキュリティグループ詳細

次のAPIによって参照されます：DescribeDBSecurityGroups、DescribeProjectSecurityGroups。

| 名称 | タイプ |  説明 |
|------|------|-------|
| ProjectId | Integer | プロジェクトID |
| CreateTime | String | 作成時間。時間フォーマット：yyyy-mm-dd hh:mm:ss |
| Inbound | Array of [Inbound](#Inbound) | インバウンド規則 |
| Outbound | Array of [Outbound](#Outbound) | アウトバウンド規則 |
| SecurityGroupId | String | セキュリティグループID |
| SecurityGroupName | String | セキュリティグループ名称 |
| SecurityGroupRemark | String | セキュリティグループ備考 |

## SellConfig

販売構成詳細

次のAPIによって参照されます：DescribeDBZoneConfig。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Device | String | デバイスタイプ |
| Type | String | 販売仕様の説明 |
| CdbType | String | インスタンスタイプ |
| Memory | Integer | メモリのサイズ。単位はMB |
| Cpu | Integer | CPUコア数 |
| VolumeMin | Integer | ディスク最小仕様。単位はGB |
| VolumeMax | Integer | ディスク最大仕様。単位はGB |
| VolumeStep | Integer | ディスクのステップサイズ。単位はGB |
| Connection | Integer | リンク数 |
| Qps | Integer | 1秒あたりの照合数量 |
| Iops | Integer | 1秒あたりのIO数 |
| Info | String | 適用シナリオの説明 |
| Status | Integer | 状態値 |

## SellType

販売インスタンスタイプ

次のAPIによって参照されます：DescribeDBZoneConfig。

| 名称 | タイプ |  説明 |
|------|------|-------|
| TypeName | String | 販売インスタンス名称 |
| EngineVersion | Array of String | カーネルバージョン番号 |
| Configs | Array of [SellConfig](#SellConfig) | 販売仕様詳細構成 |

## SlaveConfig

スレーブデータベースの構成情報

次のAPIによって参照されます：DescribeDBInstanceConfig。

| 名称 | タイプ |  説明 |
|------|------|-------|
| ReplicationMode | String | スレーブデータベースレプリケーション方式。可能な戻り値：aysnc-非同期、semisync-準同期 |
| Zone | String | スレーブデータベースAvailability Zoneの正式名称。例えば、ap-shanghai-1 |

## SlaveInfo

スレーブ情報

次のAPIによって参照されます：DescribeDBInstances。

| 名称 | タイプ |  説明 |
|------|------|-------|
| First | [SlaveInstanceInfo](#SlaveInstanceInfo) | 第1スレーブ情報 |
| Second | [SlaveInstanceInfo](#SlaveInstanceInfo) | 第2スレーブ情報 |

## SlaveInstanceInfo

スレーブ情報

次のAPIによって参照されます：DescribeDBInstances。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Vport | Integer | ポート番号 |
| Region | String | 地域情報 |
| Vip | String | 仮想IP情報 |
| Zone | String | Availability Zone情報 |

## SlowLogInfo

スロークエリログ詳細の照合

次のAPIによって参照されます：DescribeSlowLogs。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Name | String | バックアップファイル名 |
| Size | Integer | バックアップファイルのサイズ。単位：Byte |
| Date | Timestamp | バックアップのスナップショット時間。時間フォーマット：2016-03-17 02:10:37 |
| IntranetUrl | String | プライベートネットワークのダウンロードアドレス |
| InternetUrl | String | パブリックネットワークのダウンロードアドレス |
| Type | String | ログの具体的なタイプ。可能な値：slowlog - スローログ |

## SqlFileInfo

sqlファイル情報

次のAPIによって参照されます：DescribeUploadedFiles。

| 名称 | タイプ |  説明 |
|------|------|-------|
| UploadTime | Timestamp | アップロード時間 |
| UploadInfo | [UploadInfo](#UploadInfo) | アップロード進捗 |
| FileName | String | ファイル名 |
| FileSize | Integer | ファイルのサイズ。単位はBytes |
| IsUploadFinished | Integer | アップロードが完了したかどうかを示すフラグ。選択可能な値：0 - 未完了、1 - 完了 |
| FileId | String | ファイルID |

## TableName

テーブル名

次のAPIによって参照されます：DescribeBackupTables。

| 名称 | タイプ |  説明 |
|------|------|-------|
| TableName | String | テーブル名 |

## TablePrivilege

データベーステーブル権限

次のAPIによって参照されます：DescribeAccountPrivileges、ModifyAccountPrivileges。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| Database | String | はい | データベース名 |
| Table | String | はい | データベーステーブル名 |
| Privileges | Array of String | はい | 権限情報 |

## TagInfo

タグ情報

次のAPIによって参照されます：CreateDBInstance、CreateDBInstanceHour、ModifyInstanceTag。

| 名称 | タイプ |  説明 |
|------|------|-------|
| TagKey | String | タグキー |
| TagValue | Array of String | タグ値 |

## TagInfoUnit

タグ情報ユニット

次のAPIによって参照されます：DescribeTagsOfInstanceIds。

| 名称 | タイプ |  説明 |
|------|------|-------|
| TagKey | String | タグキー |
| TagValue | String | タグ値 |

## TagsInfoOfInstance

インスタンスのタグ情報

次のAPIによって参照されます：DescribeTagsOfInstanceIds。

| 名称 | タイプ |  説明 |
|------|------|-------|
| InstanceId | String | インスタンスID |
| Tags | Array of [TagInfoUnit](#TagInfoUnit) | タグ情報 |

## UploadInfo

ファイルアップロードの説明

次のAPIによって参照されます：DescribeUploadedFiles。

| 名称 | タイプ |  説明 |
|------|------|-------|
| AllSliceNum | Integer | ファイルのすべてのシャード数 |
| CompleteNum | Integer | 完了したシャード数 |

## ZoneConf

複数のAvailability Zone情報

次のAPIによって参照されます：DescribeDBZoneConfig。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| DeployMode | Array of Integer | はい | Availability Zone配置方式。可能な値：0-単一Availability Zone、1-複数Availability Zone |
| MasterZone | Array of String | はい | マスタインスタンス所属のAvailability Zone |
| SlaveZone | Array of String | はい | インスタンスは複数のAvailability Zone配置の場合、スタンバイデータベース1所属のAvailability Zone |
| BackupZone | Array of String | はい | インスタンスは複数のAvailability Zone配置の場合、スタンバイデータベース2所属のAvailability Zone |

## ZoneSellConf

Availability Zone販売構成

次のAPIによって参照されます：DescribeDBZoneConfig。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Status | Integer | Availability Zoneステータス。可能な戻り値：0-非オンライン、1-オンライン、2-開放、3-販売停止、4-非表示 |
| ZoneName | String | Availability Zone中国語名称 |
| IsCustom | Boolean | インスタンスタイプがカスタムタイプであるかどうか |
| IsSupportDr | Boolean | ディザスタリカバリインスタンス対応の有無 |
| IsSupportVpc | Boolean | VPC対応の有無 |
| HourInstanceSaleMaxNum | Integer | 時間別課金インスタンスの最大販売数量 |
| IsDefaultZone | Boolean | デフォルトのAvailability Zoneであるかどうか |
| IsBm | Boolean | BM区であるかどうか |
| PayType | Array of String | サポートする支払タイプ。可能な戻り値：0-年額/月額、1-時間別課金、2-後払い |
| ProtectMode | Array of String | データレプリケーションタイプ。0-非同期レプリケーション、1-準同期レプリケーション、2-強同期レプリケーション |
| Zone | String | Availability Zone名称 |
| SellType | Array of [SellType](#SellType) | 販売インスタンスタイプ配列 |
| ZoneConf | [ZoneConf](#ZoneConf) | 複数のAvailability Zone情報 |


