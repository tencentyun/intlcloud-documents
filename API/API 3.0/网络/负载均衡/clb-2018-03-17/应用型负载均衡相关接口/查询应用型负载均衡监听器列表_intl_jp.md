## 1. API説明

APIリクエストドメイン名：clb.tencentcloudapi.com。

DescribeListeners APIはCLB装置IDに基づき、リスナーのプロトコルまたはポートをフィルタリング条件としてリスナーリストを取得することができます。全くフィルタリング条件を指定しない場合、このCLB装置下のデフォルトのデータ長（20個）のリスナーをデフォルトで返します。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互通信できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例：clb.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/214/30670)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：DescribeListeners |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-03-17 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/214/30670#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| LoadBalancerId | はい | String | ロードバランサーインスタンスID |
| ListenerIds.N | いいえ | Array of String | 照合するアプリケーション型CLBリスナーID配列 |
| Protocol | いいえ | String | 照合するリスナーのプロトコルタイプであり、値：TCP &#124; UDP &#124; HTTP &#124; HTTPS &#124; TCP_SSL |
| Port | いいえ | Integer | 照合するリスナーのポート |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| Listeners | Array of [Listener](/document/api/214/30694#Listener) | リスナーリスト|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 ロードバランサーインスタンスのすべてのリスナー情報の照合

#### 入力例

```
https://clb.tencentcloudapi.com/?Action=DescribeListeners
&LoadBalancerId=lb-1wvl0ejw
&<共通リクエストパラメータ>
```

#####　出力例

```
{
    "Response": {
        "Listeners": [
            {
                "ListenerId": "lbl-7gogrzv2",
                "Protocol": "HTTPS",
                "Port": 1111,
                "HealthCheck": null,
                "Certificate": null,
                "Scheduler": null,
                "SessionExpireTime": null,
                "SniSwitch": 1,
                "Rules": [
                    {
                        "LocationId": "loc-8s90r6oc",
                        "Domain": "clue.foo2",
                        "Url": "/aa1",
                        "SessionExpireTime": 0,
                        "HealthCheck": {
                            "HealthSwitch": 0,
                            "TimeOut": 2,
                            "IntervalTime": 5,
                            "HealthNum": 3,
                            "UnHealthNum": 3,
                            "HttpCode": 31,
                            "HttpCheckPath": "/",
                            "HttpCheckDomain": "clue.foo",
                            "HttpCheckMethod": "head"
                        },
                        "Certificate": {
                            "SSLMode": "UNIDIRECTIONAL",
                            "CertId": "McKgYApY",
                            "CertCaId": ""
                        },
                        "Scheduler": "WRR"
                    }
                ]
            }
        ],
        "RequestId": "e571614d-c674-4dd8-9f00-4ba0f322d1c1"
    }
}
```

### 例2 ポート、プロトコルおよびリスナーIDに基づくリスナーの照合

#### 入力例

```
https://clb.tencentcloudapi.com/?Action=DescribeListeners
&LoadBalancerId=lb-1wvl0ejw
&Protocol=TCP
&Port=2007
&ListenerIds.0=lbl-ohamxrok
&<共通リクエストパラメータ>
```

#####　出力例

```
{
    "Response": {
        "Listeners": [
            {
                "ListenerId": "lbl-ohamxrok",
                "Protocol": "TCP",
                "Port": 2007,
                "HealthCheck": {
                    "HealthSwitch": 1,
                    "TimeOut": 2,
                    "IntervalTime": 5,
                    "HealthNum": 3,
                    "UnHealthNum": 3,
                    "HttpCode": null,
                    "HttpCheckPath": null,
                    "HttpCheckDomain": null,
                    "HttpCheckMethod": null
                },
                "Certificate": null,
                "Scheduler": "WRR",
                "SessionExpireTime": 0,
                "SniSwitch": 0,
                "Rules": null
            }
        ],
        "RequestId": "7371485a-fa7a-48c0-b733-fa8b0fdb1a72"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールはオンライン呼び出し、署名の検証、SDKコード生成と高速検索APIなどの機能を提供し、クラウドAPI使用の難易度を大幅に低減することができるため、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=clb&Version=2018-03-17&Action=DescribeListeners)

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

