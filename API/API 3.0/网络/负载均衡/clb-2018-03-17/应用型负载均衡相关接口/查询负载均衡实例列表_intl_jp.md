## 1. API説明

APIリクエストドメイン名：clb.tencentcloudapi.com

CLBインスタンスリストの照合


デフォルトのAPIリクエスト頻度制限：20回/秒

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互通信できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例：clb.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/214/30670)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：DescribeLoadBalancers |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-03-17 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/214/30670#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。|
| LoadBalancerIds.N | いいえ | Array of String | 　CLBインスタンスID。|
| LoadBalancerType | いいえ | String | CLBインスタンスのネットワークタイプ：<br/>OPEN：パブリックネットワークの属性、INTERNAL：プライベートネットワークの属性。|
| Forward | いいえ | Integer | 1：アプリケーション型、0：従来型。|
| LoadBalancerName | いいえ | Array of String | 　CLBインスタンス名。|
| Domain | いいえ | String | Tencent CloudがCLBインスタンスに割り当てるドメイン名、アプリケーション型CLBのこのフィールドは意味がありません。|
| LoadBalancerVips.N | いいえ | Array of String | CLBインスタンスのVIPアドレス、複数のアドレスをサポートします。|
| BackendPublicIps.N | いいえ | Array of String | バックエンドCVMのパブリックネットワークIP。|
| BackendPublicIps.N | いいえ | Array of String | バックエンドCVMのパブリックネットワークIP。|
| Offset | いいえ | Integer | データオフセット、デフォルトは0|
| Limit | いいえ | Integer | 返すCLB数、デフォルトは20。|
| OrderBy | いいえ | String | 並び替えたフィールド、以下のフィールドをサポートします：LoadBalancerName、CreateTime、Domain、LoadBalancerType。|
| OrderType | いいえ | Integer | 1：降順、0：昇順、デフォルトで作成時間に従って降順。|
| SearchKey | いいえ | String | フィールドを検索し、名称、ドメイン、VIPをファジィマッチングします。|
| ProjectId | いいえ | Integer | CLBインスタンスのあるプロジェクトID。DescribeProject APIを介して取得します。|
| WithRs | いいえ | Integer | 照合するCLBはRSをバインディングするかどうか、0：CVMをバインディングしません。1：CVMをバインディングします。-1：すべてを照合します。|

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| TotalCount | Integer | フィルタ条件を満たすCLBインスタンスの合計数。|
| LoadBalancerSet | Array of [LoadBalancer](/document/api/214/30694#LoadBalancer) | 返すCLBインスタンス配列。|
| RequestId | String | 唯一のリクエストID、毎回リクエストが返されます。問題を特定する時今回のリクエストのRequestIdを提供する必要があります。|

## 4. 例

### 例1 CLBインスタンス IDに基づく照合

#### 入力例

```
https://clb.tencentcloudapi.com/?Action=DescribeLoadBalancers
&LoadBalancerIds.0=lb-6efswuxa
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "TotalCount": 1,
        "LoadBalancerSet": [
            {
                "LoadBalancerId": "lb-6efswuxa",
                "LoadBalancerName": "newlbname",
                "Forward": 1,
                "Domain": "",
                "LoadBalancerVips": [
                    "139.199.232.22"
                ],
                "LoadBalancerType": "OPEN",
                "Status": 1,
                "CreateTime": "2018-09-13 10:25:03",
                "StatusTime": "2018-09-13 10:45:55",
                "ProjectId": 0,
                "VpcId": "",
                "OpenBgp": 0,
                "Snat": false,
                "Isolation": 0,
                "Log": ""
            }
        ],
        "RequestId": "319412e1-8138-49a4-a128-a290641054c1"
    }
}
```

### 例2 CLBのタイプ、所属するプロジェクト、CLB名称、CLBインスタンスのvipに基づく照合

#### 入力例

```
https://clb.tencentcloudapi.com/?Action=DescribeLoadBalancers
&LoadBalancerType=OPEN
&Forward=1
&ProjectId=0
&LoadBalancerName=newlbname
&LoadBalancerVips.0=139.199.232.22
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "TotalCount": 1,
        "LoadBalancerSet": [
            {
                "LoadBalancerId": "lb-6efswuxa",
                "LoadBalancerName": "newlbname",
                "Forward": 1,
                "Domain": "",
                "LoadBalancerVips": [
                    "139.199.232.22"
                ],
                "LoadBalancerType": "OPEN",
                "Status": 1,
                "CreateTime": "2018-09-13 10:25:03",
                "StatusTime": "2018-09-13 10:45:55",
                "ProjectId": 0,
                "VpcId": "",
                "OpenBgp": 0,
                "Snat": false,
                "Isolation": 0,
                "Log": ""
            }
        ],
        "RequestId": "cbe24464-5c73-4493-9943-f72306c6ac14"
    }
}
```

### 例3 バイクエンドでバインディングする、指定プライベートネットワークIPがあるサーバーのCLBインスタンスの照合

プライベートネットワークIPは10.186.225.251であるCVMをバインディングするCLBインスタンスの照合

#### 入力例

```
https://clb.tencentcloudapi.com/?Action=DescribeLoadBalancers
&WithRs=1
&BackendPrivateIps.0=10.186.225.25
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "TotalCount": 1,
        "LoadBalancerSet": [
            {
                "LoadBalancerId": "lb-o5z8mjxc",
                "LoadBalancerName": "atomtest",
                "Forward": 1,
                "Domain": "",
                "LoadBalancerVips": [
                    "139.199.232.90"
                ],
                "LoadBalancerType": "OPEN",
                "Status": 1,
                "CreateTime": "2017-11-13 10:37:43",
                "StatusTime": "2018-08-10 11:06:39",
                "ProjectId": 0,
                "VpcId": "",
                "OpenBgp": 0,
                "Snat": false,
                "Isolation": 1,
                "Log": ""
            }
        ],
        "RequestId": "5c51b1cb-88bf-4774-b671-436a59449c12"
    }
}
```

### 例4 名称、ドメイン名、VIPの複数のフィールドに基づくCLBインスタンスのファジィ照合

#### 入力例

```
https://clb.tencentcloudapi.com/?Action=DescribeLoadBalancers
&SearchKey=newlbname
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "TotalCount": 1,
        "LoadBalancerSet": [
            {
                "LoadBalancerId": "lb-6efswuxa",
                "LoadBalancerName": "newlbname",
                "Forward": 1,
                "Domain": "",
                "LoadBalancerVips": [
                    "139.199.232.22"
                ],
                "LoadBalancerType": "OPEN",
                "Status": 1,
                "CreateTime": "2018-09-13 10:25:03",
                "StatusTime": "2018-09-13 10:45:55",
                "ProjectId": 0,
                "VpcId": "",
                "OpenBgp": 0,
                "Snat": false,
                "Isolation": 0,
                "Log": ""
            }
        ],
        "RequestId": "1c9e2295-f5ef-48c0-847d-47a6d950578d"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIを使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=clb&Version=2018-03-17&Action=DescribeLoadBalancers)

### SDK

クラウドAPI 3.0は、API呼び出しを容易にするために複数のプログラミング言語をサポートする、関連開発ツールセット（SDK）を提供します。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### CLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. エラーコード

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](/document/api/214/30673#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| FailedOperation | 操作失敗 |
| InternalError | 内部エラー |
| InvalidParameter | パラメータエラー。|
| InvalidParameterValue | パラメータ値エラー |
| UnauthorizedOperation | 操作が承認されていません |

