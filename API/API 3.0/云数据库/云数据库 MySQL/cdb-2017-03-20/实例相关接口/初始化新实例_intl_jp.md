## 1. API説明

APIリクエストドメイン名： cdb.tencentcloudapi.com 。

このAPI（InitDBInstances）はデータベースインスタンス（パスワード、デフォルトの文字セット、インスタンスポート番号など）を初期化するために使用されます

デフォルトのAPIリクエスト頻度制限：100回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：cdb.ap-shanghai-fsi.tencentcloudapi.com 。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/236/15833)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：InitDBInstances |
| Version | はい | String | 共通パラメータ、該当APIの値：2017/03/20 |
| Region | はい | String | 共通パラメータ。詳細について製品がサポートする[地域リスト](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| InstanceIds.N | はい | Array of String | インスタンスID。フォーマット：cdb-c1nl9rpv。データベースコンソールページで表示されるインスタンスIDと同じ。[インスタンスリストの照合](https://cloud.tencent.com/document/api/236/15872) APIで取得できます。その値は出力パラメータのフィールドInstanceIdの値です。 |
| NewPassword | はい | String | インスタンスの新しいパスワード。パスワードルール：8～64文字で、少なくともアルファベット、数字と文字（対応文字：!@#$%^*()）の2種類を含む必要があります。 |
| Parameters.N | はい | Array of [ParamInfo](/document/api/236/15878#ParamInfo) | インスタンスのパラメータリスト。現時点で「character_set_server」、「lower_case_table_names」パラメータを設定することをサポートします。その中、「character_set_server」パラメータの選択可能な値は["utf8","latin1","gbk","utf8mb4"]です。「lower_case_table_names」の選択可能な値は[“0”,“1”]です。 |
| Vport | いいえ | Integer | インスタンスのポート。数値範囲は[1024, 65535] |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| AsyncRequestIds | Array of String | 非同期タスクのリクエストID配列。このIDで非同期タスクの実行結果を照合できます|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 新しいインスタンスの初期化

#### 入力例

```
https://cdb.tencentcloudapi.com/?Action=InitDBInstances
&InstanceIds.0=cdb-f35wr6wj
&NewPassword=Gx18ux23F^X
&Parameters.0.name=lower_case_table_names
&Parameters.0.value=1
&Parameters.1.name=character_set_server
&Parameters.1.value=utf8
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "AsyncRequestIds":[
            "8cd119d4-61ba-11e7-aeff-018cfa1f5560"
        ]
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=InitDBInstances)

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

