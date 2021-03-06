## 1. API説明

APIリクエストドメイン名： cdb.tencentcloudapi.com 。

該当API（ModifyAccountPrivileges）はデータベースのアカウントの権限情報の変更に使用されます。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：cdb.ap-shanghai-fsi.tencentcloudapi.com 。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/236/15833)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、該当APIの値：ModifyAccountPrivileges |
| Version | はい | String | 共通パラメータ、該当APIの値：2017/03/20 |
| Region | はい | String | 共通パラメータ。詳細について製品がサポートする[地域リスト](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| InstanceId | はい | String | インスタンスID、フォーマット：cdb-c1nl9rpv、データベースコンソールページに表示するインスタンスIDと同じです。 |
| Accounts.N | はい | Array of [Account](https://cloud.tencent.com/document/api/236/15878#Account) | ユーザー名とドメイン名を含むデータベースのアカウント。 |
| GlobalPrivileges.N | いいえ | Array of String | グローバル権限。その中、GlobalPrivilegesの権限の選択可能な値：「SELECT」、「INSERT」、「UPDATE」、「DELETE」、「CREATE」「DROP」、「REFERENCES」、「INDEX」、「ALTER」、「SHOW DATABASES」、「CREATE TEMPORARY TABLES」、「LOCK TABLES」、「EXECUTE」、「CREATE VIEW」、「SHOW VIEW」、「CREATE ROUTINE」、「ALTER ROUTINE」、「EVENT」、「TRIGGER」。 |
| DatabasePrivileges.N | いいえ | Array of [DatabasePrivilege](https://cloud.tencent.com/document/api/236/15878#DatabasePrivilege) | データベースの権限。Privileges権限の選択可能な値：「SELECT」、「INSERT」、「UPDATE」、「DELETE」、「CREATE」、「DROP」、「REFERENCES」、「INDEX」、「ALTER」、「CREATE TEMPORARY TABLES」、「LOCK TABLES」、「EXECUTE」、「CREATE VIEW」、「SHOW VIEW」、「CREATE ROUTINE」、「ALTER ROUTINE」、「EVENT」、「TRIGGER」。 |
| TablePrivileges.N | いいえ | Array of [TablePrivilege](https://cloud.tencent.com/document/api/236/15878#TablePrivilege) | データベース中のテーブルの権限。Privileges権限の選択可能な値：「SELECT」、「INSERT」、「UPDATE」、「DELETE」、「CREATE」、「DROP」、「REFERENCES」、「INDEX」、「ALTER」、「CREATE VIEW」、「SHOW VIEW」「TRIGGER」。 |
| ColumnPrivileges.N | いいえ | Array of [ColumnPrivilege](https://cloud.tencent.com/document/api/236/15878#ColumnPrivilege) | データベーステーブルの列の権限。Privileges権限の選択可能な値：「SELECT」、「INSERT」、「UPDATE」、「REFERENCES」。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| AsyncRequestId | String | 非同期タスクのリクエストID。このIDで非同期タスクの実行結果を照合できます。|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 データベースインスタンスアカウントの権限を変更する

#### 入力例

```
https://cdb.tencentcloudapi.com/?Action=ModifyAccountPrivileges
&InstanceId=cdb-f35wr6wj
&Accounts.0.user=ajnnw
&GlobalPrivileges.0=SELECT
&Accounts.0.host=127.0.0.1
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "AsyncRequestId":"256117ed-efa08b54-61784d44-91781bbd"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=ModifyAccountPrivileges)

### SDK

クラウドAPI 3.0は、API呼び出しを容易にするために複数のプログラミング言語をサポートする、関連開発ツールセット（SDK）を提供します。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. エラーコード

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](https://cloud.tencent.com/document/api/236/15835#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| FailedOperation.StatusConflict | タスク状態競合。 |
| InvalidParameter | パラメータエラー。 |
| InvalidParameter.InstanceNotFound | インスタンスが存在しません。 |

