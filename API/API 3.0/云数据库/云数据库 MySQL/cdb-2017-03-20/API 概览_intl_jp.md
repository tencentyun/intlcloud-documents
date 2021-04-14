## タスク関連API

| API名 | API機能 |
|---------|---------|
| [DescribeAsyncRequestInfo](https://cloud.tencent.com/document/api/236/20410) | 非同期タスクの実行結果の照合 |
| [DescribeTasks](https://cloud.tencent.com/document/api/236/15848) | データベースインスタンスタスクリストの照合 |

## パラメータ関連API

| API名 | API機能 |
|---------|---------|
| [CreateParamTemplate](https://cloud.tencent.com/document/api/236/32663) | パラメータテンプレートの作成 |
| [DeleteParamTemplate](https://cloud.tencent.com/document/api/236/32824) | パラメータテンプレートの削除 |
| [DescribeDefaultParams](https://cloud.tencent.com/document/api/236/32662) | デフォルトの設定可能なパラメータリストの照合 |
| [DescribeInstanceParamRecords](https://cloud.tencent.com/document/api/236/32661) | インスタンスパラメータ変更履歴の照合 |
| [DescribeInstanceParams](https://cloud.tencent.com/document/api/236/20411) | インスタンスの設定可能なパラメータリストの照合 |
| [DescribeParamTemplateInfo](https://cloud.tencent.com/document/api/236/32660) | パラメータテンプレート詳細の照合 |
| [DescribeParamTemplates](https://cloud.tencent.com/document/api/236/32659) | パラメータテンプレートリストの照合 |
| [ModifyInstanceParam](https://cloud.tencent.com/document/api/236/15860) | インスタンスパラメータの変更 |
| [ModifyParamTemplate](https://cloud.tencent.com/document/api/236/32658) | パラメータテンプレートの変更 |

## ロールバック関連API

| API名 | API機能 |
|---------|---------|
| [DescribeRollbackRangeTime](https://cloud.tencent.com/document/api/236/18726) | ロールバック可能な時間の照合 |
| [StartBatchRollback](https://cloud.tencent.com/document/api/236/18725) | ロールバックデータベーステーブル |

## バックアップ関連API

| API名 | API機能 |
|---------|---------|
| [CreateBackup](https://cloud.tencent.com/document/api/236/15844) | データベースバックアップの作成 |
| [DeleteBackup](https://cloud.tencent.com/document/api/236/15841) | データベースバックアップの削除 |
| [DescribeBackupConfig](https://cloud.tencent.com/document/api/236/15837) | データベースバックアップ構成情報の照合 |
| [DescribeBackupDatabases](https://cloud.tencent.com/document/api/236/15840) | バックアップデータベースリストの照合 |
| [DescribeBackupTables](https://cloud.tencent.com/document/api/236/15846) | 指定したデータベースのバックアップデータテーブルの照合 |
| [DescribeBackups](https://cloud.tencent.com/document/api/236/15842) | バックアップログの照合 |
| [DescribeBinlogs](https://cloud.tencent.com/document/api/236/15843) | 2進数ログの照合 |
| [DescribeSlowLogs](https://cloud.tencent.com/document/api/236/15845) | スロークエリログの照合 |
| [ModifyBackupConfig](https://cloud.tencent.com/document/api/236/15839) | データベースバックアップ構成の変更 |

## セキュリティグループ関連API

| API名 | API機能 |
|---------|---------|
| [AssociateSecurityGroups](https://cloud.tencent.com/document/api/236/15852) | セキュリティグループへのクラウドリソースの一括バインディング |
| [DescribeDBSecurityGroups](https://cloud.tencent.com/document/api/236/15854) | インスタンスセキュリティグループ情報の照合 |
| [DescribeProjectSecurityGroups](https://cloud.tencent.com/document/api/236/15850) | プロジェクトセキュリティグループ情報の照合 |
| [DisassociateSecurityGroups](https://cloud.tencent.com/document/api/236/15851) | セキュリティグループのクラウドリソースの一括バインディング解除 |
| [ModifyDBInstanceSecurityGroups](https://cloud.tencent.com/document/api/236/15853) | データベースセキュリティグループの変更 |

## インスタンス関連API

| API名 | API機能 |
|---------|---------|
| [CloseWanService](https://cloud.tencent.com/document/api/236/15863) | インスタンスのパブリックネットワークアクセスの無効化 |
| [CreateDBInstance](https://cloud.tencent.com/document/api/236/15871) | データベースインスタンス（年額/月額）の作成 |
| [CreateDBInstanceHour](https://cloud.tencent.com/document/api/236/15865) | データベースインスタンス（従量制課金）の作成 |
| [DescribeDBInstanceCharset](https://cloud.tencent.com/document/api/236/15866) | データベースインスタンスの文字セットの照合 |
| [DescribeDBInstanceConfig](https://cloud.tencent.com/document/api/236/17491) | データベースインスタンス構成情報の照合 |
| [DescribeDBInstanceGTID](https://cloud.tencent.com/document/api/236/15862) | クラウドデータインスタンスのGTIDの有効化状態の照合 |
| [DescribeDBInstanceRebootTime](https://cloud.tencent.com/document/api/236/15874) | データベースインスタンスの再起動予定時間の照合 |
| [DescribeDBInstances](https://cloud.tencent.com/document/api/236/15872) | インスタンスリストの照合 |
| [DescribeDBPrice](https://cloud.tencent.com/document/api/236/18566) | データベース価格の照合 |
| [DescribeDBSwitchRecords](https://cloud.tencent.com/document/api/236/17490) | データベース切り替え記録の照合 |
| [DescribeDBZoneConfig](https://cloud.tencent.com/document/api/236/17229) | データベースの販売可能な仕様の取得 |
| [DescribeTagsOfInstanceIds](https://cloud.tencent.com/document/api/236/32666) | インスタンスにバインディングされるタグの取得 |
| [InitDBInstances](https://cloud.tencent.com/document/api/236/15873) | 新しいインスタンスの初期化 |
| [InquiryPriceUpgradeInstances](https://cloud.tencent.com/document/api/236/32665) | データベースアップグレード価格の照合 |
| [IsolateDBInstance](https://cloud.tencent.com/document/api/236/15869) | データベースインスタンスの隔離 |
| [ModifyAutoRenewFlag](https://cloud.tencent.com/document/api/236/19652) | データベースインスタンスの自動更新フラグの変更 |
| [ModifyDBInstanceName](https://cloud.tencent.com/document/api/236/15877) | データベースインスタンス名の変更 |
| [ModifyDBInstanceProject](https://cloud.tencent.com/document/api/236/15868) | データベースインスタンスの所属プロジェクトの変更 |
| [ModifyDBInstanceVipVport](https://cloud.tencent.com/document/api/236/15867) | データベースインスタンスのIPとポート番号の変更 |
| [ModifyInstanceTag](https://cloud.tencent.com/document/api/236/32664) | インスタンスタグの変更 |
| [OpenDBInstanceGTID](https://cloud.tencent.com/document/api/236/17489) | インスタンスのGTIDの有効化 |
| [OpenWanService](https://cloud.tencent.com/document/api/236/15875) | インスタンスのパブリックネットワークアクセスの有効化 |
| [RenewDBInstance](https://cloud.tencent.com/document/api/236/30160) | データベースインスタンスの更新 |
| [RestartDBInstances](https://cloud.tencent.com/document/api/236/17488) | インスタンスの再起動 |
| [SwitchForUpgrade](https://cloud.tencent.com/document/api/236/15864) | 新しいインスタンスへのアクセス切り替え |
| [UpgradeDBInstance](https://cloud.tencent.com/document/api/236/15876) | データベースインスタンスのアップグレード |
| [UpgradeDBInstanceEngineVersion](https://cloud.tencent.com/document/api/236/15870) | インスタンスバージョンのアップグレード |

## データインポート関連API

| API名 | API機能 |
|---------|---------|
| [CreateDBImportJob](https://cloud.tencent.com/document/api/236/15858) | データインポートタスクの作成 |
| [DescribeDBImportRecords](https://cloud.tencent.com/document/api/236/15856) | データベースインポートタスク記録の照合 |
| [DescribeUploadedFiles](https://cloud.tencent.com/document/api/236/30161) | インポートSQLファイルリストの照合 |
| [StopDBImportJob](https://cloud.tencent.com/document/api/236/15857) | データインポートタスクの終了 |

## データベース関連API

| API名 | API機能 |
|---------|---------|
| [DescribeDatabases](https://cloud.tencent.com/document/api/236/17493) | データベースの照合 |
| [DescribeTables](https://cloud.tencent.com/document/api/236/18727) | データベーステーブルの照合 |

## 監視関連API

| API名 | API機能 |
|---------|---------|
| [DescribeDeviceMonitorInfo](https://cloud.tencent.com/document/api/236/32668) | 物理サーバー監視情報 |

## アカウント関連API

| API名 | API機能 |
|---------|---------|
| [CreateAccounts](https://cloud.tencent.com/document/api/236/17502) | データベースアカウントの作成 |
| [DeleteAccounts](https://cloud.tencent.com/document/api/236/17501) | データベースアカウントの削除 |
| [DescribeAccountPrivileges](https://cloud.tencent.com/document/api/236/17500) | データベースアカウント権限情報の照合 |
| [DescribeAccounts](https://cloud.tencent.com/document/api/236/17499) | データベースのすべてのアカウント情報の照合 |
| [DescribeSupportedPrivileges](https://cloud.tencent.com/document/api/236/32825) | データベースインスタンスがサポートする権限情報の照合 |
| [ModifyAccountDescription](https://cloud.tencent.com/document/api/236/17498) | データベースインスタンスアカウントの備考情報の変更 |
| [ModifyAccountPassword](https://cloud.tencent.com/document/api/236/17497) | データベースインスタンスアカウントのパスワードの変更 |
| [ModifyAccountPrivileges](https://cloud.tencent.com/document/api/236/17496) | データベースインスタンスアカウントの権限の変更 |
| [VerifyRootAccount](https://cloud.tencent.com/document/api/236/17495) | rootアカウント権限の検証 |


