### API説明
このAPI（UpdateSAMLProvider）は、SAML IDプロバイダーの説明またはメタデータドキュメントをアップデートするために使用されます。
リクエストドメイン名：cam.api.qcloud.com
リクエスト方法：HTTP POST

### 入力パラメータ
以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、他の共通パラメータのリストについては、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/15692)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| name | はい | String | SAML IDプロバイダー名 |
| desc | いいえ | String | IDプロバイダーの説明 |
| SAMLMetadataDocument | いいえ | String | SAML IDプロバイダーメタデータドキュメント。Base64でエンコードされている必要があり、最大64KBをサポートします。 |

備考：IdPメタデータドキュメントが上限を超えた場合は、メタデータXMLドキュメント内のIDPSSODescriptor以外の他のXMLノードを削除できます。

### 出力パラメータ

なし。


### 例

IdPという名前のSAML IDプロバイダーの説明およびメタデータドキュメントをアップデートします。

##### 入力例：

```
POST /v2/index.php HTTP/1.1
Host: cam.api.qcloud.com
Accept: */*
Content-Length: 3927
Content-Type: application/x-www-form-urlencoded

Action=UpdateSAMLProvider&name=idp&SAMLMetadataDocument=U0FNTE1ldGFkYXRhRG9jdW1lbnQgdjI=&desc=descriptor2&<共通リクエストパラメータ>
```
##### 出力例：

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": [
    ]
}
```

### エラーコード

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](https://cloud.tencent.com/document/api/213/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| InvalidParameter.ProviderNotExist| IDプロバイダーが存在しません |
| InvalidParameter.SAMLMetadataDocument | SAML IDプロバイダーメタデータドキュメントエラー |
