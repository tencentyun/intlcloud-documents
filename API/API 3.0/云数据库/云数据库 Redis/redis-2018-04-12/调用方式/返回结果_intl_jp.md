## 正確な戻り結果

例えば、CVM のインターフェースでインスタンスのステータスリスト(DescribeInstancesStatus) 2017-03-12 バージョンを確認する場合、呼び出しに成功すると以下のように返されることが考えられます。

    {
        "Response": {
            "TotalCount": 0,
            "InstanceStatusSet": [],
            "RequestId": "b5b41468-520d-4192-b42f-595cc34b6c1c"
        }
    }

* Response 及びその内部の RequestId は固定のフィールドです。リクエストの成否に関わらず API 処理さえすれば必ず返されます。
* RequestId は API リクエストに使用される一意の識別子です。API に異常が発生した場合は弊社に連絡し、該当するID を提供して問題を解決します。
* 固定されたフィールドを除き、その他はいずれも具体的なインターフェースが定義したフィールドです。異なるインターフェースが返すフィールドについては、インターフェースドキュメントの定義を参照してください。この例の TotalCount と InstanceStatusSet は、いずれも DescribeInstancesStatus インターフェースが定義するフィールドです。リクエストを呼び出すユーザーはこの時まだ CVM インスタンスがないため、 TotalCount のこの状況においける戻り値は 0であり、 InstanceStatusSet リストは空になります。

## エラー戻り結果

呼び出しに失敗した場合、その戻り値は以下の通りです。

    {
        "Response": {
            "Error": {
                "Code": "AuthFailure.SignatureFailure",
                "Message": "The provided credentials could not be validated. Please check your signature is correct."
            },
            "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
        }
    }

* Error の発生は、そのリクエストの呼び出しに失敗したことを表します。Error フィールドは、その内部の Code および Message フィールドと併せて、呼び出しに失敗すると必ず返されます。
* Code は具体的に誤りのあるエラーコードを表しています。リクエストにエラーがあった場合、まずそのエラーコードをもとに、共通エラーコードと現在のインターフェースに対応するエラーコードリストから対応する原因と解決方法を調査することができます。
* Message はこのエラーが発生した具体的な原因を示しています。サービスの展開や体験の最適化に従い、このテキストは継続的に変更または更新されることがあります。ユーザーはこの戻り値に依存するべきではありません。
* RequestId は API リクエストに使用される一意の識別子です。API に異常が発生した場合は弊社に連絡し、該当するID を提供して問題を解決します。


## 共通エラーコード


戻り結果の中に Error フィールドが存在する場合、API インターフェースの呼び出しに失敗したことを表します。Error 内の Code フィールドがエラーコードを示している場合、全てのサービスで発生する可能性のあるエラーコードは共通エラーコードです。以下の表に共通エラーコードを示します。


| エラーコード | エラーの説明 |
|----------|----------|
| AuthFailure.InvalidSecretId | 不正なパスワード（クラウド API キータイプではない）。|
| AuthFailure.MFAFailure | MFA エラー。|
| AuthFailure.SecretIdNotFound | キーが存在しません。|
| AuthFailure.SignatureExpire | 署名が期限切れです。|
| AuthFailure.SignatureFailure | 署名エラー。|
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

