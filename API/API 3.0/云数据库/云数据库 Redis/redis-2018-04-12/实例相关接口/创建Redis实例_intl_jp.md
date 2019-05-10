## 1. インターフェースについて

インターフェースのリクエストドメイン名：redis.tencentcloudapi.com 。

redisインスタンスの作成

初期設定の状態では、インターフェースのリクエスト頻度は20回/秒に制限されています。

注意：このインターフェースは、金融エリアのリージョンに対応しています。金融エリアとそれ以外のエリアは隔てられているため、相互運用ができません。そのため、共通パラメータの Region が金融エリアのリージョン（ap-shanghai-fsi など）である場合、同時に金融エリアのリージョンを持つドメイン名を指定する必要があります。最も良いのは、redis.ap-shanghai-fsi.tencentcloudapi.com のように Region のエリアと一致させることです。



## 2. パラメータ入力

以下のリクエストパラメータリストは、インターフェースリクエストパラメータと一部の共通パラメータのみを表しています。完全な共通パラメータのリストは、[共通のリクエストパラメータ](/document/api/239/20005)を参照してください。

| パラメータ名 | 選択必須 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | 要 | String | 共通パラメータ。本インターフェースの取得値：CreateInstances |
| Version | 要 | String | 共通パラメータ。本インターフェースの値：2018-04-12 |
| Region | 要 | String | 共通パラメータ。製品がサポートする[リージョンリスト](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。|
| ZoneId | 要 | Integer | インスタンスが属するアベイラビリティゾーンのid |
| TypeId | 要 | Integer | インスタンスタイプ：2 – Redis2.8マスタースレーブ版、3 – Redis3.2マスタースレーブ版(CKVマスタースレーブ版)、4 – Redis3.2クラスタ版(CKVクラスタ版)、5-Redis2.8スタンドアロン版、7 – Redis4.0クラスタ版、 |
| MemSize | 要 | Integer | インスタンスの容量。単位はMBとし、値の大きさは販売仕様照会インターフェースが返した仕様に準ずる|
| GoodsNum | 要 | Integer | インスタンスの数。1回に購入するインスタンスの数は、販売仕様照会インターフェースが返した仕様に準ずる|
| Period | 要 | Integer | 購入時期。単位は月、値の範囲[1,2,3,4,5,6,7,8,9,10,11,12,24,36] |
| Password | 要 | String | インスタンスのパスワード。パスワードルールは、1.長さ8～16文字。2:少なくともアルファベット、数字および記号!@^*()のうちの2種類を含むこと |
| BillingMode | 要 | Integer | 支払い方法:0-従量課金、1-年払い（月払い）。|
| VpcId | 不要 | String | VPC ID。送信しない場合はデフォルトで基本ネットワークを選択します。vpc-sad23jfdfk などの VPC リストを使用して照会してくだい |
| SubnetId | 要 | String | 基本ネットワークでは、subnetId は無効です。 vpcサブネットワークでは、値はsubnet-fdj24n34j2 のようにサブネットワークで照会します |
| ProjectId | 不要 | Integer | プロジェクトid。値は、ユーザーアカウント>ユーザーアカウント関連インターフェース照会>プロジェクトリストによって返されたprojectIdに準じます |
| AutoRenew | 不要 | Integer | 自動更新を表示します。0 - デフォルト状態（手動更新）、1 - 自動更新、2 - 絶対に自動更新しない |
| SecurityGroupIdList.N | 不要 | Array of String | セキュリティグループid配列 |
| VPort | 不要 | Integer | ユーザーがカスタマイズしたポート。記載がない場合、デフォルトで 6379 |
| RedisShardNum | 不要 | Integer | インスタンスのシャード数。Redis2.8マスタースレーブ版、CKVマスタースレーブ版とRedis2.8スタンドアロン版の場合は入力不要です |
| RedisReplicasNum | 不要 | Integer | インスタンスのコピー数は、Redis2.8マスタースレーブ版、CKVマスタースレーブ版とRedis2.8スタンドアロン版の場合は入力不要です |
| ReplicasReadonly | 不要 | Boolean | コピーの読み取り専用をサポートするかどうかについて、Redis2.8マスタースレーブ版、CKVマスタースレーブ版とRedis2.8スタンドアロン版の場合入力不要です |

## 3. パラメータ出力

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| DealId | String | トランザクションId|
| RequestId | String | 一意のリクエスト ID。毎回リクエストするごとに戻ります。問題を見つけ出す際、そのリクエストの RequestId を提供する必要があります。|

## 4. サンプル

### サンプル1 リクエストサンプル

#### 入力サンプル

```
https://redis.tencentcloudapi.com/?Action=CreateInstances
&ZoneId=100002
&TypeId=2
&MemSize=1024
&GoodsNum=1
&Period=1
&Password=********
&BillingMode=1
&<共通リクエストパラメータ>
```

#### 出力サンプル

```
{
    "Response": {
        "DealId": "123456",
        "RequestId": "d4e2fd95-eac5-41ef-a7a9-7d30024d5507"
    }
}
```


## 5. 開発者リソース

### API Explorer

**本ツールはオンライン呼び出し、署名認証、SDK コード生成、高速インターフェース検索などの能力を提供します。クラウド API の使用難易度を大きく下げることができるため、使用することをお勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=CreateInstances)

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
| InvalidParameter.OnlyVPCOnSpecZoneId |上海金融はvpcネットワークのみ提供します。|
| InvalidParameterValue.InvalidInstanceTypeId | 購入をリクエストしたインスタンスタイプのエラー（TypeId 1:クラスタ版、2:マスタースレーブ版すなわち旧マスタースレーブ版)。|
| InvalidParameterValue.InvalidSubnetId | vpcネットワークにおいて、vpcid サブネットワークid は不正です。|
| InvalidParameterValue.PasswordEmpty | パスワードが空です。|
| InvalidParameterValue.PasswordRuleError | パスワードを設定した場合、MC が送信する old password が以前に設定したパスワードと異なります。|
| LimitExceeded.InvalidMemSize | 求める容量が販売仕様にありません（memSizeは1024の整数倍で、単位はMBです）。|
| LimitExceeded.InvalidParameterGoodsNumNotInRange | 1回で購入をリクエストするインスタンス数が、販売数の制限範囲内にありません。|
| LimitExceeded.PeriodExceedMaxLimit | 購入期間が3年を超えており、リクエスト期間が最長期間を超えています。|
| LimitExceeded.PeriodLessThanMinLimit | 購入期間が不正です。期間は最短1か月です。|
| ResourceNotFound.AccountDoesNotExists | uin 値が空です。|
| ResourceNotFound.InstanceNotExists | serialId に基づいて対応する redis が見つかりません。|
| ResourceUnavailable.InstanceDeleted | インスタンスがリサイクル済みです。|
| ResourceUnavailable.NoRedisService | リクエストしたエリアでは、リクエストしたタイプのredisサービスを提供していません。|
| ResourceUnavailable.NoTypeIdRedisService | リクエストしたエリアでは、リクエストしたタイプのredisサービスを提供していません。|
| UnauthorizedOperation.NoCAMAuthed | cam 権限なし。|
| UnauthorizedOperation.UserNotInWhiteList | ユーザーがホワイトリストにありません。|

