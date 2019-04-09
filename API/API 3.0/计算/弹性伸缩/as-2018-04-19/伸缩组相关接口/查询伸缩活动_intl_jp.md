## 1. API説明

APIリクエストドメイン名：as.tencentcloudapi.com 。

このAPI（DescribeAutoScalingActivities）は、スケーリンググループのスケーリングアクティビティ記録を照合するために使用されます。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：as.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータについては、[共通リクエストパラメータ](/document/api/377/20426)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：DescribeAutoScalingActivities |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-04-19 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| ActivityIds.N | いいえ | Array of String | 1つ以上のスケーリングアクティビティIDで照合します。スケーリングアクティビティIDは`asa-5l2ejpfo`のような形をしています。各リクエストの上限は100です。このパラメータは`ActivityIds`と`Filters`の両方の指定をサポートしません。 |
| Filters.N | いいえ | Array of [Filter](/document/api/377/20453#Filter) | フィルタ条件。<br/><li> auto-scaling-group-id - String - 必須項目：いいえ -（フィルタ条件）スケーリンググループIDでフィルタリングします。</li><li> activity-status-code - String - 必須項目：いいえ -（フィルタ条件）スケーリングアクティビティのステータスでフィルタリングします。（INIT：初期化中&#124;RUNNING：実行中&#124;SUCCESSFUL：アクティビティ成功&#124;PARTIALLY_SUCCESSFUL：アクティビティの一部が成功&#124;FAILED：アクティビティ失敗&#124;CANCELLED：アクティビティキャンセル）</li><li> activity-type - String - 必須項目：いいえ -（フィルタ条件）スケーリングアクティビティのタイプでフィルタリングします。（SCALE_OUT：拡張アクティビティ&#124;SCALE_IN：圧縮アクティビティ&#124;ATTACH_INSTANCES：インスタンス追加&#124;REMOVE_INSTANCES：インスタンス終了&#124;DETACH_INSTANCES：インスタンス除去&#124;TERMINATE_INSTANCES_UNEXPECTEDLY：インスタンスはCVMコンソールで終了されます&#124;REPLACE_UNHEALTHY_INSTANCE：異常なインスタンスを置き換えます&#124;UPDATE_LOAD_BALANCERS：CLB装置をアップデートします）</li><li> activity-id - String - 必須項目：いいえ -（フィルタ条件）スケーリングアクティビティIDでフィルタリングします。</li><br/>各リクエストの`Filters`の上限は10で、`Filter.Values`の上限は5です。このパラメータは`ActivityIds`と`Filters`の両方の指定をサポートしません。 |
| Limit | いいえ | Integer | 返される数、デフォルトは20、最大値は100です。`Limit`の詳細については、API [紹介](https://cloud.tencent.com/document/api/213/15688)の関連セクションを参照してください。 |
| Offset | いいえ | Integer | オフセット、デフォルトは0です。`Offset`の詳細については、API [紹介](https://cloud.tencent.com/document/api/213/15688)の関連セクションを参照してください。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| TotalCount | Integer | 条件を満たすスケーリングアクティビティの数量。|
| ActivitySet | Array of [Activity](/document/api/377/20453#Activity) | 条件を満たすスケーリングアクティビティ情報のセット。|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1　Filtersを使用してスケーリングアクティビティのリストを確認します

#### 入力例

```
https://as.tencentcloudapi.com/?Action=DescribeAutoScalingActivities
&Filters.0.Name=activity-id
&Filters.0.Values.0=asa-o4v87ae9
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "TotalCount": 1,
        "ActivitySet": [
            {
                "Description": "Activity was launched in response to a difference between desired capacity and actual capacity, scale out 1 instance(s).",
                "AutoScalingGroupId": "asg-2umy3jbd",
                "ActivityRelatedInstanceSet": [
                    {
                        "InstanceId": "ins-q3ss14yo",
                        "InstanceStatus": "SUCCESSFUL"
                    }
                ],
                "ActivityType": "SCALE_OUT",
                "ActivityId": "asa-o4v87ae9",
                "StartTime": "2018-11-20T08:33:56Z",
                "CreatedTime": "2018-11-20T08:33:56Z",
                "EndTime": "2018-11-20T08:34:52Z",
                "Cause": "Activity was launched in response to a difference between desired capacity and actual capacity.",
                "StatusMessageSimplified": "Success",
                "StatusMessage": "Success",
                "StatusCode": "SUCCESSFUL"
            }
        ],
        "RequestId": "1082ab5d-c985-4d8c-bb9d-0d05e282b4a7"
    }
}
```

### 例2　スケーリングアクティビティIDに基づいてスケーリングアクティビティのリストを照合します

#### 入力例

```
https://as.tencentcloudapi.com/?Action=DescribeAutoScalingActivities
&ActivityIds.0=asa-o4v87ae9
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "TotalCount": 1,
        "ActivitySet": [
            {
                "Description": "Activity was launched in response to a difference between desired capacity and actual capacity, scale out 1 instance(s).",
                "AutoScalingGroupId": "asg-2umy3jbd",
                "ActivityRelatedInstanceSet": [
                    {
                        "InstanceId": "ins-q3ss14yo",
                        "InstanceStatus": "SUCCESSFUL"
                    }
                ],
                "ActivityType": "SCALE_OUT",
                "ActivityId": "asa-o4v87ae9",
                "StartTime": "2018-11-20T08:33:56Z",
                "CreatedTime": "2018-11-20T08:33:56Z",
                "EndTime": "2018-11-20T08:34:52Z",
                "Cause": "Activity was launched in response to a difference between desired capacity and actual capacity.",
                "StatusMessageSimplified": "Success",
                "StatusMessage": "Success",
                "StatusCode": "SUCCESSFUL"
            }
        ],
        "RequestId": "1082ab5d-c985-4d8c-bb9d-0d05e282b4a7"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeAutoScalingActivities)

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
| InvalidParameter.Conflict | パラメータの競合：指定された複数のパラメータが競合しており、同時に存在することはできません。 |
| InvalidParameterValue.Filter | 無効なフィルタです。 |
| InvalidParameterValue.LimitExceeded | 値が制限を超えています。 |

