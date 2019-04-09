## 1. API説明

APIリクエストドメイン名： cdb.tencentcloudapi.com 。

このAPI（ModifyDBInstanceVipVport）はデータベースインスタンスのIPとポート番号の変更、基本ネットワークからVPCネットワークへの転換やVPCネットワークのサブネットの変更に使用されます。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：cdb.ap-shanghai-fsi.tencentcloudapi.com 。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/236/15833)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：ModifyDBInstanceVipVport |
| Version | はい | String | 共通パラメータ、該当APIの値：2017/03/20 |
| Region | はい | String | 共通パラメータ。詳細について製品がサポートする[地域リスト](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| InstanceId | はい | String | インスタンスID。フォーマット：cdb-c1nl9rpv。データベースコンソールページで表示されるインスタンスIDと同じ。[インスタンスリストの照合](https://cloud.tencent.com/document/api/236/15872) APIで取得できます。その値は出力パラメータのフィールドInstanceIdの値です。 |
| DstIp | いいえ | String | 目標IP。このパラメータとDstPortパラメータのどちらかを渡す必要があります。 |
| DstPort | いいえ | Integer | 目標ポート。対応範囲：[1024-65535]。このパラメータとDstIpパラメータのどちらかを渡す必要があります。 |
| UniqVpcId | いいえ | String | VPCの統一ID。 |
| UniqSubnetId | いいえ | String | サブネットの統一ID。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| AsyncRequestId | String | 非同期タスクID。|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 データベースインスタンスのIPとポート番号の変更

#### 入力例

```
https://cdb.tencentcloudapi.com/?Action=ModifyDBInstanceVipVport
&InstanceId=cdb-f35wr6wj
&DstIp=10.0.1.1
&DstPort=1025
&VpcId=11357
&SubnetId=23789
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "AsyncRequestId":"d2baf2fb-cbae62df-7dd0d736-9cbd3e31"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=ModifyDBInstanceVipVport)

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
| FailedOperation.StatusConflict | タスク状態競合。 |
| InvalidParameter | パラメータエラー。 |

