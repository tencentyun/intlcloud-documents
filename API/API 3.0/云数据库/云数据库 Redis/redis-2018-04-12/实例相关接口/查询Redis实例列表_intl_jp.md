## 1. インターフェースについて

インターフェースのリクエストドメイン名：redis.tencentcloudapi.com 。

Redisインスタンスリストを照会する

初期設定の状態では、インターフェースのリクエスト頻度は20回/秒に制限されています。

注意：このインターフェースは、金融エリアのリージョンに対応しています。金融エリアとそれ以外のエリアは隔てられているため、相互運用ができません。そのため、共通パラメータの Region が金融エリアのリージョン（ap-shanghai-fsi など）である場合、同時に金融エリアのリージョンを持つドメイン名を指定する必要があります。最も良いのは、redis.ap-shanghai-fsi.tencentcloudapi.com のように Region のエリアと一致させることです。



## 2. パラメータ入力

以下のリクエストパラメータリストは、インターフェースリクエストパラメータと一部の共通パラメータのみを表しています。完全な共通パラメータのリストは、[共通のリクエストパラメータ](/document/api/239/20005)を参照してください。

| パラメータ名 | 選択必須 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | 要 | String | 共通パラメータ。本インターフェースの値：DescribeInstances |
| Version | 要 | String | 共通パラメータ。本インターフェースの値：2018-04-12 |
| Region | 要 | String | 共通パラメータ。製品がサポートする[リージョンリスト](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。|
| Limit | 不要 | Integer | インスタンスリストのサイズ。パラメータのデフォルト値は20 |
| Offset | 不要 | Integer | オフセット量。Limit の整数倍を取ります |
| InstanceId | 不要 | String | インスタンスId。crs-6ubhgoujのようになります |
| OrderBy | 不要 | String | 列挙する範囲は次の通りです。projectId,createtime,instancename,type,curDeadline |
| OrderType | 不要 | Integer | 1逆順、0順番、デフォルトでは逆順 |
| VpcIds.N | 不要 | Array of String | VPC ID 配列。配列の添え字は0から開始します。送信しない場合は、デフォルトで基本ネットワークを選択します。例：47525 |
| SubnetIds.N | 不要 | Array of String | サブネットワークID配列。配列の添え字は0から開始します。例：56854 |
| ProjectIds.N | 不要 | Array of Integer | プロジェクトID を構成する配列は。配列の添え字は0から開始します |
| SearchKey | 不要 | String | インスタンスのIDを検索します。|
| InstanceName | 不要 | String | インスタンス名 |
| UniqVpcIds.N | 不要 | Array of String | VPC ID の配列。配列の添え字は0から開始します。送信しない場合は、デフォルトで基本ネットワークを選択します。例：vpc-sad23jfdfk |
| UniqSubnetIds.N | 不要 | Array of String | サブネットワーク ID 配列。配列の添え字は0から開始します。例：subnet-fdj24n34j2 |
| RegionIds.N | 不要 | Array of Integer | リージョン ID。既に使用されていない場合、共通パラメータ Region を介して対応するリージョンを照会することができます|

## 3. パラメータ出力

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| TotalCount | Integer | インスタンス数|
| InstanceSet | Array of [InstanceSet](/document/api/239/20022#InstanceSet) | インスタンスの詳細情報リスト|
| RequestId | String | 一意のリクエスト ID。毎回リクエストするごとに戻ります。問題を見つけ出す際、そのリクエストの RequestId を提供する必要があります。|

## 4. サンプル

### サンプル1 リクエストサンプル

#### 入力サンプル

```
https://redis.tencentcloudapi.com/?Action=DescribeInstances
&Limit=5
&Offset=0
&<共通リクエストパラメータ>
```

#### 出力サンプル

```
{
    "Response": {
        "TotalCount": 1,
        "InstanceSet": [
            {
                "InstanceName": "crs-6ubhgouj",
                "InstanceId": "crs-6ubhgouj",
                "Appid": 251005863,
                "ProjectId": 0,
                "RegionId": 1,
                "ZoneId": 100002,
                "VpcId": 0,
                "SubnetId": 0,
                "UniqVpcId": "",
                "UniqSubnetId": "",
                "Status": 2,
                "WanIp": "10.66.126.126",
                "Port": 6379,
                "Createtime": "2015-06-11 16:54:21",
                "Type": 1,
                "BillingMode": 1,
                "Engine":"コミュニティ版Redis",
                "ProductType": "Redis2.8クラスタ版",
                "Size": 2048,
                "SizeUsed": 0,
                "DeadlineTime": "2020-09-08 16:21:05",
                "AutoRenewFlag": 0
            }
        ],
        "RequestId": "03f6c2f8-cd3f-41aa-82b8-3bce0c605da5"
    }
}
```


## 5. 開発者リソース

### API Explorer

**本ツールはオンライン呼び出し、署名認証、SDK コード生成、高速インターフェース検索などの能力を提供します。クラウド API の使用難易度を大きく下げることができるため、使用することをお勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeInstances)

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
| InternalError.DbOperationFailed | システムの DB 操作エラー。update insert select..とすることができます。|
| InvalidParameter | パラメータエラー |
| InvalidParameter.EmptyParam | パラメータは空です。|
| InvalidParameter.InvalidParameter | サービスパラメータエラー。|
| UnauthorizedOperation.NoCAMAuthed | cam 権限なし。|

