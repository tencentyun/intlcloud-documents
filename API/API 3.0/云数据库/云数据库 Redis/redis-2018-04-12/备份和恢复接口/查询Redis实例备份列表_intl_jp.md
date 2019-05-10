## 1. インターフェースについて

インターフェースのリクエストドメイン名：redis.tencentcloudapi.com 。

CRS インスタンスバックアップリストの照会

初期設定の状態では、インターフェースのリクエスト頻度は20回/秒に制限されています。

注意：このインターフェースは、金融エリアのリージョンに対応しています。金融エリアとそれ以外のエリアは隔てられているため、相互運用ができません。そのため、共通パラメータの Region が金融エリアのリージョン（ap-shanghai-fsi など）である場合、同時に金融エリアのリージョンを持つドメイン名を指定する必要があります。最も良いのは、redis.ap-shanghai-fsi.tencentcloudapi.com のように Region のエリアと一致させることです。



## 2. パラメータ入力

以下のリクエストパラメータリストは、インターフェースリクエストパラメータと一部の共通パラメータのみを表しています。完全な共通パラメータのリストは、[共通のリクエストパラメータ](/document/api/239/20005)を参照してください。

| パラメータ名 | 選択必須 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | 要 | String | 共通パラメータ。本インターフェースの取得値：DescribeInstanceBackups |
| Version | 要 | String | 共通パラメータ。本インターフェースの値：2018-04-12 |
| Region | 要 | String | 共通パラメータ。製品がサポートする[リージョンリスト](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。|
| InstanceId | 要 | String | 操作待ちのインスタンスID。DescribeInstance インターフェースの戻り値における InstanceId を介して取得できます。|
| Limit | 不要 | Integer | インスタンスリストのサイズ。デフォルトで20です |
| Offset | 不要 | Integer | オフセット量。Limit の整数倍を取ります |
| BeginTime | 不要 | String | 開始時間。2017-02-08 16:46:34の形式です。インスタンスが [beginTime, endTime] の時間帯でバックアップを開始するバックアップリストを照会します。|
| EndTime | 不要 | String | 終了時間。2017-02-08 19:09:26の形式です。インスタンスが [beginTime, endTime] の時間帯でバックアップを開始するバックアップリストを照会します。|
| Status.N | 不要 | Array of String | 1：バックアッププロセス中、2：バックアップ正常、3：バックアップをRDBファイルに変換処理中、4：RDB変換が完了済み、-1：バックアップ期限切れ、-2：バックアップ削除済み。|

## 3. パラメータ出力

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| TotalCount | Integer | バックアップ総数|
| BackupSet | Array of [RedisBackupSet](/document/api/239/20022#RedisBackupSet) | インスタンスのバックアップ配列|
| RequestId | String | 一意のリクエスト ID。毎回リクエストするごとに戻ります。問題を見つけ出す際、そのリクエストの RequestId を提供する必要があります。|

## 4. サンプル

### サンプル1 リクエストサンプル

#### 入力サンプル

```
https://redis.tencentcloudapi.com/?Action=DescribeInstanceBackups
&Limit=5&Offset=0
&InstanceId=crs-5a4py64p
&<共通リクエストパラメータ>
```

#### 出力サンプル

```
{
    "Response": {
        "RequestId": "2d4387ee-2011-449e-a32b-87f9366f3ef4",
        "TotalCount": 2,
        "RedisBackupSet": [
            {
                "StartTime": "2018-09-04 12:51:21",
                "BackupId": "2e4127f8-affe-11e8-941e-4846fb00c75d",
                "BackupType": "0",
                "Status": 2,
                "Remark": "テスト使用",
                "Locked": 0
            },
            {
                "StartTime": "2018-09-04 12:53:06",
                "BackupId": "6cbbf53a-affe-11e8-905b-4846fb00c75d",
                "BackupType": "0",
                "Status": 2,
                "Remark": "xxx",
                "Locked": 0
            }
        ]
    }
}
```


## 5. 開発者リソース

### API Explorer

**本ツールはオンライン呼び出し、署名認証、SDK コード生成、高速インターフェース検索などの能力を提供します。クラウド API の使用難易度を大きく下げることができるため、使用することをお勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeInstanceBackups)

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
| InvalidParameter.InvalidParameter | サービスパラメータエラー。|
| UnauthorizedOperation.NoCAMAuthed | cam 権限なし。|

