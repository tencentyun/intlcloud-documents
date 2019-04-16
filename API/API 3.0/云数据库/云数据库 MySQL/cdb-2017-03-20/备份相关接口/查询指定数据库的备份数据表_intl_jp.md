## 1. API説明

APIリクエストドメイン名： cdb.tencentcloudapi.com 。

このAPI（DescribeBackupTables）は指定したデータベースのバックアップデータテーブル名を照合するために使用されます。

デフォルトのAPIリクエスト頻度制限：100回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：cdb.ap-shanghai-fsi.tencentcloudapi.com 。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/236/15833)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：DescribeBackupTables |
| Version | はい | String | 共通パラメータ、該当APIの値：2017/03/20 |
| Region | はい | String | 共通パラメータ。詳細について製品がサポートする[地域リスト](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| InstanceId | はい | String | インスタンスID。フォーマット：cdb-c1nl9rpv。データベースページコンソールページで表示されるインスタンスIDと同じ |
| StartTime | はい | String | 開始時間。フォーマット：2017-07-12 10:29:20。 |
| DatabaseName | はい | String | 指定したデータベース名。 |
| SearchTable | いいえ | String | 照合するデータテーブル名の接頭辞。 |
| Offset | いいえ | Integer | ページングのオフセット。 |
| Limit | いいえ | Integer | ページングのサイズ。最小値は1、最大値は2000。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| TotalCount | Integer | 返されたデータ数。|
| Items | Array of [TableName](/document/api/236/15878#TableName) | 条件を満たすデータテーブル配列。|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 指定したデータベースのバックアップデータテーブルの照合

#### 入力例

```
https://cdb.tencentcloudapi.com/?Action=DescribeBackupTables
&InstanceId=cdb-c1nl9rpv
&StartTime=2017-07-12 10:29:20
&DatabaseName=mysql
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "TotalCount":"28",
        "Items":[
            {
                "TableName":"general_log"
            },
            {
                "TableName":"slow_log"
            },
            {
                "TableName":"columns_priv"
            },
            {
                "TableName":"db"
            },
            {
                "TableName":"event"
            },
            {
                "TableName":"func"
            },
            {
                "TableName":"help_category"
            },
            {
                "TableName":"help_keyword"
            },
            {
                "TableName":"help_relation"
            },
            {
                "TableName":"help_topic"
            },
            {
                "TableName":"innodb_index_stats"
            },
            {
                "TableName":"innodb_table_stats"
            },
            {
                "TableName":"ndb_binlog_index"
            },
            {
                "TableName":"plugin"
            },
            {
                "TableName":"proc"
            },
            {
                "TableName":"procs_priv"
            },
            {
                "TableName":"proxies_priv"
            },
            {
                "TableName":"servers"
            },
            {
                "TableName":"slave_master_info"
            },
            {
                "TableName":"slave_relay_log_info"
            },
            {
                "TableName":"slave_worker_info"
            },
            {
                "TableName":"tables_priv"
            },
            {
                "TableName":"time_zone"
            },
            {
                "TableName":"time_zone_leap_second"
            },
            {
                "TableName":"time_zone_name"
            },
            {
                "TableName":"time_zone_transition"
            },
            {
                "TableName":"time_zone_transition_type"
            },
            {
                "TableName":"user"
            }
        ]
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeBackupTables)

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
| InternalError.DatabaseAccessError | データベース内部エラー。 |
| InvalidParameter | パラメータエラー。 |
| InvalidParameter.InstanceNotFound | インスタンスが存在しません。 |

