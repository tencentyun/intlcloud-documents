
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

### 共通エラーコード

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
| InternalError.AsyncRequestError | 非同期タスクの照合エラー。 |
| InvalidParameter | パラメータエラー |

