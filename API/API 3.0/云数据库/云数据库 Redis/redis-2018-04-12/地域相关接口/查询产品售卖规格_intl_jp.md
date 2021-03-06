## 1. インターフェースについて

インターフェースのリクエストドメイン名：redis.tencentcloudapi.com 。

本インターフェースは、指定されたアベイラビリティゾーンとインスタンスタイプにおける Redis の販売仕様を照会します。ユーザーが購入ホワイトリストにない場合、このアベイラビリティゾーンまたはこのタイプの販売仕様の詳細を照会することはできません。特定の地域のホワイトリストの購入を申請すると、作業指示を送信できます

初期設定の状態では、インターフェースのリクエスト頻度は20回/秒に制限されています。

注意：このインターフェースは、金融エリアのリージョンに対応しています。金融エリアとそれ以外のエリアは隔てられているため、相互運用ができません。そのため、共通パラメータの Region が金融エリアのリージョン（ap-shanghai-fsi など）である場合、同時に金融エリアのリージョンを持つドメイン名を指定する必要があります。最も良いのは、redis.ap-shanghai-fsi.tencentcloudapi.com のように Region のエリアと一致させることです。



## 2. パラメータ入力

以下のリクエストパラメータリストは、インターフェースリクエストパラメータと一部の共通パラメータのみを表しています。完全な共通パラメータのリストは、[共通のリクエストパラメータ](https://cloud.tencent.com/document/api/239/20005)を参照してください。

| パラメータ名 | 選択必須 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | 要 | String | 共通パラメータ。本インターフェースの取得値：DescribeProductInfo |
| Version | 要 | String | 共通パラメータ。本インターフェースの値：2018-04-12 |
| Region | 要 | String | 共通パラメータ。製品がサポートする[リージョンリスト](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。|

## 3. パラメータ出力

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| RegionSet | Array of [RegionConf](https://cloud.tencent.com/document/api/239/20022#RegionConf) | リージョン販売情報|
| RequestId | String | 一意のリクエスト ID。毎回リクエストするごとに戻ります。問題を見つけ出す際、そのリクエストの RequestId を提供する必要があります。|

## 4. サンプル

### サンプル1 リクエストサンプル

#### 入力サンプル

```
https://redis.tencentcloudapi.com/?Action=DescribeProductInfo
&<共通リクエストパラメータ>
```

#### 出力サンプル

```
{
    "Response":{
        "RegionSet":[
            {
                "RegionId":"ap-guangzhou",
                "RegionName":"广州",
                "RegionShortName":"GZ",
                "Area":"華南エリア",
                "ZoneSet":[
                    {
                        "ZoneId":"ap-guangzhou-2",
                        "ZoneName":"広州2区",
                        "IsSaleout":false,
                        "IsDefault":false,
                        "NetWorkType":[
                            "basenet",
                            "vpcnet"
                        ],
                        "ProductSet":[
                            {
                                "Type":7,
                                "TypeName":"Redis クラスタ版",
                                "MinBuyNum":1,
                                "MaxBuyNum":10,
                                "Saleout":false,
                                "Engine":"ソーシャル版Redis",
                                "Version":"Redis 4.0",
                                "TotalSize":[
                                    "12",
                                    "20",
                                    "32",
                                    "64",
                                    "96",
                                    "128",
                                    "256",
                                    "384",
                                    "512",
                                    "768",
                                    "1024",
                                    "2048",
                                    "3072",
                                    "4096"
                                ],
                                "ShardSize":[
                                    "4",
                                    "8",
                                    "12",
                                    "16",
                                    "20",
                                    "24",
                                    "32"
                                ],
                                "ReplicaNum":[
                                    "1",
                                    "2",
                                    "3",
                                    "4",
                                    "5"
                                ],
                                "ShardNum":[
                                    "3",
                                    "5",
                                    "8",
                                    "12",
                                    "16",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "64",
                                    "80",
                                    "96",
                                    "128"
                                ],
                                "PayMode":"1",
                                "EnableRepicaReadOnly":true
                            },
                            {
                                "Type":4,
                                "TypeName":"CKVクラスタ版",
                                "MinBuyNum":1,
                                "MaxBuyNum":10,
                                "Saleout":false,
                                "Engine":"Tencent Cloud CKV",
                                "Version":"Redis 3.2",
                                "TotalSize":[
                                    "12",
                                    "20",
                                    "32",
                                    "64",
                                    "96",
                                    "128",
                                    "256",
                                    "384",
                                    "512",
                                    "768",
                                    "1024",
                                    "2048",
                                    "3072",
                                    "4096"
                                ],
                                "ShardSize":[
                                    "4",
                                    "8",
                                    "16",
                                    "24",
                                    "32",
                                    "48",
                                    "64",
                                    "80",
                                    "96",
                                    "128",
                                    "160",
                                    "192",
                                    "256",
                                    "320",
                                    "384"
                                ],
                                "ReplicaNum":[
                                    "1",
                                    "2",
                                    "3",
                                    "4",
                                    "5"
                                ],
                                "ShardNum":[
                                    "3",
                                    "5",
                                    "8",
                                    "12",
                                    "16",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "64",
                                    "80",
                                    "96",
                                    "128"
                                ],
                                "PayMode":"1",
                                "EnableRepicaReadOnly":false
                            },
                            {
                                "Type":2,
                                "TypeName":"Redis マスタースレーブ版",
                                "MinBuyNum":1,
                                "MaxBuyNum":10,
                                "Saleout":false,
                                "Engine":"ソーシャル版Redis",
                                "Version":"Redis 2.8",
                                "TotalSize":[
                                    "1",
                                    "2",
                                    "4",
                                    "8",
                                    "12",
                                    "16",
                                    "20",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "60",
                                    "0.25"
                                ],
                                "ShardSize":[
                                    "1",
                                    "2",
                                    "4",
                                    "8",
                                    "12",
                                    "16",
                                    "20",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "60",
                                    "0.25"
                                ],
                                "ReplicaNum":[
                                    "1"
                                ],
                                "ShardNum":[
                                    "1"
                                ],
                                "PayMode":"1",
                                "EnableRepicaReadOnly":false
                            },
                            {
                                "Type":5,
                                "TypeName":"Redis スタンドアロン版",
                                "MinBuyNum":1,
                                "MaxBuyNum":10,
                                "Saleout":false,
                                "Engine":"ソーシャル版Redis",
                                "Version":"Redis 2.8",
                                "TotalSize":[
                                    "1",
                                    "2",
                                    "4",
                                    "8",
                                    "12",
                                    "16",
                                    "20",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "60"
                                ],
                                "ShardSize":[
                                    "1",
                                    "2",
                                    "4",
                                    "8",
                                    "12",
                                    "16",
                                    "20",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "60"
                                ],
                                "ReplicaNum":[
                                    "0"
                                ],
                                "ShardNum":[
                                    "1"
                                ],
                                "PayMode":"1",
                                "EnableRepicaReadOnly":false
                            },
                            {
                                "Type":2,
                                "TypeName":"Redis マスタースレーブ版",
                                "MinBuyNum":1,
                                "MaxBuyNum":10,
                                "Saleout":false,
                                "Engine":"ソーシャル版Redis",
                                "Version":"Redis 2.8",
                                "TotalSize":[
                                    "1",
                                    "2",
                                    "4",
                                    "8",
                                    "12",
                                    "16",
                                    "20",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "60"
                                ],
                                "ShardSize":[
                                    "1",
                                    "2",
                                    "4",
                                    "8",
                                    "12",
                                    "16",
                                    "20",
                                    "24",
                                    "32",
                                    "40",
                                    "48",
                                    "60"
                                ],
                                "ReplicaNum":[
                                    "1"
                                ],
                                "ShardNum":[
                                    "1"
                                ],
                                "PayMode":"0",
                                "EnableRepicaReadOnly":false
                            },
                            {
                                "Type":3,
                                "TypeName":"CKVスタンドアロン版",
                                "MinBuyNum":1,
                                "MaxBuyNum":10,
                                "Saleout":false,
                                "Engine":"Tencent Cloud CKV",
                                "Version":"Redis 3.2",
                                "TotalSize":[
                                    "4",
                                    "8",
                                    "16",
                                    "24",
                                    "32",
                                    "48",
                                    "64",
                                    "80",
                                    "96",
                                    "128",
                                    "160",
                                    "192",
                                    "256",
                                    "320",
                                    "384"
                                ],
                                "ShardSize":[
                                    "4",
                                    "8",
                                    "16",
                                    "24",
                                    "32",
                                    "48",
                                    "64",
                                    "80",
                                    "96",
                                    "128",
                                    "160",
                                    "192",
                                    "256",
                                    "320",
                                    "384"
                                ],
                                "ReplicaNum":[
                                    "0"
                                ],
                                "ShardNum":[
                                    "1"
                                ],
                                "PayMode":"1",
                                "EnableRepicaReadOnly":false
                            }
                        ]
                    }
                ]
            }
        ],
        "RequestId":"3c5730c6-02f2-46fd-8bf1-725b8b608fb9"
    }
}
```


## 5. 開発者リソース

### API Explorer

**本ツールはオンライン呼び出し、署名認証、SDK コード生成、高速インターフェース検索などの能力を提供します。クラウド API の使用難易度を大きく下げることができるため、使用することをお勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeProductInfo)

### SDK

クラウド API 3.0 は、付属の開発ツールセット（SDK）を提供します。さまざまなプログラミング言語をサポートすることで、より簡単に API を呼び出すことができます。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. エラーコード

以下では、インターフェースのサービスロジックに関連するエラーコードのみを示します。その他のエラーコードについては[共通エラーコード](https://cloud.tencent.com/document/api/239/20007#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)をご覧ください。

| エラーコード | 説明 |
|---------|---------|
| FailedOperation.SystemError | 内部システムエラー。サービスには関係ありません。|
| InvalidParameter | パラメータエラー |
| InvalidParameter.EmptyParam | パラメータは空です。|

