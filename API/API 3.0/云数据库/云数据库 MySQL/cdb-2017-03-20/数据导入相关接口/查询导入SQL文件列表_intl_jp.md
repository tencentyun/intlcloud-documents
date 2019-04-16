## 1. API説明

APIリクエストドメイン名： cdb.tencentcloudapi.com 。

このAPI（DescribeUploadedFiles）はユーザーインポートのSQLファイルリストの照合に使用されます。

## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/236/15833)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：DescribeUploadedFiles |
| Version | はい | String | 共通パラメータ、該当APIの値：2017/03/20 |
| Region | いいえ | String | 共通パラメータ。このAPIはこのパラメータを渡す必要がありません。 |
| Path | はい | String | ファイルパス。このフィールドにはユーザーのメインアカウントのOwnerUin情報を入力します。 |
| Offset | いいえ | Integer | オフセットを記録し、デフォルト値は0。 |
| Limit | いいえ | Integer | 単回リクエストが返された数量。デフォルト値は20。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| TotalCount | Integer | 照合条件を満たすSQLファイル総数。|
| Items | Array of [SqlFileInfo](/document/api/236/15878#SqlFileInfo) | 返されたSQLファイルリスト。|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 インポートSQLファイルリストの照合

#### 入力例

```
https://cdb.tencentcloudapi.com/?Action=DescribeUploadedFiles
&Path=100000983328
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "TotalCount":1,
        "Items":[
            {
                "UploadTime":"2016-11-28 15:16:13",
                "UploadInfo":{
                    "AllSliceNum":5,
                    "CompleteNum":3
                },
                "FileName":"joellwang.sql",
                "FileSize":8581633,
                "IsUploadFinished":0,
                "FileId":"5596d7433fe211da4b487228db4e7c57",
                "Access_url": "http://xxxxxx-xxxxxxx.file.myqcloud.com:8080/100000983328/task.sql"
            }
        ]        
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeUploadedFiles)

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
| InternalError.CosError | ファイル情報取得失敗。 |
| InvalidParameter | パラメータエラー。 |

