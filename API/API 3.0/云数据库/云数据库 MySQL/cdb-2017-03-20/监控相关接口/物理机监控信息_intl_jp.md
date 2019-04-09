## 1. API説明

APIリクエストドメイン名： cdb.tencentcloudapi.com 。

このAPI（DescribeDeviceMonitorInfo）はデータベース物理サーバー当日の監視情報の照合に使用されます。現時点でメモリ488G、ディスク6Tのインスタンス照合のみをサポートします。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：cdb.ap-shanghai-fsi.tencentcloudapi.com 。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/236/15833)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ。このAPIの値：DescribeDeviceMonitorInfo |
| Version | はい | String | 共通パラメータ、該当APIの値：2017/03/20 |
| Region | はい | String | 共通パラメータ。詳細について製品がサポートする[地域リスト](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| InstanceId | はい | String | インスタンスID。フォーマット：cdb-c1nl9rpv。データベースページコンソールページで表示されるインスタンスIDと同じ |
| Count | いいえ | Integer | 当日最近Count個の5分間粒度の監視データを返します。最小値は1、最大値は288。このパラメータを渡さないとデフォルトで当日すべての5分間粒度の監視データを返します。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| Cpu | [DeviceCpuInfo](/document/api/236/15878#DeviceCpuInfo) | インスタンスCPU監視データ|
| Mem | [DeviceMemInfo](/document/api/236/15878#DeviceMemInfo) | インスタンスメモリ監視データ|
| Net | [DeviceNetInfo](/document/api/236/15878#DeviceNetInfo) | インスタンスネットワーク監視データ|
| Disk | [DeviceDiskInfo](/document/api/236/15878#DeviceDiskInfo) | インスタンスディスク監視データ|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 インスタンス所在物理サーバーの監視情報の取得

#### 入力例

```
https://cdb.tencentcloudapi.com/?Action=DescribeDeviceMonitorInfo
&InstanceId=cdb-uns231ns
&Count=2
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "Cpu": {
            "Load": [
                174,
                169
            ],
            "Rate": [
                {
                    "CpuCore": 0,
                    "Rate": [
                        4,
                        5
                    ]
                },
                {
                    "CpuCore": 0,
                    "Rate": [
                        7,
                        7
                    ]
                },
                {
                    "CpuCore": 1,
                    "Rate": [
                        15,
                        7
                    ]
                },
                {
                    "CpuCore": 2,
                    "Rate": [
                        7,
                        7
                    ]
                },
                {
                    "CpuCore": 3,
                    "Rate": [
                        6,
                        5
                    ]
                },
                {
                    "CpuCore": 4,
                    "Rate": [
                        4,
                        2
                    ]
                },
                {
                    "CpuCore": 5,
                    "Rate": [
                        4,
                        5
                    ]
                },
                {
                    "CpuCore": 6,
                    "Rate": [
                        7,
                        5
                    ]
                },
                {
                    "CpuCore": 7,
                    "Rate": [
                        7,
                        9
                    ]
                },
                {
                    "CpuCore": 8,
                    "Rate": [
                        8,
                        8
                    ]
                },
                {
                    "CpuCore": 9,
                    "Rate": [
                        6,
                        4
                    ]
                },
                {
                    "CpuCore": 10,
                    "Rate": [
                        4,
                        14
                    ]
                },
                {
                    "CpuCore": 11,
                    "Rate": [
                        2,
                        2
                    ]
                },
                {
                    "CpuCore": 12,
                    "Rate": [
                        6,
                        3
                    ]
                },
                {
                    "CpuCore": 13,
                    "Rate": [
                        10,
                        14
                    ]
                },
                {
                    "CpuCore": 14,
                    "Rate": [
                        12,
                        6
                    ]
                },
                {
                    "CpuCore": 15,
                    "Rate": [
                        5,
                        2
                    ]
                },
                {
                    "CpuCore": 16,
                    "Rate": [
                        4,
                        2
                    ]
                },
                {
                    "CpuCore": 17,
                    "Rate": [
                        2,
                        4
                    ]
                },
                {
                    "CpuCore": 18,
                    "Rate": [
                        4,
                        6
                    ]
                },
                {
                    "CpuCore": 19,
                    "Rate": [
                        14,
                        9
                    ]
                },
                {
                    "CpuCore": 20,
                    "Rate": [
                        6,
                        6
                    ]
                },
                {
                    "CpuCore": 21,
                    "Rate": [
                        5,
                        5
                    ]
                },
                {
                    "CpuCore": 22,
                    "Rate": [
                        3,
                        12
                    ]
                },
                {
                    "CpuCore": 23,
                    "Rate": [
                        2,
                        2
                    ]
                }
            ]
        },
        "Mem": {
            "Total": [
                65716676,
                65716676
            ],
            "Used": [
                57163160,
                57158148
            ]
        },
        "Net": {
            "Conn": [
                133,
                130
            ],
            "PackageIn": [
                960,
                960
            ],
            "PackageOut": [],
            "FlowIn": [
                150,
                112
            ],
            "FlowOut": [
                1342,
                1260
            ]
        },
        "Disk": {
            "Read": [
                0,
                0
            ],
            "Write": [
                740,
                797
            ],
            "IoRatioPerSec": [
                0,
                0
            ],
            "IoWaitTime": [
                61,
                65
            ]
        },
        "RequestId": "85b295bb-8f43-ce01-e35f-5a02e2beeeac"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeDeviceMonitorInfo)

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
| FailedOperation.StatusConflict | タスク状態競合。 |
| InvalidParameter | パラメータエラー。 |
| InvalidParameter.InstanceNotFound | インスタンスが存在しません。 |
| OperationDenied | 操作不能です。 |

