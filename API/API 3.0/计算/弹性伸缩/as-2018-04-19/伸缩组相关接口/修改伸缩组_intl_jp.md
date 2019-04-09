## 1. API説明

APIリクエストドメイン名：as.tencentcloudapi.com 。

このAPI（ModifyAutoScalingGroup）は、スケーリンググループを変更するために使用されます。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：as.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータについては、[共通リクエストパラメータ](/document/api/377/20426)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：ModifyAutoScalingGroup |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-04-19 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| AutoScalingGroupId | はい | String | スケーリンググループID |
| AutoScalingGroupName | いいえ | String | スケーリンググループの名前。アカウント内で唯一である必要があります。この名前は、中国語、英語、数字、アンダースコア、区切り記号「-」、小数点のみをサポートし、最大長は55バイトを超えることはできません。 |
| DefaultCooldown | いいえ | Integer | デフォルトの冷却時間。秒単位で、デフォルト値は300です |
| DesiredCapacity | いいえ | Integer | 目標インスタンス数。最小インスタンス数と最大インスタンス数の間にあります |
| LaunchConfigurationId | いいえ | String | 起動構成ID |
| MaxSize | いいえ | Integer | 最大インスタンス数。その値の範囲は0～2000です。 |
| MinSize | いいえ | Integer | 最小インスタンス数。その範囲は0～2000です。 |
| ProjectId | いいえ | Integer | プロジェクトID |
| SubnetIds.N | いいえ | Array of String | サブネットIDリスト |
| TerminationPolicies.N | いいえ | Array of String | 終了ポリシー。現在の最大長は1です。値はOLDEST_INSTANCEとNEWEST_INSTANCEを含みます。<br/><br><li> OLDEST_INSTANCEは、スケーリンググループ内の最も古いインスタンスを優先に終了します。<br/><br><li> NEWEST_INSTANCEは、スケーリンググループ内の最新のインスタンスを優先に終了します。 |
| VpcId | いいえ | String | VPC ID、基本ネットワークの場合はブランクのままにしておきます。具体的なVPC IDに変更する場合は対応するSubnetIdsを指定する必要があり、基本ネットワークに変更する場合は対応するZonesを指定する必要があります。 |
| Zones.N | いいえ | Array of String | Availability Zoneリスト |
| RetryPolicy | いいえ | String | 再試行ポリシー。そのの値はIMMEDIATE_RETRYとINCREMENTAL_INTERVALSを含みます。デフォルト値はIMMEDIATE_RETRYです。<br/><br><li> IMMEDIATE_RETRYは、すぐに再試行し、短時間で素早く再試行することです。連続した失敗が一定の回数（5回）を超えると、再試行は停止します。<br/><br><li> INCREMENTAL_INTERVALSは、間隔を増分して再試行することです。連続した失敗の回数が増えるにつれて、再試行間隔は徐々に増え、再試行間隔は数秒から1日までです。 |
| ZonesCheckPolicy | いいえ | String | Availability Zone検証ポリシー。値はALLおよびANYがあり、デフォルト値はANYです。スケーリンググループが実際にリソース関連のフィールド（起動構成、Availability Zone、サブネット）を変更するときに機能します。<br/><br><li> ALLは、すべてのAvailability Zone（Zone）またはサブネット（SubnetId）が使用可能な場合は、検証に合格し、それ以外の場合は検証エラーが報告されます。<br/><br><li> ANYは、任意のAvailability Zone（Zone）またはサブネット（SubnetId）が使用可能な場合は、検証に合格し、それ以外の場合は検証エラーが報告されます。<br/><br/>Availability Zoneまたはサブネットが使用できない一般的な原因は、Availability ZoneのCVMインスタンスタイプの売り切れ、Availability ZoneのCBSクラウドディスクの売り切れ、Availability Zoneの割り当て量不足、サブネットIPの不足などです。<br/>Zones/SubnetIdsのAvailability Zoneまたはサブネットが存在しない場合は、ZonesCheckPolicyの値に関係なく検証エラーが報告されます。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1　スケーリンググループのVPCサブネット情報を変更します

#### 入力例

```
https://as.tencentcloudapi.com/?Action=ModifyAutoScalingGroup
&AutoScalingGroupId=asg-ka0s0q80
&VpcId=vpc-hy436tmc
&SubnetIds.0=subnet-3tmerl37
&SubnetIds.1=subnet-b0vxjhot
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "RequestId": "c503ddc6-496c-44c9-8cec-e9f1c3f9c11c"
    }
}
```

### 例2　スケーリンググループの目標インスタンス、最大インスタンス数、最小インスタンス数を変更します

#### 入力例

```
https://as.tencentcloudapi.com/?Action=ModifyAutoScalingGroup
&AutoScalingGroupId=asg-ka0s0q80
&DesiredCapacity=3
&MaxSize=10
&MinSize=1
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "RequestId": "b41d8d30-21d4-412c-b7f3-53041879968c"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyAutoScalingGroup)

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
| InvalidParameter.InScenario | 特定のシナリオで不法なパラメータです。 |
| InvalidParameterValue.CvmError | CVMパラメータ検証が異常です。 |
| InvalidParameterValue.GroupNameDuplicate | スケーリンググループの名前が重複しています。 |
| InvalidParameterValue.LaunchConfigurationNotFound | 指定された起動構成が見つかりませんでした。 |
| InvalidParameterValue.LbProjectInconsistent | CLB装置のプロジェクトが一致しません。 |
| InvalidParameterValue.LbVpcInconsistent | CLB装置とスケーリンググループのVPCが一致しません。 |
| InvalidParameterValue.LimitExceeded | 値が制限を超えています。 |
| InvalidParameterValue.OnlyVpc | アカウントはVPCネットワークのみをサポートします。 |
| InvalidParameterValue.Range | 値が指定範囲外です。 |
| InvalidParameterValue.Size | スケーリンググループの最大数、最小数、および目標インスタンス数の値が不正です。 |
| InvalidParameterValue.SubnetIds | サブネット情報が不正です。 |
| InvalidParameterValue.TooLong | 値が多すぎます。 |
| LimitExceeded | 割り当て量の制限を超えています |
| LimitExceeded.MaxSizeLimitExceeded | 最大インスタンス数が制限を超えています。 |
| LimitExceeded.MinSizeLimitExceeded | 最小インスタンス数が制限を下回っています。 |
| MissingParameter | パラメータ欠如エラー |
| MissingParameter.InScenario | 特定のシナリオでパラメータが欠如しています。 |
| ResourceNotFound.AutoScalingGroupIdNotFound | スケーリンググループが存在しません。 |
| ResourceUnavailable.LaunchConfigurationStatusAbnormal | 起動構成のステータスが異常です。 |
| ResourceUnavailable.ProjectInconsistent | プロジェクトが一致しません。 |

