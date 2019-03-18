### API説明
このAPI（GetSAMLProvider）は、特定のSAML IDプロバイダーの詳細情報を照合するために使用されます。
リクエストドメイン名：cam.api.qcloud.com

### 入力パラメータ
以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、他の共通パラメータのリストについては、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/15692)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| name | はい | String | SAML IDプロバイダー名 |

### 出力パラメータ
| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
|ownerUin　|Integer|Tencent CloudアカウントID|
|name　|String |IDプロバイダーの名称|
|desc　|String |IDプロバイダーの説明|
|createTime|Date|IDプロバイダーの作成時間|
|modifyTime　|Date| IDプロバイダーの最終変更時間　|
|SAMLMetadata　|String|SAML IDプロバイダーのメタデータドキュメント|

### 例

IdPという名前のSAML IDプロバイダーの詳細情報を照合します。

##### 入力例：

```
https://cam.api.qcloud.com/v2/index.php?Action=GetSAMLProvider
&name=idp
&<共通リクエストパラメータ>
```
##### 出力例：

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "ownerUin": 798950673,
        "name": "idp",
        "desc": "SAML IDプロバイダー",
        "createTime": "2018-10-30 14:43:37",
        "modifyTime": "2018-10-30 14:50:39",
        "SAMLMetadata": "U0FNTE1ldGFkYXRh"
    }
}
```

### エラーコード

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](https://cloud.tencent.com/document/api/213/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。
