## 1. インターフェースについて

インターフェースのリクエストドメイン名：redis.tencentcloudapi.com 。

インスタンス関連情報の変更（現在はインスタンス名の変更のみサポート）

初期設定の状態では、インターフェースのリクエスト頻度は20回/秒に制限されています。

注意：このインターフェースは、金融エリアのリージョンに対応しています。金融エリアとそれ以外のエリアは隔てられているため、相互運用ができません。そのため、共通パラメータの Region が金融エリアのリージョン（ap-shanghai-fsi など）である場合、同時に金融エリアのリージョンを持つドメイン名を指定する必要があります。最も良いのは、redis.ap-shanghai-fsi.tencentcloudapi.com のように Region のエリアと一致させることです。



## 2. パラメータ入力

以下のリクエストパラメータリストは、インターフェースリクエストパラメータと一部の共通パラメータのみを表しています。完全な共通パラメータのリストは、[共通のリクエストパラメータ](/document/api/239/20005)を参照してください。

| パラメータ名 | 選択必須 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | 要 | String | 共通パラメータ。本インターフェースの値：ModifyInstance |
| Version | 要 | String | 共通パラメータ。本インターフェースの値：2018-04-12 |
| Region | 要 | String | 共通パラメータ。製品がサポートする[リージョンリスト](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。|
| Operation | 要 | String | インスタンス変更操作は、rename（インスタンス名変更を表示）のように記載 |
| InstanceId | 不要 | String | インスタンスId |
| InstanceName | 不要 | String | インスタンスの新名称 |

## 3. パラメータ出力

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| RequestId | String | 一意のリクエスト ID。毎回リクエストするごとに戻ります。問題を見つけ出す際、そのリクエストの RequestId を提供する必要があります。|

## 4. サンプル

### サンプル1 リクエストサンプル

#### 入力サンプル

```
https://redis.tencentcloudapi.com/?Action=ModifyInstance
&Operation=rename
&InstanceId=crs-28v6tnn3
&InstanceName=クラスタ版の回帰
&<共通リクエストパラメータ>
```

#### 出力サンプル

```
{
    "Response": {
        "RequestId": "9c1abac4-9e47-4747-ac8a-b7167d96f176"
    }
}
```


## 5. 開発者リソース

### API Explorer

**本ツールはオンライン呼び出し、署名認証、SDK コード生成、高速インターフェース検索などの能力を提供します。クラウド API の使用難易度を大きく下げることができるため、使用することをお勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=ModifyInstance)

### SDK

クラウド API 3.0 は、付属の開発ツールセット（SDK）を提供します。さまざまなプログラミング言語をサポートすることで、より簡単に API を呼び出すことができます。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. エラーコード

以下では、インターフェースのサービスロジックに関連するエラーコードのみを示します。その他のエラーコードについては[共通エラーコード](/document/api/239/20007#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)をご覧ください。

| エラーコード | 説明 |
|---------|---------|
| FailedOperation.SystemError | 内部システムエラー。サービスには関係ありません。|
| UnauthorizedOperation | 許可されていない操作です。|
| UnauthorizedOperation.NoCAMAuthed | cam 権限なし。|
| UnauthorizedOperation.UserNotInWhiteList | ユーザーがホワイトリストにありません。|
| UnsupportedOperation.ClusterInstanceAccessedDeny | redis クラスタ版は、セキュリティグループへの接続を許可されません。|
| UnsupportedOperation.IsAutoRenewError | 自動更新識別エラー。|
| UnsupportedOperation.OnlyClusterInstanceCanExportBackup | クラスタ版インスタンスのみ、バックアップのエクスポートをサポートします。|

