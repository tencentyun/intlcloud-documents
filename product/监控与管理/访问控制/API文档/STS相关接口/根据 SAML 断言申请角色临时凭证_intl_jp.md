### API説明
このAPI（AssumeRoleWithSAML）は、SAMLアサーションに基づいてロールの一時的認証情報を申請するために使用されます。
リクエストドメイン名：sts.api.qcloud.com
リクエスト方法：HTTP POST

### 入力パラメータ
以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、他の共通パラメータのリストについては、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/15692)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| SAMLAssertion | はい | String | Base64エンコードのSAMLアサーション情報 |
| PrincipalArn | はい |String|アクターアクセス可能リソース名 |
| RoleArn | はい | String | ロールアクセス可能リソース名 |
| RoleSessionName | はい |String|セッション名 |

### 出力パラメータ
| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
|  credentials | [credentials](#dataStructure)  | オブジェクトにtoken、tmpSecretId、tmpSecretKeyトライアドが含まれています  |
| expiredTime | Integer |証明書の無効時間、秒までの正確なUnixタイムスタンプを返します |
| expiration |String | 証明書の無効時間は、ISO8601フォーマットのUTC時間で表されます |

<span id="dataStructure"></span>
### Credentialsデータ構造

| フィールド  | タイプ  | 説明  |
|---------|---------|---------|
| token | String | token 値 |
| tmpSecretId | String | 一時的セキュリティ証明書ID |
| tmpSecretKey | String | 一時的セキュリティ証明書Key |


### 例
IdPという名前のSAML IDプロバイダーを作成します。

##### 入力例：

``` 
POST /v2/index.php HTTP/1.1
Host: sts.api.qcloud.com
Accept: */*
Content-Length: 3927
Content-Type: application/x-www-form-urlencoded

Action=AssumeRoleWithSAML
&PrincipalArn=qcs::cam::uin/798950673:saml-provider/OneLogin
&RoleArn=qcs::cam::uin/798950673:roleName/OneLogin-Role
&RoleSessionName=test
&SAMLAssertion=c2FtbCBhc3NlcnRpb24=
&<共通リクエストパラメータ>
``` 
##### 出力例：

``` 
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "credentials": {
            "sessionToken": "d154fa74af184dfac3deb3a729c103a3003d52f840001",
            "tmpSecretId": "AKID7byWjIxUdUuRfhuctpd2T7XLpkCeqMub",
            "tmpSecretKey": "LN1yqrCt2oejxQB7AQsL8iP9VE4hzfZ9"
        },
        "expiredTime": 1541594376,
        "expiration": "2018-11-07T12:39:36Z"
    }
}
``` 

### エラーコード

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](https://cloud.tencent.com/document/api/213/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| InvalidParameter.ProviderNotExist | IDプロバイダーはすでに存在します |
| InvalidParameter.SAMLResponse | 無効なSAMLアサーション応答 |
| InvalidParameter.InvalidRoleArn | 無効なロールアクセス可能リソース名 |

