## 1. API説明

APIリクエストドメイン名：as.tencentcloudapi.com 。

このAPI（DescribeLaunchConfigurations）は起動構成の情報を照合するために使用されます。

* 起動構成ID、起動構成名称などの情報に基づいて起動構成の詳細情報を照合できます。フィルタリング情報の詳細については`Filter`を参照してください。
* パラメータがブランクの場合、現在のユーザーに一定の数量の起動構成（`Limit`で指定された数量、デフォルトは20）を返します。

デフォルトのAPIリクエスト頻度制限：10回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：as.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータについては、[共通リクエストパラメータ](/document/api/377/20426)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：DescribeLaunchConfigurations |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-04-19 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| LaunchConfigurationIds.N | いいえ | Array of String | 1つ以上の起動構成IDに従って照合してください。起動構成IDの形は：`asc-ouy1ax38`。毎回リクエストの最大制限は100です。このパラメータは`LaunchConfigurationIds`と`Filters`の両方の指定をサポートしません |
| Filters.N | いいえ | Array of [Filter](/document/api/377/20453#Filter) | フィルタリング条件。<br/><li> launch-configuration-id - String - 必須項目：いいえ -（フィルタリング条件）起動構成IDでフィルタします。</li><li> launch-configuration-name - String - 必須項目であるか：いいえ -（フィルタリング条件）起動構成名称でフィルタします。</li><br/>毎回リクエストの`Filters`の上限は10で、`Filter.Values`の上限は5です。このパラメータは`LaunchConfigurationIds`と`Filters`の両方の指定をサポートしません。 |
| Limit | いいえ | Integer | 返される数、デフォルトは20、最大値は100です。`Limit`の詳細については、API [紹介](https://cloud.tencent.com/document/api/213/15688)の関連セクションを参照してください。 |
| Offset | いいえ | Integer | オフセット、デフォルトは0です。`Offset`の詳細については、API [紹介](https://cloud.tencent.com/document/api/213/15688)の関連セクションを参照してください。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| TotalCount | Integer | 条件を満たす起動構成の数量。|
| LaunchConfigurationSet | Array of [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration) | 起動構成詳細情報リスト。|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 Filtersを使用して起動構成リストを確認します

#### 入力例

```
https://as.tencentcloudapi.com/?Action=DescribeLaunchConfigurations
&Filters.0.Name=launch-configuration-id
&Filters.0.Values.0=asc-l7rduvv0
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "TotalCount": 1,
        "LaunchConfigurationSet": [
            {
                "ProjectId": 0,
                "LaunchConfigurationId": "asc-l7rduvv0",
                "LaunchConfigurationName": "lc2",
                "AutoScalingGroupAbstractSet": [],
                "InstanceType": "S2.SMALL2",
                "InstanceTypes": [
                    "S2.SMALL2"
                ],
                "InstanceChargeType": "POSTPAID_BY_HOUR",
                "InstanceMarketOptions": null,
                "SystemDisk": {
                    "DiskType": "LOCAL_BASIC",
                    "DiskSize": 50
                },
                "DataDisks": [
                    {
                        "DiskType": "LOCAL_BASIC",
                        "DiskSize": 50
                    }
                ],
                "LoginSettings": {
                    "KeyIds": []
                },
                "InternetAccessible": {
                    "InternetChargeType": "BANDWIDTH_POSTPAID_BY_HOUR",
                    "InternetMaxBandwidthOut": 1,
                    "PublicIpAssigned": true
                },
                "SecurityGroupIds": [],
                "EnhancedService": {
                    "SecurityService": {
                        "Enabled": true
                    },
                    "MonitorService": {
                        "Enabled": true
                    }
                },
                "UserData": null,
                "CreatedTime": "2018-05-03T03:23:10Z"
            }
        ],
        "RequestId": "15f9582f-72ff-4b5f-91b6-ff905782391b"
    }
}
```

### 例2 起動構成IDで起動構成リストを照合します

#### 入力例

```
https://as.tencentcloudapi.com/?Action=DescribeLaunchConfigurations
&LaunchConfigurationIds.0=asc-l7rduvv0
&LaunchConfigurationIds.1=asc-2ejax3t8
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "TotalCount": 2,
        "LaunchConfigurationSet": [
            {
                "ProjectId": 0,
                "LaunchConfigurationId": "asc-2ejax3t8",
                "LaunchConfigurationName": "lc1",
                "AutoScalingGroupAbstractSet": [],
                "InstanceType": "D1.2XLARGE32",
                "InstanceTypes": [
                    "D1.2XLARGE32"
                ],
                "InstanceChargeType": "POSTPAID_BY_HOUR",
                "InstanceMarketOptions": null,
                "SystemDisk": {
                    "DiskType": "LOCAL_BASIC",
                    "DiskSize": 50
                },
                "DataDisks": [],
                "LoginSettings": {
                    "KeyIds": []
                },
                "InternetAccessible": {
                    "InternetChargeType": "TRAFFIC_POSTPAID_BY_HOUR",
                    "InternetMaxBandwidthOut": 0,
                    "PublicIpAssigned": false
                },
                "SecurityGroupIds": [],
                "EnhancedService": {
                    "SecurityService": {
                        "Enabled": true
                    },
                    "MonitorService": {
                        "Enabled": true
                    }
                },
                "UserData": null,
                "CreatedTime": "2018-05-03T06:37:48Z"
            },
            {
                "ProjectId": 0,
                "LaunchConfigurationId": "asc-l7rduvv0",
                "LaunchConfigurationName": "lc2",
                "AutoScalingGroupAbstractSet": [],
                "InstanceType": "S2.SMALL2",
                "InstanceTypes": [
                    "S2.SMALL2"
                ],
                "InstanceChargeType": "POSTPAID_BY_HOUR",
                "InstanceMarketOptions": null,
                "SystemDisk": {
                    "DiskType": "LOCAL_BASIC",
                    "DiskSize": 50
                },
                "DataDisks": [
                    {
                        "DiskType": "LOCAL_BASIC",
                        "DiskSize": 50
                    }
                ],
                "LoginSettings": {
                    "KeyIds": []
                },
                "InternetAccessible": {
                    "InternetChargeType": "BANDWIDTH_POSTPAID_BY_HOUR",
                    "InternetMaxBandwidthOut": 1,
                    "PublicIpAssigned": true
                },
                "SecurityGroupIds": [],
                "EnhancedService": {
                    "SecurityService": {
                        "Enabled": true
                    },
                    "MonitorService": {
                        "Enabled": true
                    }
                },
                "UserData": null,
                "CreatedTime": "2018-05-03T03:23:10Z"
            }
        ],
        "RequestId": "f7dd68bc-d5e3-4a43-92a5-bde6d8fe9bd4"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeLaunchConfigurations)

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
| InvalidLaunchConfiguration | 無効な起動構成です。 |
| InvalidLaunchConfigurationId | 起動構成IDが無効です。 |
| InvalidParameterConflict | 指定された2つのパラメータが競合しており、同時に存在することはできません。 |
| InvalidPermission | この操作はアカウントではサポートされていません。 |

