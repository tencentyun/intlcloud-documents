## 1. インターフェースについて

インターフェースのリクエストドメイン名：redis.tencentcloudapi.com 。

自動バックアップの時間を設定します

初期設定の状態では、インターフェースのリクエスト頻度は20回/秒に制限されています。

注意：このインターフェースは、金融エリアのリージョンに対応しています。金融エリアとそれ以外のエリアは隔てられているため、相互運用ができません。そのため、共通パラメータの Region が金融エリアのリージョン（ap-shanghai-fsi など）である場合、同時に金融エリアのリージョンを持つドメイン名を指定する必要があります。最も良いのは、redis.ap-shanghai-fsi.tencentcloudapi.com のように Region のエリアと一致させることです。



## 2. パラメータ入力

以下のリクエストパラメータリストは、インターフェースリクエストパラメータと一部の共通パラメータのみを表しています。完全な共通パラメータのリストは、[共通のリクエストパラメータ](/document/api/239/20005)を参照してください。

| パラメータ名 | 選択必須 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | 要 | String | 共通パラメータ。本インターフェースの値：ModifyAutoBackupConfig |
| Version | 要 | String | 共通パラメータ。本インターフェースの値：2018-04-12 |
| Region | 要 | String | 共通パラメータ。製品がサポートする[リージョンリスト](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。|
| InstanceId | 要 | String | インスタンスID |
| WeekDays.N | 要 | Array of String | 日時 Monday，Tuesday，Wednesday，Thursday，Friday，Saturday，Sunday |
| TimePeriod | 要 | String | 時間帯 00:00-01:00, 01:00-02:00...... 23:00-00:00 |
| AutoBackupType | 不要 | Integer | 自動バックアップタイプ：1 “定時復旧”|

## 3. パラメータ出力

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| AutoBackupType | Integer | 自動バックアップタイプ：1 “定時復旧”|
| WeekDays | Array of String | 日時Monday，Tuesday，Wednesday，Thursday，Friday，Saturday，Sunday。|
| TimePeriod | String | 時間帯 00:00-01:00, 01:00-02:00...... 23:00-00:00|
| RequestId | String | 一意のリクエスト ID。毎回リクエストするごとに戻ります。問題を見つけ出す際、そのリクエストの RequestId を提供する必要があります。|

## 4. サンプル

### サンプル1 リクエストサンプル

#### 入力サンプル

```
https://redis.tencentcloudapi.com/?Action=ModifyAutoBackupConfig
&InstanceId=crs-5a4py64p
&TimePeriod=00%3A00-01%3A00
&AutoBackupType=1
&WeekDays.0=Wednesday
&<共通リクエストパラメータ>
```

#### 出力サンプル

```
{
    "Response": {
        "AutoBackupType": 1,
        "WeekDays": [
            "Wednesday"
        ],
        "TimePeriod": "00:00-01:00",
        "RequestId": "ac750a85-9a55-4a42-a9de-8c2ca1f4ff12"
    }
}
```


## 5. 開発者リソース

### API Explorer

**本ツールはオンライン呼び出し、署名認証、SDK コード生成、高速インターフェース検索などの能力を提供します。クラウド API の使用難易度を大きく下げることができるため、使用することをお勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=ModifyAutoBackupConfig)

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
| FailedOperation.Unknown | weekday入力無効データです。|
| InvalidParameter.InvalidParameter | サービスパラメータエラー。|
| InvalidParameterValue.WeekDaysIsInvalid | weekday入力無効データです。|
| UnauthorizedOperation.NoCAMAuthed | cam 権限なし。|

