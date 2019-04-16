## 1. API説明

APIリクエストドメイン名： cdb.tencentcloudapi.com 。

このAPI（DescribeDBImportRecords）はデータベースインポートタスク操作ログの照合に使用されます。

デフォルトのAPIリクエスト頻度制限：100回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：cdb.ap-shanghai-fsi.tencentcloudapi.com 。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/236/15833)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：DescribeDBImportRecords |
| Version | はい | String | 共通パラメータ、該当APIの値：2017/03/20 |
| Region | はい | String | 共通パラメータ。詳細について製品がサポートする[地域リスト](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| InstanceId | はい | String | インスタンスID、フォーマット：cdb-c1nl9rpv、データベースコンソールページに表示するインスタンスIDと同じです。 |
| StartTime | いいえ | String | 開始時間、時間フォーマットの例：2016-01-01 00:00:01。 |
| EndTime | いいえ | String | 終了時間、時間フォーマットの例：2016-01-01 23:59:59。 |
| Offset | いいえ | Integer | ページングパラメータ、オフセット、デフォルト値は0。 |
| Limit | いいえ | Integer | ページングパラメータ、単回リクエストが返された数量、デフォルト値は20、最小値は1、最大値は100。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| TotalCount | Integer | 照合条件を満たすインポートタスク操作ログ総数。|
| Items | Array of [ImportRecord](/document/api/236/15878#ImportRecord) | 返されたインポート操作記録リスト。|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 データベースインポートタスク記録の照合

#### 入力例

```
https://cdb.tencentcloudapi.com/?Action=DescribeDBImportRecords
&InstanceId=cdb-7r8h0h61
&StartTime=2016-01-01 00:00:01
&EndTime=2017-08-24 15:03:01
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "TotalCount":"4",
        "Items":[
            {
                "Status":3,
                "Code":1,
                "CostTime":0,
                "InstanceId":"e318ecb8-863f-11e7-85a5-80fb06afab26",
                "WorkId":"1649290",
                "FileName":"monkey_1501490864.sql",
                "Process":5,
                "CreateTime":"2017-11-09 14:26:31",
                "FileSize":12,
                "Message":"lock_inst.cgi: 一部のインスタンスidに対応するインスタンス記録が存在しない",
                "JobId":16242,
                "DbName":"test",
                "AsyncRequestId":"a4788d0a-df23758a-ac961e5a-af414d33"
            },
            {
                "Status":3,
                "Code":1,
                "CostTime":0,
                "InstanceId":"e318ecb8-863f-11e7-85a5-80fb06afab26",
                "WorkId":"1545387",
                "FileName":"monkey_1501490864.sql",
                "Process":5,
                "CreateTime":"2017-10-18 21:18:26",
                "FileSize":"12",
                "Message":"lock_inst.cgi: 一部のインスタンスidに対応するインスタンス記録が存在しない",
                "JobId":16223,
                "DbName":"",
                "AsyncRequestId":"198e97de-972b1971-fb0ce76a-08ca054e"
            },
            {
                "Status":3,
                "Code":1,
                "CostTime":0,
                "InstanceId":"e318ecb8-863f-11e7-85a5-80fb06afab26",
                "WorkId":"1545171",
                "FileName":"monkey_1501490864.sql",
                "Process":5,
                "CreateTime":"2017-10-18 20:12:07",
                "FileSize":"2",
                "Message":"lock_inst.cgi: 一部のインスタンスidに対応するインスタンス記録が存在しない",
                "JobId":16222,
                "DbName":"test",
                "AsyncRequestId":"9706dfbf-0d1bc6df-5f18f4e1-bb86f2f4"
            },
            {
                "Status":3,
                "Code":1,
                "CostTime":0,
                "InstanceId":"e318ecb8-863f-11e7-85a5-80fb06afab26",
                "WorkId":"2228867",
                "FileName":"monkey_1501490864.sql",
                "Process":5,
                "CreateTime":"2017-10-18 17:53:54",
                "FileSize":"12",
                "Message":"lock_inst.cgi: 一部のインスタンスidに対応するインスタンス記録が存在しない",
                "JobId":16209,
                "DbName":"",
                "AsyncRequestId":"e8713d1e-10628d32-74682eef-d0855c1a"
            }
        ]
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeDBImportRecords)

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
| InvalidParameter | パラメータエラー。 |
| InvalidParameter.InstanceNotFound | インスタンスが存在しません。 |
| InvalidParameter.InvalidAsyncRequestId | 非同期タスクが存在しません。 |

