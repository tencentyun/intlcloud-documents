
## 機能説明

戻り結果の中に Error フィールドが存在する場合、API インターフェースの呼び出しに失敗したことを表します。例えば、次のようになります。

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

Error 内の Code はエラーコードを表し、Message はそのエラーの具体的な情報を表します。

## エラーリストコード

### 共通エラーコード

| エラーコード | 説明 |
|--------|------|
| AuthFailure.InvalidSecretId | 不正なパスワード（クラウド API キータイプではない）。|
| AuthFailure.MFAFailure | MFA エラー。|
| AuthFailure.SecretIdNotFound | キーが存在しません。パスワードが削除されていたり、使用禁止になっていないかコンソールで確認してください。ステータスが正常であった場合、キーが正確に入力されているか確認してください。前後にスペースがないようにします。|
| AuthFailure.SignatureExpire | 署名が期限切れです。Timestamp とサーバの時間差は、5分を超えることはできません。ローカルの時間が標準時間と同期されているか確認してください。|
| AuthFailure.SignatureFailure | 署名エラー。署名計算エラーの場合、呼び出し方式のインターフェース認証ドキュメントと比較して、署名計算プロセスを確認してください。|
| AuthFailure.TokenFailure | token エラー。|
| AuthFailure.UnauthorizedOperation | CAM 権限設定がリクエストされていません。|
| DryRunOperation | DryRun 操作。リクエストが成功する見込みであり、DryRun パラメータを多く伝達しただけであることを表します。|
| FailedOperation | 操作に失敗しました。|
| InternalError | 内部エラー。|
| InvalidAction | インターフェースが存在しません。|
| InvalidParameter | パラメータエラー。|
| InvalidParameterValue | パラメータ取得値エラー。|
| LimitExceeded | 割り当て制限超過。|
| MissingParameter | パラメータが見つからないエラー。|
| NoSuchVersion | インターフェースのバージョンが存在しません。|
| RequestLimitExceeded | リクエストの回数が頻度制限を超えました。|
| ResourceInUse | リソースが占用されています。|
| ResourceInsufficient | リソースが不足しています。|
| ResourceNotFound | リソースが存在しません。|
| ResourceUnavailable | リソースを使用できません。|
| UnauthorizedOperation | 許可されていない操作です。|
| UnknownParameter | 未知のパラメータエラーです。|
| UnsupportedOperation | 操作がサポートされていません。|
| UnsupportedProtocol | http(s)リクエストのプロトコルエラーです。GET および POST リクエストのみサポートしています。|
| UnsupportedRegion | インターフェースは送信するリージョンをサポートしていません。|

### サービスエラーコード



| エラーコード | 説明 |
|:-------|:-----|
| FailedOperation.SystemError | 内部システムエラー。サービスには関係ありません。|
| FailedOperation.Unknown | weekday入力無効データです。|
| InternalError.DbOperationFailed | システムの DB 操作エラー。update insert select..とすることができます。|
| InvalidParameter | パラメータエラー |
| InvalidParameter.EmptyParam | パラメータは空です。|
| InvalidParameter.InvalidParameter | サービスパラメータエラー。|
| InvalidParameter.OnlyVPCOnSpecZoneId |上海金融はvpcネットワークのみ提供します。|
| InvalidParameterValue.InvalidInstanceTypeId | 購入をリクエストしたインスタンスタイプのエラー（TypeId 1:クラスタ版、2:マスタースレーブ版すなわち旧マスタースレーブ版)。|
| InvalidParameterValue.InvalidSubnetId | vpcネットワークにおいて、vpcid サブネットワークid は不正です。|
| InvalidParameterValue.MemSizeNotInRange | 求める容量が販売する容量の範囲内にありません。|
| InvalidParameterValue.PasswordEmpty | パスワードが空です。|
| InvalidParameterValue.PasswordError | パスワードの検証エラー、パスワードエラー。|
| InvalidParameterValue.PasswordRuleError | パスワードを設定した場合、MC が送信する old password が以前に設定したパスワードと異なります。|
| InvalidParameterValue.ReduceCapacityNotAllowed | リクエストする容量が小さすぎるため、容量縮小ができません。|
| InvalidParameterValue.WeekDaysIsInvalid | weekday入力無効データです。|
| LimitExceeded.InvalidMemSize | 求める容量が販売仕様にありません（memSizeは1024の整数倍で、単位はMBです）。|
| LimitExceeded.InvalidParameterGoodsNumNotInRange | 1回で購入をリクエストするインスタンス数が、販売数の制限範囲内にありません。|
| LimitExceeded.PeriodExceedMaxLimit | 購入期間が3年を超えており、リクエスト期間が最長期間を超えています。|
| LimitExceeded.PeriodLessThanMinLimit | 購入期間が不正です。期間は最短1か月です。|
| ResourceInUse.InstanceBeenLocked | インスタンスはその他のプロセスによってロックされています。|
| ResourceNotFound.AccountDoesNotExists | uin 値が空です。|
| ResourceNotFound.InstanceNotExists | serialId に基づいて対応する redis が見つかりません。|
| ResourceUnavailable.AccountBalanceNotEnough | リクエストする発注番号が存在しません。|
| ResourceUnavailable.InstanceDeleted | インスタンスがリサイクル済みです。|
| ResourceUnavailable.InstanceLockedError | redis が既にその他のプロセスによってロックされています。|
| ResourceUnavailable.InstanceStatusAbnormal | redis の状態が異常です。対応するプロセスを実行できません。|
| ResourceUnavailable.NoRedisService | リクエストしたエリアでは、リクエストしたタイプのredisサービスを提供していません。|
| ResourceUnavailable.NoTypeIdRedisService | リクエストしたエリアでは、リクエストしたタイプのredisサービスを提供していません。|
| UnauthorizedOperation | 許可されていない操作です。|
| UnauthorizedOperation.NoCAMAuthed | cam 権限なし。|
| UnauthorizedOperation.UserNotInWhiteList | ユーザーがホワイトリストにありません。|
| UnsupportedOperation.ClusterInstanceAccessedDeny | redis クラスタ版は、セキュリティグループへの接続を許可されません。|
| UnsupportedOperation.IsAutoRenewError | 自動更新識別エラー。|
| UnsupportedOperation.OnlyClusterInstanceCanExportBackup | クラスタ版インスタンスのみ、バックアップのエクスポートをサポートします。|

