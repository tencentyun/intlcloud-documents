## 1. API説明

APIリクエストドメイン名： cdb.tencentcloudapi.com 。

このAPI（DescribeTasks）はデータベースインスタンスタスクリストを照合するために使用されます。

デフォルトのAPIリクエスト頻度制限：100回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：cdb.ap-shanghai-fsi.tencentcloudapi.com 。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/236/15833)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ。このAPIの値：DescribeTasks |
| Version | はい | String | 共通パラメータ、該当APIの値：2017/03/20 |
| Region | はい | String | 共通パラメータ。詳細について製品がサポートする[地域リスト](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| InstanceId | いいえ | String | インスタンスID。フォーマット：cdb-c1nl9rpv。データベースコンソールページで表示されるインスタンスIDと同じ。[インスタンスリストの照合](https://cloud.tencent.com/document/api/236/15872) APIで取得できます。その値は出力パラメータのフィールドInstanceIdの値です |
| AsyncRequestId | いいえ | String | 非同期タスクリクエストID。クラウドデータベースの関連操作を実行することによって返されたAsyncRequestId |
| TaskTypes.N | いいえ | Array of Integer | タスクタイプ。値を渡さないとすべてのタスクタイプを照合します。可能な値：1-データベースロールバック、2-SQL操作、3-データインポート、5-パラメータ設定、6-初期化、7-再起動、8-GTIDの有効化、9-読み取り専用インスタンスのアップグレード、10-データベースの一括ロールバック、11-プライマリインスタンスのアップグレード、12-データベーステーブルの削除、13-マスタリインスタンスへの切り替え |
| TaskStatus.N | いいえ | Array of Integer | タスクステータス。値を渡さないとすべてのタスクステータスを照合します。可能な値：-1-未定義、0-初期化、1-動作中、2-実行成功、3-実行失敗、4-終了済、5-削除済、6-一時停止中。 |
| StartTimeBegin | いいえ | String | 最初タスクの開始時間。範囲照合のために使用されます。時間フォーマット：2017-12-31 10:40:01 |
| StartTimeEnd | いいえ | String | 最終タスクの開始時間。範囲照合のために使用されます。時間フォーマット：2017-12-31 10:40:01 |
| Offset | いいえ | Integer | オフセットを記録する。デフォルト値は0 |
| Limit | いいえ | Integer | 単回リクエストによって返された数量。デフォルト値は20、最大値は100 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| TotalCount | Integer | 照合条件を満たすインスタンス総数|
| Items | Array of String | 返されたインスタンスタスク情報|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 データベースインスタンスタスクリストの照合

#### 入力例

```
https://cdb.tencentcloudapi.com/?Action=DescribeTasks
&InstanceIds.0=cdb-eb2w7dto
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "TotalCount":13,
        "Items":[
            {
                "Status":2,
                "Code":0,
                "Data":[
                    {
                        "InstanceId":"cdb-gt70m8aa",
                        "Character_set_server":"utf8",
                        "Lower_case_table_names":"0",
                        "Vport":3306
                    }
                ],
                "JobId":15964,
                "StartTime":"2017-06-27 15:05:33",
                "Progress":100,
                "Message":"インスタンス初期化成功",
                "EndTime":"2017-06-27 15:06:36",
                "Type":6
            },
            {
                "Status":3,
                "Code":-5003,
                "Data":[
                    {
                        "Code":3,
                        "InstanceId":"cdb-atjl8gns",
                        "StartTime":"2017-07-21 17:19:30",
                        "Databases":[
                            {
                                "Message":"dial tcp :0: connection refused",
                                "Code":3,
                                "Database":"clear_test"
                            }
                        ],
                        "Message":"dial tcp :0: connection refused",
                        "EndTime":"2017-07-21 17:19:31"
                    }
                ],
                "JobId":51788,
                "StartTime":"2017-07-21 17:19:30",
                "Progress":0,
                "Message":"",
                "EndTime":"2017-07-21 17:19:31",
                "Type":2
            },
            {
                "Status":2,
                "Code":0,
                "Data":[
                    {
                        "InstanceId":"cdb-gt70m8aa",
                        "Before":{
                            "SlaveZoneFirst":160002,
                            "MasterZone":160002,
                            "Memory":1000,
                            "DeployMode":"",
                            "Volume":50,
                            "ProtectMode":"",
                            "SlaveZoneSecond":"",
                            "EngineVersion":"5.6",
                            "CdbType":"CUSTOM"
                        },
                        "After":{
                            "SlaveZoneFirst":160002,
                            "MasterZone":160002,
                            "Memory":2000,
                            "DeployMode":"",
                            "Volume":100,
                            "ProtectMode":"",
                            "SlaveZoneSecond":"",
                            "EngineVersion":"5.6",
                            "CdbType":"CUSTOM"
                        },
                        "DealName":"20170627160000060843141595228010"
                    }
                ],
                "JobId":15967,
                "StartTime":"2017-06-27 15:13:52",
                "Progress":100,
                "Message":"インスタンスアップグレードタスク完了",
                "EndTime":"2017-06-27 15:16:57",
                "Type":11
            },
            {
                "Status":2,
                "Code":0,
                "Data":[
                    {
                        "InstanceId":"",
                        "Parameters":[
                            {
                                "Message":"ok",
                                "Code":0,
                                "Name":"back_log",
                                "OldValue":"210",
                                "CurrentValue":"2"
                            }
                        ]
                    }
                ],
                "JobId":15969,
                "StartTime":"2017-06-27 16:33:40",
                "Progress":100,
                "Message":"パラメータ設定成功",
                "EndTime":"2017-06-27 16:34:25",
                "Type":5
            },
            {
                "Status":3,
                "Code":3,
                "Data":[
                    {
                        "InstanceId":"",
                        "Database":"test",
                        "CostTime":0,
                        "FileSize":"12",
                        "FileName":"skyler.sql"
                    }
                ],
                "JobId":15970,
                "StartTime":"2017-06-27 16:46:52",
                "Progress":5,
                "Message":"Warning: Using a password on the command line interface can be insecure.?ERROR 1064 (42000) at line 1: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'joell=skyler' at line 1?dumper err?",
                "EndTime":"2017-06-27 16:47:23",
                "Type":3
            },
            {
                "Status":3,
                "Code":3,
                "Data":[
                    {
                        "InstanceId":"",
                        "Database":"test",
                        "CostTime":0,
                        "FileSize":"5857113",
                        "FileName":"joellwang_1_4.sql"
                    }
                ],
                "JobId":15971,
                "StartTime":"2017-06-27 16:49:13",
                "Progress":5,
                "Message":"Warning: Using a password on the command line interface can be insecure.?ERROR 2006 (HY000) at line 1: MySQL server has gone away?dumper err?",
                "EndTime":"2017-06-27 16:49:44",
                "Type":3
            },
            {
                "Status":2,
                "Code":0,
                "Data":[
                    {
                        "InstanceId":"",
                        "Database":"test",
                        "CostTime":19,
                        "FileSize":"28384",
                        "FileName":"LearningSQLExample.sql"
                    }
                ],
                "JobId":15972,
                "StartTime":"2017-06-27 17:02:29",
                "Progress":100,
                "Message":"success",
                "EndTime":"2017-06-27 17:03:00",
                "Type":3
            },
            {
                "Status":2,
                "Code":0,
                "Data":[
                    {
                        "InstanceId":"cdb-o8cacfkg",
                        "Before":{
                            "SlaveZoneFirst":160002,
                            "MasterZone":160002,
                            "Memory":8000,
                            "DeployMode":"",
                            "Volume":50,
                            "ProtectMode":"",
                            "SlaveZoneSecond":"",
                            "EngineVersion":"5.6",
                            "CdbType":"CUSTOM"
                        },
                        "After":{
                            "SlaveZoneFirst":160002,
                            "MasterZone":160002,
                            "Memory":8000,
                            "DeployMode":"",
                            "Volume":100,
                            "ProtectMode":"",
                            "SlaveZoneSecond":"",
                            "EngineVersion":"5.6",
                            "CdbType":"CUSTOM"
                        },
                        "DealName":"20170627160000060849699827143219"
                    }
                ],
                "JobId":15974,
                "StartTime":"2017-06-27 18:04:19",
                "Progress":100,
                "Message":"インスタンスアップグレードタスク完了",
                "EndTime":"2017-06-27 18:08:25",
                "Type":11
            },
            {
                "Status":2,
                "Code":0,
                "Data":[
                    {
                        "InstanceId":"cdb-7262qp3q",
                        "Character_set_server":"utf8",
                        "Lower_case_table_names":"0",
                        "Vport":3306
                    }
                ],
                "JobId":15976,
                "StartTime":"2017-06-27 19:18:31",
                "Progress":100,
                "Message":"インスタンス初期化成功",
                "EndTime":"2017-06-27 19:19:34",
                "Type":6
            },
            {
                "Status":2,
                "Code":0,
                "Data":[
                    {
                        "Status":2,
                        "Code":0,
                        "InstanceId":"cdb-ewgjla5w",
                        "Databases":[
                            {
                                "DatabaseName":"test",
                                "NewDatabaseName":"test_bak"
                            }
                        ],
                        "Progress":100,
                        "Message":"ロールバック成功",
                        "RollbackTime":"2017-04-06 16:00:00",
                        "DatabaseTables":[
                            {
                                "Tables":[
                                    {
                                        "TableName":"monitor_alarm",
                                        "NewTableName":"monitor_alarm_bak_1"
                                    }
                                ],
                                "Database":"monitor_master"
                            }
                        ]
                    }
                ],
                "JobId":51695,
                "StartTime":"2017-04-06 20:42:59",
                "Progress":100,
                "Message":"インスタンスロールバック全部成功",
                "EndTime":"2017-04-06 20:45:03",
                "Type":10
            }
        ]
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeTasks)

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
| OperationDenied | 操作不能です。 |
| OperationDenied.WrongStatus | バックエンドタスクのステータスが不正です。 |

