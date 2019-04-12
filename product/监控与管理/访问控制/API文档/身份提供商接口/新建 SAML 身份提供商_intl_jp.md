### API説明

このAPI（CreateSAMLProvider）は、SAML IDプロバイダーを作成するために使用されます。
リクエストドメイン名：cam.api.qcloud.com
リクエスト方法：HTTP POST

### 入力パラメータ

以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、他の共通パラメータのリストについては、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/15692)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| name | はい | String | SAML IDプロバイダー名 |
| desc | はい | String | IDプロバイダーの説明 |
| SAMLMetadataDocument | はい | String | SAML IDプロバイダーーメタデータドキュメント。Base64でエンコードする必要があって、最大64KBのデータをサポートします。 |

備考：IdPメタデータドキュメントが上限を超えた場合は、メタデータXMLドキュメント内のIDPSSODescriptor以外の他のXMLノードを削除できます。例えば：

```
<?xml version="1.0" encoding="utf-8"?>
<EntityDescriptor>
	<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
		......
	</IDPSSODescriptor>
</EntityDescriptor>
```

### 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| name | String | SAML IDプロバイダー名 |
| SAMLProviderArn | String | SAML IDプロバイダーの説明情報 |

### 例

IdPという名前のSAML IDプロバイダーを作成します。

##### 入力例：

```
POST /v2/index.php HTTP/1.1
Host: cam.api.qcloud.com
Accept: */*
Content-Length: 3927
Content-Type: application/x-www-form-urlencoded

Action=CreateSAMLProvider&name=idp&SAMLMetadataDocument=U0FNTE1ldGFkYXRhRG9jdW1lbnQ&desc=descriptor&<共通リクエストパラメータ>
```
##### 出力例：

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "name": "idp",
        "SAMLProviderArn": "qcs::cam::uin/798950673:saml-provider/idp"
    }
}

```

### エラーコード
以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](https://cloud.tencent.com/document/api/213/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| InvalidParameter.ProviderAlreadyExist | IDプロバイダーはすでに存在します |
| InvalidParameter. SAMLMetadataDocument | SAML IDプロバイダーメタデータドキュメントエラー |
| InvalidParameter.ProviderMaxLimit | IDプロバイダーが上限に達します |
