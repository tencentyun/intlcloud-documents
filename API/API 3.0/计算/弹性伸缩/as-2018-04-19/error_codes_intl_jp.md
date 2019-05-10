
## 機能説明

戻り結果にはErrorフィールドが存在すれば、APIの呼び出しが失敗したと示します。例：

```
 {
    "Response": {
        "Error": {
            "Code": "AuthFailure.SignatureFailure",
            "Message": "The provided credentials could not be validated. Please check your signature is correct."
        },
        "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
    }
}
```

ErrorのCodeはエラーコードを示します。Messageは該当エラーの具体的な情報を示します。

## エラーコードリスト

###　共通エラーコード

| エラーコード | 説明 |
|--------|------|
| AuthFailure.InvalidSecretId | 暗号鍵が不正です（クラウドAPI暗号鍵タイプではありません）。 |
| AuthFailure.MFAFailure | MFAエラー |
| AuthFailure.SecretIdNotFound | 暗号鍵が存在しません。コンソールで暗号鍵が削除されたか、無効にされたかを確認してください。状態が正常の場合、暗号鍵が正しく入力されたかどうかを確認してください。前後にスペースを入れないことにご注意ください。|
| AuthFailure.SignatureExpire | 署名期限切れ。Timestampとサーバー時間の差は5分を超えてはいけませんので、ローカル時間は標準時間と一致するかどうかを確認してください。|
| AuthFailure.SignatureFailure | 署名エラー。署名計算エラー、呼び出し方法にあるAPI認証ドキュメントを参照して、署名計算プロセスを確認してください。|
| AuthFailure.TokenFailure | トークンエラー。 |
| AuthFailure.UnauthorizedOperation | リクエストはCAMに承認されていません。 |
| DryRunOperation | DryRun操作。リクエストが成功しますが、余計なDryRunパラメータが渡されます。 |
| FailedOperation | 操作失敗。 |
| InternalError | 内部エラー。 |
| InvalidAction | APIが存在しません。 |
| InvalidParameter | パラメータエラー。 |
| InvalidParameterValue | パラメータ値エラー。 |
| LimitExceeded | 割り当て量の制限を超えました。 |
| MissingParameter | パラメータ欠如エラー。 |
| NoSuchVersion | APIバージョンが存在しません。 |
| RequestLimitExceeded | リクエスト回数は頻度の制限を超えました。 |
| ResourceInUse | リソースが占有されています。 |
| ResourceInsufficient | リソースが足りません。 |
| ResourceNotFound | リソースが存在しません。 |
| ResourceUnavailable | リソースが使用できません。 |
| UnauthorizedOperation | 操作が承認されていません。 |
| UnknownParameter | 不明なパラメータエラー。 |
| UnsupportedOperation | 操作はサポートされません。 |
| UnsupportedProtocol | http(s)リクエストプロトコルエラー、GETとPOSTリクエストのみサポートされます。 |
| UnsupportedRegion | APIは渡された地域をサポートしません。 |

### 業務エラーコード

