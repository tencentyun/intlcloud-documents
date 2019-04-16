### API説明

このAPI（DeleteSAMLProvider）は、SAML IDプロバイダーを削除するために使用されます。
リクエストドメイン名：cam.api.qcloud.com

### 入力パラメータ

以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、他の共通パラメータのリストについては、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/15692)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| name | はい | String | SAML IDプロバイダーの名称|

### 出力パラメータ

なし。


### 例

IdPという名前のSAML IDプロバイダーを削除します

##### 入力例：

```
https://cam.api.qcloud.com/v2/index.php?Action=DeleteSAMLProvider
&name=idp
&<共通リクエストパラメータ>
```

##### 出力例：

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": []
}
```

### エラーコード

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](https://cloud.tencent.com/document/api/213/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| InvalidParameter.ProviderNotExist | IDプロバイダーが存在しません|
