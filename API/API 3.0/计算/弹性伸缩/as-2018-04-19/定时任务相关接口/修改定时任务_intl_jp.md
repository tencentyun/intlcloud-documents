## 1. API説明

APIリクエストドメイン名：as.tencentcloudapi.com 。

このAPI（ModifyScheduledAction）は時限タスクを変更するために使用されます。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：as.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータについては、[共通リクエストパラメータ](/document/api/377/20426)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：ModifyScheduledAction |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-04-19 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| ScheduledActionId | はい | String | 変更待ちの時限タスクID |
| ScheduledActionName | いいえ | String | 時限タスク名称。この名前は、中国語、英語、数字、アンダースコア、区切り記号「-」、小数点のみをサポートし、最大長は60バイトを超えることはできません。同じスケーリンググループの下で唯一である必要があります。 |
| MaxSize | いいえ | Integer | 時限タスクがトリガされたとき、設定されたスケーリンググループの最大のインスタンス数。 |
| MinSize | いいえ | Integer | 時限タスクがトリガされたとき、設定されたスケーリンググループの最小のインスタンス数。 |
| DesiredCapacity | いいえ | Integer | 時限タスクがトリガされたとき、設定されたスケーリンググループの希望インスタンス数。 |
| StartTime | いいえ | Timestamp | 時限タスクの初めてのトリガ時間。値は`北京時間`（UTC+8）、`ISO8601`標準に従って、フォーマット：`YYYY-MM-DDThh:mm:ss+08:00`。 |
| EndTime | いいえ | Timestamp | 時限タスクの終了時間。値は`北京時間`（UTC+8）、`ISO8601`標準に従って、フォーマット：`YYYY-MM-DDThh:mm:ss+08:00`。<br>このパラメータは`Recurrence`と同時に指定される必要があります。終了時間に達してから、時限タスクが無効になります。 |
| Recurrence | いいえ | String | 時限タスクの繰り返し方法。標準[Cron](https://zh.wikipedia.org/wiki/Cron)フォーマットです<br>このパラメータは`EndTime`と同時に指定される必要があります。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 時限タスクを変更します

#### 入力例

```
https://as.tencentcloudapi.com/?Action=ModifyScheduledAction
&ScheduledActionId=asst-chwbkq4c
&ScheduledActionName=scheduled-action-0
&MaxSize=5
&MinSize=0
&DesiredCapacity=3
&StartTime=2018-08-28T23:00:00+08:00
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "RequestId": "5f6f0f95-216f-4745-a2e6-617897e9cedb"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyScheduledAction)

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
| InvalidParameterValue.CronExpressionIllegal | 時限タスクによって指定されたCron式が無効です。 |
| InvalidParameterValue.EndTimeBeforeStartTime | 時限タスクの終了時刻は開始時刻より前です。 |
| InvalidParameterValue.InvalidScheduledActionNameIncludeIllegalChar | 時限タスク名に無効な文字が含まれています。 |
| InvalidParameterValue.ScheduledActionNameDuplicate | 時限タスク名が重複しています。 |
| InvalidParameterValue.Size | スケーリンググループの最大数、最小数、および目標インスタンス数の値が不正です。 |
| InvalidParameterValue.StartTimeBeforeCurrentTime | 時限タスクの開始時刻は現在時刻より前です。 |
| InvalidParameterValue.TimeFormat | 時間のフォーマットが間違っています。 |
| InvalidParameterValue.TooLong | 値が多すぎます。 |
| LimitExceeded.DesiredCapacityLimitExceeded | 目標インスタンス数が制限を超えています。 |
| LimitExceeded.MaxSizeLimitExceeded | 最大インスタンス数が制限を超えています。 |
| LimitExceeded.MinSizeLimitExceeded | 最小インスタンス数が制限を下回っています。 |
| LimitExceeded.ScheduledActionLimitExceeded | 時限タスクの数が制限を超えています。 |
| ResourceNotFound.ScheduledActionNotFound | 指定された時限タスクは存在しません。 |

