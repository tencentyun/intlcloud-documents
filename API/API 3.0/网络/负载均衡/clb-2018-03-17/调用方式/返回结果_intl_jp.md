## 正しい戻り結果

CVM APIのインスタンスステータスリスト表示（DescribeInstancesStatus）2017-03-12のバージョンを例として、呼び出しに成功すれば、以下のように返すことができます。

    {
        "Response": {
            "TotalCount": 0,
            "InstanceStatusSet": [],
            "RequestId": "b5b41468-520d-4192-b42f-595cc34b6c1c"
        }
    }

* ResponseおよびそのRequestIdは固定的なフィールドです。リクエストが成功したかどうかに関わらず、APIが処理されている限り、必ず戻り結果があります。
* RequestIdは1つのAPIリクエストの唯一のIDです。APIに異常が発生した場合、こちらに連絡して問題を解決するためのIDを提供してください。
* 固定のフィールドを除き、残りは具体的なAPIで定義するフィールドです。異なるAPIで返したフィールドについては、APIドキュメントの定義を参照してください。この例では、TotalCountとInstanceStatusSetは両方ともDescribeInstancesStatus APIで定義したフィールドです。リクエストを呼び出すユーザーはまだCVMインスタンスを持っていないため、TotalCountのこの場合での戻し値は0で、InstanceStatusSetリストは空白です。

## 間違った戻り結果

呼び出しに失敗すれば、その戻り値の例は以下のとおりです：

    {
        "Response": {
            "Error": {
                "Code": "AuthFailure.SignatureFailure",
                "Message": "The provided credentials could not be validated. Please check your signature is correct."
            },
            "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
        }
    }

* Errorの発生はこのリクエストの呼び出しが失敗したことを示します。Errorフィールドおよびその内部のCodeとMessageフィールドは、呼び出しに失敗した場合、必ず戻り値があります。
* Codeは具体なエラーコードを示します。リクエストがエラーになった場合、まずこのエラーコードに基づいて、共通エラーコードと現在のAPIに対応するエラーコードリストで対応する原因とソリューションを確認できます。
* Messageはこのエラーの具体的な原因を示します。業務の発展と体験の最適化につれて、このテキストは常に変更またはアップデートされる可能性があるため、必ずこの戻り値とは限りません。
* RequestIdは1つのAPIリクエストの唯一のIDです。APIに異常が発生した場合、こちらに連絡して問題を解決するためのIDを提供してください。


## 共通エラーコード


戻り結果にErrorフィールドが存在すれば、APIの呼び出しが失敗したと示します。ErrorのCodeフィールドはエラーコードを示します。すべての業務で発生する可能性があるエラーコードは、共通エラーコードです。下記のテーブルで共通エラーコードをリストします。


| エラーコード | エラー説明 |
|----------|----------|
| AuthFailure.InvalidSecretId | 暗号鍵が不正です（クラウドAPI暗号鍵タイプではありません）。 |
| AuthFailure.MFAFailure | MFAエラー。 |
| AuthFailure.SecretIdNotFound | 暗号鍵が存在しません。 |
| AuthFailure.SignatureExpire | 署名期限切れ。 |
| AuthFailure.SignatureFailure | 署名エラー。 |
| AuthFailure.TokenFailure | トークンエラー。 |
| AuthFailure.UnauthorizedOperation | リクエストはCAMに承認されていません。 |
| DryRunOperation | DryRun操作。リクエストが成功するが、余計なDryRunパラメータが渡されます。 |
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
| ResourceUnavailable | リソースが利用できません。 |
| UnauthorizedOperation | 操作が承認されていません。 |
| UnknownParameter | 不明なパラメータエラー。 |
| UnsupportedOperation | 操作はサポートされません。 |
| UnsupportedProtocol | http(s)リクエストプロトコルエラー。GETとPOSTリクエストのみサポートされます。 |
| UnsupportedRegion | APIは渡された地域をサポートしません。 |

