## 1. API説明

APIリクエストドメイン名：as.tencentcloudapi.com 。

このAPI（DescribeAutoScalingGroups）は、スケーリンググループの情報を照合するために使用されます。

* スケーリンググループID、スケーリンググループ名、または起動構成IDなどの情報に基づいて、スケーリンググループの詳細情報を照合できます。フィルタリング情報の詳細については、`Filter`を参照してください。
* パラメータがブランクの場合、現在のユーザーに一定数のスケーリンググループ（`Limit`で指定された数、デフォルトは20）を返します。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：as.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータについては、[共通リクエストパラメータ](/document/api/377/20426)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：DescribeAutoScalingGroups |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-04-19 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| AutoScalingGroupIds.N | いいえ | Array of String | 1つ以上のスケーリンググループIDで照合します。スケーリングIDは`asg-nkdwoui0`のような形をしています。各リクエストの上限は100です。このパラメータは`AutoScalingGroups`と`Filters`の両方の指定をサポートしません。 |
| Filters.N | いいえ | Array of [Filter](/document/api/377/20453#Filter) | フィルタ条件。<br/><li> auto-scaling-group-id - String - 必須項目：いいえ -（フィルタ条件）スケーリンググループIDでフィルタリングします。</li><li> auto-scaling-group-name - String - 必須項目：いいえ -（フィルタ条件）スケーリンググループの名前でフィルタリングします。</li><li> launch-configuration-id - String - 必須項目：いいえ -（フィルタ条件）起動構成IDでフィルタリングします。</li><br/>各リクエストの`Filters`の上限は10で、`Filter.Values`の上限は5です。このパラメータは`AutoScalingGroupIds`と`Filters`の両方の指定をサポートしません。 |
| Limit | いいえ | Integer | 返される数、デフォルトは20、最大値は100です。`Limit`の詳細については、API [紹介](https://cloud.tencent.com/document/api/213/15688)の関連セクションを参照してください。 |
| Offset | いいえ | Integer | オフセット、デフォルトは0です。`Offset`の詳細については、API [紹介](https://cloud.tencent.com/document/api/213/15688)の関連セクションを参照してください。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| AutoScalingGroupSet | Array of [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup) | スケーリンググループの詳細情報のリスト。|
| TotalCount | Integer | 条件を満たすスケーリンググループの数量。|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1　スケーリンググループを照合します

スケーリンググループを照合するためのスケーリンググループIDを指定します

#### 入力例

```
https://as.tencentcloudapi.com/?Action=DescribeAutoScalingGroups
&AutoScalingGroupIds.0=asg-nkdwoui0
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "AutoScalingGroupSet": [
            {
                "LaunchConfigurationId": "asc-7vucy6ae",
                "ForwardLoadBalancerSet": [
                    {
                        "TargetAttributes": [
                            {
                                "Port": 8080,
                                "Weight": 10
                            }
                        ],
                        "LocationId": "loc-l3hmaev9",
                        "ListenerId": "lbl-ncw704sn",
                        "LoadBalancerId": "lb-23aejgcv"
                    }
                ],
                "LoadBalancerIdSet": [],
                "InstanceCount": 1,
                "DesiredCapacity": 1,
                "AutoScalingGroupStatus": "NORMAL",
                "AutoScalingGroupId": "asg-nkdwoui0",
                "ProjectId": 0,
                "TerminationPolicySet": [
                    "OLDEST_INSTANCE"
                ],
                "AutoScalingGroupName": "vpc-7layer-lb",
                "InServiceInstanceCount": 1,
                "DefaultCooldown": 301,
                "MinSize": 0,
                "MaxSize": 10,
                "VpcId": "vpc-hy436tmc",
                "LaunchConfigurationName": "起動構成1",
                "CreatedTime": "2018-09-27T02:01:28Z",
                "SubnetIdSet": [
                    "subnet-3tmerl37",
                    "subnet-b0vxjhot"
                ],
                "EnabledStatus": "ENABLED",
                "ZoneSet": []
            }
        ],
        "TotalCount": 1,
        "RequestId": "b8d3660c-bed1-40ad-9e7d-77390c9610be"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeAutoScalingGroups)

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
| InvalidFilter | 無効なフィルタです。 |
| InvalidParameterConflict | 指定された2つのパラメータが競合しており、同時に存在することはできません。 |
| InvalidParameterValue.Filter | 無効なフィルタです。 |
| InvalidPermission | この操作はアカウントではサポートされていません。 |

