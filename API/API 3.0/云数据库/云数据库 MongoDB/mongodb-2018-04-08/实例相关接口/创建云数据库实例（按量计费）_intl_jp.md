## 1. API説明

APIリクエストドメイン名：mongodb.tencentcloudapi.com。

このAPI（CreateDBInstanceHour）は、従量制課金のTencentDB for MongoDBインスタンス（マスタインスタンス、ディザスタリカバリインスタンスおよび読み取り専用インスタンスを含む）を作成するために使用されます。インスタンス仕様、インスタンスタイプ、MongoDBのバージョン、購入期間、数量などの情報を渡すことでクラウドデータベースインスタンスを作成できます。

デフォルトAPIのリクエスト頻度制限：20回/秒

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：mongodb.ap-shanghai-fsi.tencentcloudapi.com 。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータについては、[共通リクエストパラメータ](/document/api/240/31800)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、該当APIの値：CreateDBInstanceHour |
| Version | はい | String | 共通パラメータ、該当APIの値：2018-04-08 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/240/31800#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| Memory | はい | Integer | インスタンスメモリサイズ、単位：GB |
| Volume | はい | Integer | インスタンスディスクサイズ、単位：GB |
| ReplicateSetNum | はい | Integer | コピーセットの数、1は単一のコピーセットインスタンス、1より大きい場合はシャードクラスタインスタンス、最大は10未満 |
| SecondaryNum | はい | Integer | 各コピーセットにあるスレーブノードの数、現在2つのスレーブノードだけがサポートされます |
| EngineVersion | はい | String | MongoDBエンジンバージョン、値にはMONGO_2、MONGO_3_MMAP、MONGO_3_WT 、MONGO_3_ROCKSおよびMONGO_36_WTが含まれます |
| Machine | はい | String | インスタンスタイプ、GIO：High IOバージョン；TGIO：High IO 10ギガビット |
| GoodsNum | はい | Integer | インスタンス数、デフォルト値は1、最小値は1、最大値は10 |
| Zone | はい | String | Availability Zone情報、フォーマット：ap-guangzhou-2 |
| InstanceRole | はい | String | インスタンスロール、サポートする値は以下のとおりです：MASTER-マスタインスタンス、DR-ディザスタリカバリインスタンス、RO-読み取り専用インスタンス |
| InstanceType | はい | String | インスタンスタイプ、REPLSET-コピーセット、SHARD-シャードクラスタ |
| Encrypt | いいえ | Integer | データが暗号化されるかどうか、エンジンのバージョンがMONGO_3_ROCKSの場合に限り、暗号化を選択できます |
| VpcId | いいえ | String | VPC ID、転送しないと、デフォルトとして基本ネットワークを選択します |
| SubnetId | いいえ | String | VPCのサブネットID、VpcIdを設定した場合、SubnetIdが必須です |
| ProjectId | いいえ | Integer | プロジェクトID、入力しないとデフォルトプロジェクトとなります |
| SecurityGroup.N | いいえ | Array of String | セキュリティグループのパラメータ |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| DealId | String | 注文ID|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 クラウドデータベースインスタンス（従量制課金）の作成

ユーザーがAPIを通して従量制課金のクラウドデータベースインスタンスを作成する必要があります

#### 入力例

```
https://mongodb.tencentcloudapi.com/?Action=CreateDBInstanceHour
&Memory=4
&Volume=250
&ReplicateSetNum=1
&SecondaryNum=2
&EngineVersion=MONGO_3_WT
&Machine=TGIO
&GoodsNum=1
&Zone=ap-guangzhou-3
&InstanceRole=MASTER
&InstanceType=REPLSET
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "RequestId": "d3aecf52-5abf-49e4-bf79-1a6c47a406d4",
        "DealId": "28920"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIを使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mongodb&Version=2018-04-08&Action=CreateDBInstanceHour)

### SDK

クラウドAPI 3.0は、API呼び出しを容易にするために複数のプログラミング言語をサポートする、関連開発ツールセット（SDK）を提供します。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### CLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. エラーコード

このAPIには業務ロジックに関連するエラーコードがまだありません。その他のエラーコードについては、[共通エラーコード](/document/api/240/31803#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