| エラーコード | 説明 |
|:-------|:-----|
| AccountQualificationRestrictions | このリクエストアカウントは資格審査に合格しませんでした。 |
| CallCvmError | CVM APIの呼び出しが失敗しました。 |
| InternalError | 内部エラー |
| InvalidFilter | 無効なフィルタです。 |
| InvalidImageId.NotFound | このイメージが見つかりませんでした。 |
| InvalidLaunchConfiguration | 無効な起動構成です。 |
| InvalidLaunchConfiguration.NameDuplicate | 起動構成名が重複しています。 |
| InvalidLaunchConfigurationId | 起動構成IDが無効です。 |
| InvalidLaunchConfigurationId.InUse | 起動構成は使用中です。 |
| InvalidLaunchConfigurationId.NotFound | この起動構成が見つかりませんでした。 |
| InvalidParameter.Conflict | パラメータの競合：指定された複数のパラメータが競合しており、同時に存在することはできません。 |
| InvalidParameter.InScenario | 特定のシナリオで不法なパラメータです。 |
| InvalidParameter.MustOneParameter | パラメーターが欠落しており、2つのパラメータのいずれかを指定する必要があります。 |
| InvalidParameterConflict | 指定された2つのパラメータが競合しており、同時に存在することはできません。 |
| InvalidParameterValue.CronExpressionIllegal | 時限タスクによって指定されたCron式が無効です。 |
| InvalidParameterValue.CvmConfigurationError | CVMパラメータ検証が異常です。 |
| InvalidParameterValue.CvmError | CVMパラメータ検証が異常です。 |
| InvalidParameterValue.EndTimeBeforeStartTime | 時限タスクの終了時刻は開始時刻より前です。 |
| InvalidParameterValue.Filter | 無効なフィルタです。 |
| InvalidParameterValue.ForwardLb | アプリケーション型CLB装置を誤って指定しました。 |
| InvalidParameterValue.GroupNameDuplicate | スケーリンググループの名前が重複しています。 |
| InvalidParameterValue.InvalidScheduledActionNameIncludeIllegalChar | 時限タスク名に無効な文字が含まれています。 |
| InvalidParameterValue.LaunchConfigurationNotFound | 指定された起動構成が見つかりませんでした。 |
| InvalidParameterValue.LbProjectInconsistent | CLB装置のプロジェクトが一致しません。 |
| InvalidParameterValue.LbVpcInconsistent | CLB装置とスケーリンググループのVPCが一致しません。 |
| InvalidParameterValue.LimitExceeded | 値が制限を超えています。 |
| InvalidParameterValue.OnlyVpc | アカウントはVPCネットワークのみをサポートします。 |
| InvalidParameterValue.Range | 値が指定範囲外です。 |
| InvalidParameterValue.ScheduledActionNameDuplicate | 時限タスク名が重複しています。 |
| InvalidParameterValue.Size | スケーリンググループの最大数、最小数、および目標インスタンス数の値が不正です。 |
| InvalidParameterValue.StartTimeBeforeCurrentTime | 時限タスクの開始時刻は現在時刻より前です。 |
| InvalidParameterValue.SubnetIds | サブネット情報が不正です。 |
| InvalidParameterValue.TimeFormat | 時間のフォーマットが間違っています。 |
| InvalidParameterValue.TooLong | 値が多すぎます。 |
| InvalidPermission | この操作はアカウントではサポートされていません。 |
| LaunchConfigurationQuotaLimitExceeded | 起動構成の割り当て量が制限を超えています。 |
| LimitExceeded | 割り当て量の制限を超えています |
| LimitExceeded.AutoScalingGroupLimitExceeded | スケーリンググループの数が制限を超えています。 |
| LimitExceeded.DesiredCapacityLimitExceeded | 目標インスタンス数が制限を超えています。 |
| LimitExceeded.MaxSizeLimitExceeded | 最大インスタンス数が制限を超えています。 |
| LimitExceeded.MinSizeLimitExceeded | 最小インスタンス数が制限を下回っています。 |
| LimitExceeded.ScheduledActionLimitExceeded | 時限タスクの数が制限を超えています。 |
| MissingParameter | パラメータ欠如エラー |
| MissingParameter.InScenario | 特定のシナリオでパラメータが欠如しています。 |
| ResourceInUse.ActivityInProgress | スケーリンググループはスケーリングアクティビティを実行しています。 |
| ResourceInUse.InstanceInGroup | スケーリンググループにはまだ正常的なインスタンスがあります。 |
| ResourceInsufficient.AutoScalingGroupAboveMaxSize | スケーリンググループの最大インスタンス数を超えました。 |
| ResourceInsufficient.AutoScalingGroupBelowMinSize | スケーリンググループの最小インスタンス数より少ないです。 |
| ResourceNotFound.AutoScalingGroupIdNotFound | スケーリンググループが存在しません。 |
| ResourceNotFound.InstancesNotFound | 指定されたインスタンスは存在しません。 |
| ResourceNotFound.InstancesNotInAutoScalingGroup | ターゲットインスタンスはスケーリンググループにありません。 |
| ResourceNotFound.LoadBalancerNotFound | 指定されたCLB装置が見つかりませんでした。 |
| ResourceNotFound.ScheduledActionNotFound | 指定された時限タスクは存在しません。 |
| ResourceUnavailable.AutoScalingGroupAbnormalStatus | スケーリンググループのステータスが異常です。 |
| ResourceUnavailable.AutoScalingGroupDisabled | スケーリンググループは使用中止されました。 |
| ResourceUnavailable.AutoScalingGroupInActivity | スケーリンググループはアクティビティ中です。 |
| ResourceUnavailable.CvmVpcInconsistent | インスタンスとスケーリンググループのVPCが一致しません。 |
| ResourceUnavailable.InstancesAlreadyInAutoScalingGroup | インスタンスは既にスケーリンググループに存在します。 |
| ResourceUnavailable.LaunchConfigurationStatusAbnormal | 起動構成のステータスが異常です。 |
| ResourceUnavailable.ProjectInconsistent | プロジェクトが一致しません。 |

