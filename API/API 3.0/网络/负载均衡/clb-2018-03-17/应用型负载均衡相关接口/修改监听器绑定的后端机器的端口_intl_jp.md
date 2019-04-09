## 1. API説明

APIリクエストドメイン名：clb.tencentcloudapi.com。

ModifyTargetPort APIは、リスナーにバインディングされているバックエンドCVMのポートを変更するために使用されます。
このAPIは非同期APIであり、APIの返し動作が完了した後、返されたRequestIDを入力パラメータとする必要があり、DescribeTaskStatus APIを呼び出して今回のタスクが成功したか照合します。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互通信できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例：clb.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/214/30670)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：ModifyTargetPort |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-03-17 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/214/30670#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| LoadBalancerId | はい | String | ロードバランサーインスタンスID |
| ListenerId | はい | String | CLBリスナーID |
| Targets.N | はい | Array of [Target](/document/api/214/30694#Target) | ポートを変更するRSリスト |
| NewPort | はい | Integer | RSがリスナーにバインディングされる新しいポート |
| LocationId | いいえ | String | 転送規則ID |
| Domain | いいえ | String | ターゲット規則のドメイン名であり、LocationIdパラメータを提供する時、このパラメータは有効になりません |
| Url | いいえ | String | ターゲット規則のURLであり、LocationIdパラメータを提供する時、このパラメータは有効になりません |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 バックエンドでバインディングされるCVMのポートの変更

リスナーlbl-d1ubsydqに登録されているCVM ins-dm4xtz0iのポートを元の233から334に変更します

#### 入力例

```
https://clb.tencentcloudapi.com/?Action=ModifyTargetPort
&LoadBalancerId=lb-cuxw2rm0
&ListenerId=lbl-d1ubsydq
&Targets.0.InstanceId=ins-dm4xtz0i
&Targets.0.Port=233
&NewPort=334
&<共通リクエストパラメータ>
```

#####　出力例

```
{
    "Response": {
        "RequestId": "a2764f3c-f173-421c-8e42-7b1e7a608ffd"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールはオンライン呼び出し、署名の検証、SDKコード生成と高速検索APIなどの機能を提供し、クラウドAPI使用の難易度を大幅に低減することができるため、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=clb&Version=2018-03-17&Action=ModifyTargetPort)

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

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](/document/api/214/30673#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| FailedOperation | 操作失敗 |
| InternalError | 内部エラー |
| InvalidParameter | パラメータエラー。 |
| InvalidParameterValue | パラメータ値エラー |
| UnauthorizedOperation | 操作が承認されていません |

