## 1. API説明

APIリクエストドメイン名：as.tencentcloudapi.com 。

このAPI（DescribeScheduledActions）は、1つ以上の時限タスクの詳細情報を照合するために使用されます。

* 時限タスクID、時限タスク名称またはスケーリンググループIDなどの情報に基づいて時限タスクの詳細情報を照合できます。フィルタリング情報の詳細については`Filter`を参照してください。
* パラメータがブランクの場合、現在のユーザーに一定の数量（Limitで指定された数量、デフォルトは20）の時限タスクを返します。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：as.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータについては、[共通リクエストパラメータ](/document/api/377/20426)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：DescribeScheduledActions |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-04-19 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| ScheduledActionIds.N | いいえ | Array of String | 1つ以上の時限タスクIDに従って照合してください。インスタンスIDの形は：asst-am691zxo。毎回リクエストのインスタンスの上限は100です。パラメータはScheduledActionIdsとFiltersの両方の指定をサポートしません。 |
| Filters.N | いいえ | Array of [Filter](/document/api/377/20453#Filter) | フィルタリング条件。<br/><li> scheduled-action-id - String - 必須項目：いいえ -（フィルタリング条件）時限タスクIDに従ってフィルタします。</li><li> scheduled-action-name - String - 必須項目であるか：いいえ - （フィルタリング条件）時限タスク名称に従ってフィルタします。</li><li> auto-scaling-group-id - String - 必須項目であるか：いいえ - （フィルタリング条件）スケーリンググループIDに従ってフィルタします。</li> |
| Offset | いいえ | Integer | オフセット、デフォルトは0です。Offsetの詳細な紹介についてAPI [概要](https://cloud.tencent.com/document/api/213/15688)中の関連セクションを参照してください。 |
| Limit | いいえ | Integer | 返し数量、デフォルトは20で、最大値は100です。Limitの詳細な紹介についてAPI [概要](https://cloud.tencent.com/document/api/213/15688)中の関連セクションを参照してください。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| TotalCount | Integer | 条件を満たすの時限タスク数量。|
| ScheduledActionSet | Array of [ScheduledAction](/document/api/377/20453#ScheduledAction) | 時限タスク詳細情報リスト。|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 時限タスクを照合します

#### 入力例

```
https://as.tencentcloudapi.com/?Action=DescribeScheduledActions
&ScheduledActionIds.0=asst-caa5ha40
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "TotalCount": 1,
        "ScheduledActionSet": [
            {
                "ScheduledActionId": "asst-caa5ha40",
                "ScheduledActionName": "testv2-0",
                "AutoScalingGroupId": "asg-2nr9xh8h",
                "StartTime": "2018-09-28T00:00:00+08:00",
                "Recurrence": "0 0 * * *",
                "EndTime": "2018-09-28T23:59:59+08:00",
                "MaxSize": 10,
                "DesiredCapacity": 0,
                "MinSize": 0,
                "CreatedTime": "2018-09-24T07:41:54Z"
            }
        ]
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeScheduledActions)

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

