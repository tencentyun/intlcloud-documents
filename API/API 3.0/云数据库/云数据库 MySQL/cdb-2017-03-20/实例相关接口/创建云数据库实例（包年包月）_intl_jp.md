## 1. API説明

APIリクエストドメイン名： cdb.tencentcloudapi.com 。

このAPI（CreateDBInstance）は年額/月額のデータベースインスタンス（マスタインスタンス、ディザスタリカバリインスタンス、読み取り専用インスタンスを含む）を作成するために使用されます。インスタンス仕様、MySQLバージョン番号、購入期間や数量などの情報を渡すことでデータベースインスタンスを作成できます。

このAPIは非同期APIです。[インスタンスリストの照合](https://cloud.tencent.com/document/api/236/15872) APIでこのインスタンスの詳細情報を照合することもできます。このインスタンスのStatusは1、且TaskStatusは0であれば、インスタンスの出荷が成功したことを示します。

1. まずは[データベースの販売可能な仕様の取得](https://cloud.tencent.com/document/api/236/17229) APIで作成可能なインスタンス仕様情報を照合し、次は[データベース価格の照合](https://cloud.tencent.com/document/api/236/18566) APIで作成可能なインスタンスの販売価格を照合してください。
2. 単回作成するインスタンスは最大100個をサポートします。インスタンス期間は最大36ヶ月をサポートします。
3. MySQL5.5、MySQL5.6、MySQL5.7バージョンの作成をサポートします。
4. マスタインスタンス、読み取り専用インスタンス、ディザスタリカバリインスタンスの作成をサポートします。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：cdb.ap-shanghai-fsi.tencentcloudapi.com 。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/236/15833)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、該当APIの値：CreateDBInstance |
| Version | はい | String | 共通パラメータ、該当APIの値：2017/03/20 |
| Region | はい | String | 共通パラメータ。詳細について製品がサポートする[地域リスト](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| Memory | はい | Integer | インスタンスメモリのサイズ。単位：MB。[データベースの販売可能な仕様の取得](https://cloud.tencent.com/document/api/236/17229) APIで作成可能なメモリ仕様を取得してください |
| Volume | はい | Integer | インスタンスディスクのサイズ。単位：GB。[データベースの販売可能な仕様の取得](https://cloud.tencent.com/document/api/236/17229) APIで作成可能なディスク範囲を取得してください |
| Period | はい | Integer | インスタンス期間。単位：月。選択可能な値：[1,2,3,4,5,6,7,8,9,10,11,12,24,36] |
| GoodsNum | はい | Integer | インスタンス数、デフォルト値は1、最小値は1、最大値は100 |
| Zone | いいえ | String | Availability Zone情報。このパラメータをデフォルト値に設定した場合、システムは自動的に1つのAvailability Zoneを選択します。[データベースの販売可能な仕様の取得](https://cloud.tencent.com/document/api/236/17229) APIで作成可能なAvailability Zoneを取得してください |
| UniqVpcId | いいえ | String | VPC ID。渡さない場合デフォルトで基本ネットワークが選択されます。[VPCリストの照合](https://cloud.tencent.com/document/api/215/15778)を使用してください |
| UniqSubnetId | いいえ | String | VPCのサブネットID。UniqVpcIdが設定された場合、UniqSubnetIdは入力必須です。[サブネットリストの照合](https://cloud.tencent.com/document/api/215/15784)を使用してください |
| ProjectId | いいえ | Integer | プロジェクトID。入力しないとデフォルトプロジェクトです。[プロジェクトリストの照合](https://cloud.tencent.com/document/product/378/4400) APIでプロジェクトIDを取得してください |
| Port | いいえ | Integer | カスタムポート。ポート範囲：[ 1024～65535 ] |
| InstanceRole | いいえ | String | インスタンスタイプ。デフォルトはmaster、対応値：master-マスタインスタンス、dr-ディザスタリカバリインスタンス、ro-読み取り専用インスタンス |
| MasterInstanceId | いいえ | String | インスタンスID。読み取り専用インスタンスを購入する際には入力必須です。このフィールドは読み取り専用インスタンスのマスタインスタンスIDを示します。[インスタンスリストの照合](https://cloud.tencent.com/document/api/236/15872) APIでデータベースインスタンスIDを照合してください |
| EngineVersion | いいえ | String | MySQLバージョン。値：5.5、5.6と5.7。[データベースの販売可能な仕様の取得](https://cloud.tencent.com/document/api/236/17229) APIで作成可能なインスタンスバージョンを取得してください |
| Password | いいえ | String | rootアカウントの設定パスワード。パスワードルール：8～64文字、少なくともアルファベット、数字と文字（対応文字：_+-&=!@#$%^*()）の2種類を含む必要があります。マスタインスタンスを購入する際にこのパラメータを指定できます。読み取り専用インスタンスまたはディザスタリカバリインスタンスを購入する際にこのパラメータを指定しても意味がありません |
| ProtectMode | いいえ | Integer | データレプリケーション方式。デフォルトは0です。対応値：0-非同期レプリケーション、1-準同期レプリケーション、2-強同期レプリケーション |
| DeployMode | いいえ | Integer | 複数のAvailability Zone。デフォルトは0。対応値：0-単一Availability Zone、1-複数Availability Zone |
| SlaveZone | いいえ | String | スレーブデータベース1のAvailability Zone情報。デフォルトは地区の値 |
| ParamList.N | いいえ | Array of [ParamInfo](https://cloud.tencent.com/document/api/236/15878#ParamInfo) | パラメータリスト。パラメータフォーマットの例：ParamList.0.Name=auto_increment&ParamList.0.Value=1。[インスタンスの設定可能なパラメータリストの照合](https://cloud.tencent.com/document/api/236/20411)で設定可能なパラメータを照合できます |
| BackupZone | いいえ | String | スレーブデータベース2のAvailability Zone ID。デフォルトは0です。マスタインスタンスを購入する際にこのパラメータを指定できます。読み取り専用インスタンスまたはディザスタリカバリインスタンスを購入する際にこのパラメータを指定しても意味がありません |
| AutoRenewFlag | いいえ | Integer | 自動更新フラグ。選択可能な値：0-非自動更新、1-自動更新 |
| MasterRegion | いいえ | String | マスタインスタンス地域情報。ディザスタリカバリインスタンスを購入する際に、このフィールドは入力必須です |
| SecurityGroup.N | いいえ | Array of String | セキュリティグループパラメータ。[プロジェクトセキュリティグループ情報の照合](https://cloud.tencent.com/document/api/236/15850) APIで特定プロジェクトのセキュリティグループの詳細を照合できます |
| RoGroup | いいえ | [RoGroup](https://cloud.tencent.com/document/api/236/15878#RoGroup) | 読み取り専用インスタンスパラメータ |
| InstanceName | いいえ | String | インスタンス名 |
| ResourceTags.N | いいえ | Array of [TagInfo](https://cloud.tencent.com/document/api/236/15878#TagInfo) | インスタンスとバインディングされるタグ |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| DealIds | Array of String | 短い注文ID|
| InstanceIds | Array of String | インスタンスIDリスト|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 マスタインスタンスの購入

#### 入力例

```
https://cdb.tencentcloudapi.com/?Action=CreateDBInstance
&Memory=1000
&Volume=25
&Period=1
&GoodsNum=1
&Zone=ap-guangzhou-3
&UniqVpcId=vpc-0akbol5v
&UniqSubnetId=subnet-fyrtjbqw
&ProjectId=0
&InstanceRole=master
&EngineVersion=5.6
&ResourceTags.0.TagKey=marchtest
&ResourceTags.0.TagValue.0=test1
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "InstanceIds":["cdb-pn6gd5jp"],
        "DealIds":["20171201110011"]
    }
}
```

### 例2 読み取り専用インスタンスの購入

#### 入力例

```
https://cdb.tencentcloudapi.com/?Action=CreateDBInstance
&MasterInstanceId=cdb-fn3f9xpx
&Period=1
&GoodsNum=1
&Memory=4000
&Volume=100
&InstanceRole=ro
&RoGroup.roGroupMode=allinone
&RoGroup.roGroupName=jersey_test
&RoGroup.roOfflineDelay=1
&RoGroup.roMaxDelayTime=5
&RoGroup.minRoInGroup=1
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "DealIds": ["20171205110051"],
        "InstanceIds": ["cdbro-hlpl4ik9"]
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=CreateDBInstance)

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
| InternalError.DatabaseAccessError | データベース内部エラー。 |
| InternalError.DfwError | セキュリティグループ操作エラー。 |
| InternalError.TradeError | 取引システムエラー。 |
| InternalError.VpcError | VPCまたはサブネットエラー。 |
| InvalidParameter | パラメータエラー。 |
| OperationDenied.ActionNotSupport | サポートしない操作。 |
| OperationDenied.WrongPassword | パスワードエラーまたは検証に合格しません。 |

