
リソース級権限とは、ユーザーが操作を実行するリソースを指定することができる能力を指します。CDBは一部、リソース級権限をサポートし、即ちリソース級権限をサポートしたCDBの操作について、ユーザーが操作を実行できるタイミング、又はユーザーが特定のリソースを使用できるタイミングを制御することができることを示しています。Cloud Access Management（CAM）で認証できるリソースタイプは以下のとおりです。

| リソース種類 | 許可ポリシーのリソース記述方法 |
| :-------- |:-------------- |
| CDBインスタンス関連 |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`

以下の表では、現在リソース級権限をサポートしているCDBのAPI操作、及び各操作がサポートするリソースと条件キーを紹介します。リソースパスを指定する時、パスに*ワイルドカードを使用することができます。

## リソースレベルでの承認をサポートするAPIリスト
| API操作 | リソースパス |
|:---------|:-------------|
| AddTimeWindow| `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| AssociateSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| CloseWanService|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| CreateAccounts|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| CreateBackup|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| CreateDBImportJob|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DeleteAccounts|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DeleteBackup|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DeleteTimeWindow|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeAccountPrivileges|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeAccounts|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBackupConfig|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBackupDatabases|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBackupDownloadDbTableCode|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBackups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBackupTables|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBinlogs|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDatabases|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBImportRecords|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBInstanceCharset|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBInstanceConfig|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBInstanceGTID|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBInstanceRebootTime|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBSwitchRecords|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeInstanceParamRecords|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeInstanceParams|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeRoGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeRollbackRangeTime|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeSlowLogs|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeSupportedPrivileges|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeTables|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeTimeWindow|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDatabasesForInstances |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeMonitorData |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeTableColumns |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DropDatabaseTables|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| InitDBInstances|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| IsolateDBInstance|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyAccountDescription|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyAccountPassword|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyAccountPrivileges|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyAutoRenewFlag|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyBackupConfig|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyBackupInfo|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyDBInstanceName|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyDBInstanceProject|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyDBInstanceSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyDBInstanceVipVport|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyInstanceParam|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyDBInstanceModes|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyTimeWindow|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyProtectMode |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| OfflineDBInstances |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| OpenDBInstanceGTID|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| OpenWanService|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ReleaseIsolatedDBInstances|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| RestartDBInstances|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| StartBatchRollback|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| SubmitBatchOperation|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| SwitchDrInstanceToMaster|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| SwitchForUpgrade|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DisassociateSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| UpgradeDBInstance|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| UpgradeDBInstanceEngineVersion|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 

## リソースレベルでの承認をサポートしないAPIリスト
リソース権限をサポートしないCDBのAPI操作について、ユーザーにこの操作を使用する権限を付与することができますが、ポリシーのステートメントのリソース要素は*に指定しなければなりません。

| API操作                       | API記述                      |
| ----------------------------- | ---------------------------- |
| CreateDBInstance              | TencentDBインスタンスを作成します（年額月額） |
| CreateDBInstanceHour          | CDBインスタンス（従量課金）の作成 |
| CreateParamTemplate           | パラメーターテンプレートの作成                 |
| DeleteParamTemplate           | 監視テンプレート監視項目の削除           |
| DescribeProjectSecurityGroups | プロジェクトのセキュリティグループ情報の照合           |
| DescribeDefaultParams         | デフォルトの設定可能なパラメータリストの照合     |
| DescribeParamTemplateInfo     | パラメータテンプレート詳細の照合             |
| DescribeParamTemplates        | パラメータテンプレートリストの照合             |
| DescribeAsyncRequestInfo      | 非同期タスクの実行結果の照合       |
| DescribeTasks                 | CDBインスタンスタスクリストの照合     |
| DescribeUploadedFiles         | インポートSQLファイルリストの照合          |
| ModifyParamTemplate           | パラメータテンプレートの変更                 |
| RenewDBInstance               | CDBインスタンスの更新             |
| StopDBImportJob               | データインポートタスクの終了             |
| DescribleRoMinScale           | 読み取り専用インスタンスでサポートされる最小仕様を取得します          |
| DescribeRequestResult           | タスクの詳細を取得します       |
| DescribeRoMinScale           | 読み取り専用インスタンスの購入またはアップグレードの最小仕様を取得します          |

