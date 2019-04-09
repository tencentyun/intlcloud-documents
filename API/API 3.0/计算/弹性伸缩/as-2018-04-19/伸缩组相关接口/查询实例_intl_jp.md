## 1. API説明

APIリクエストドメイン名：as.tencentcloudapi.com 。

このAPI（DescribeAutoScalingInstances）は、AS関連インスタンスの情報を照合するために使用されます。

* インスタンスID、スケーリンググループIDなどの情報に基づいて、インスタンスの詳細情報を照合できます。フィルタリング情報の詳細については、`Filter`を参照してください。
* パラメータがブランクの場合、現在のユーザーに一定数のインスタンス（`Limit`で指定された数、デフォルトは20）を返します。

デフォルトのAPIリクエスト頻度制限：10回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：as.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータについては、[共通リクエストパラメータ](/document/api/377/20426)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：DescribeAutoScalingInstances |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-04-19 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| InstanceIds.N | いいえ | Array of String | 照合されるCVMのインスタンスID。このパラメータは、InstanceIdsとFiltersの両方の指定をサポートしません。 |
| Filters.N | いいえ | Array of [Filter](/document/api/377/20453#Filter) | フィルタ条件。<br/><li> instance-id - String - 必須項目：いいえ -（フィルタ条件）インスタンスIDでフィルタリングします。</li><li> auto-scaling-group-id - String - 必須項目：いいえ -（フィルタ条件）スケーリンググループIDでフィルタリングします。</li><br/>各リクエストの`Filters`の上限は10で、`Filter.Values`の上限は5です。このパラメータは`InstanceIds`と`Filters`の両方の指定をサポートしません。 |
| Offset | いいえ | Integer | オフセット、デフォルトは0です。`Offset`の詳細については、API [紹介](https://cloud.tencent.com/document/api/213/15688)の関連セクションを参照してください。 |
| Limit | いいえ | Integer | 返される数、デフォルトは20、最大値は100です。`Limit`の詳細については、API [紹介](https://cloud.tencent.com/document/api/213/15688)の関連セクションを参照してください。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| AutoScalingInstanceSet | Array of [Instance](/document/api/377/20453#Instance) | インスタンス詳細情報のリスト。|
| TotalCount | Integer | 条件を満たすインスタンスの数量。|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1　指定されたインスタンスを照合します

#### 入力例

```
https://as.tencentcloudapi.com/?Action=DescribeAutoScalingInstances
&InstanceIds.0=ins-1fswxz1m
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "TotalCount": 1,
        "AutoScalingInstanceSet": [
            {
                "ProtectedFromScaleIn": false,
                "Zone": "ap-guangzhou-3",
                "LaunchConfigurationId": "asc-5fzsm72a",
                "InstanceId": "ins-1fswxz1m",
                "AddTime": "2018-08-21T12:05:12Z",
                "CreationType": "AUTO_CREATION",
                "AutoScalingGroupId": "asg-4o61gsxi",
                "HealthStatus": "HEALTHY",
                "LifeCycleState": "IN_SERVICE",
                "LaunchConfigurationName": "シリーズ2ローカルディスク",
                "InstanceType": "S2.SMALL2"
            }
        ],
        "RequestId": "2ae3e836-d47a-431c-b54b-4e1c2f419e5b"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeAutoScalingInstances)

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

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| InternalError | 内部エラー |
| InvalidFilter | 無効なフィルタです。 |
| InvalidParameter.Conflict | パラメータの競合：指定された複数のパラメータが競合しており、同時に存在することはできません。 |
| InvalidParameterValue.Filter | 無効なフィルタです。 |

