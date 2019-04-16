## 1. API説明

APIリクエストドメイン名： cdb.tencentcloudapi.com 。

このAPI（UpgradeDBInstance）はデータベースインスタンスをアップグレードするために使用されます。インスタンスタイプについては、マスタインスタンス、ディザスタリカバリインスタンス、読み取り専用インスタンスをサポートします

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：cdb.ap-shanghai-fsi.tencentcloudapi.com 。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/236/15833)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、該当APIの値：UpgradeDBInstance |
| Version | はい | String | 共通パラメータ、該当APIの値：2017/03/20 |
| Region | はい | String | 共通パラメータ。詳細について製品がサポートする[地域リスト](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| InstanceId | はい | String | インスタンスID。フォーマット：cdb-c1nl9rpvまたはcdbro-c1nl9rpv。データベースコンソールページで表示されるインスタンスIDと同じ。[インスタンスリストの照合](https://cloud.tencent.com/document/api/236/15872) APIで取得できます。その値は出力パラメータのフィールドInstanceIdの値です |
| Memory | はい | Integer | アップグレード後のメモリのサイズ。単位：MB。渡されたMemory値の有効性を確保するために、[データベースの販売可能な仕様の取得](https://cloud.tencent.com/document/product/236/17229) APIでアップグレード可能なメモリ仕様を取得してください |
| Volume | はい | Integer | アップグレード後のディスクのサイズ。単位：GB。渡されたVolume値の有効性を確保するために、[データベースの販売可能な仕様の取得](https://cloud.tencent.com/document/product/236/17229) APIでアップグレード可能なディスク範囲を取得してください |
| ProtectMode | いいえ | Integer | データレプリケーション方式。対応値：0-非同期レプリケーション、1-準同期レプリケーション、2-強同期レプリケーション。マスタインスタンスをアップグレードする際にはこのパラメータを指定できます。読み取り専用インスタンスまたはディザスタリカバリインスタンスをアップグレードする際にこのパラメータを指定しても意味がありません |
| DeployMode | いいえ | Integer | 配置モード。デフォルトは0です。対応値：0-単一Availability Zone配置、1-複数Availability Zone配置。マスタインスタンスをアップグレードする際にはこのパラメータを指定できます。読み取り専用インスタンスまたはディザスタリカバリインスタンスをアップグレードする際にこのパラメータを指定しても意味がありません |
| SlaveZone | いいえ | String | スレーブデータベース1のAvailability Zone情報。デフォルトはインスタンスのZoneパラメータと一致します。マスタインスタンスを複数Availability Zone配置にアップグレードする際にはこのパラメータを指定できます。読み取り専用インスタンスまたはディザスタリカバリインスタンスをアップグレードする際にはこのパラメータを指定しても意味がありません。[データベースの販売可能な仕様の取得](https://cloud.tencent.com/document/product/236/17229) APIでサポートするAvailability Zoneを照合できます |
| EngineVersion | いいえ | String | マスタインスタンスデータベースエンジンバージョン。対応値：5.5、5.6と5.7 |
| WaitSwitch | いいえ | Integer | 新しいインスタンスへのアクセスに切り替える方式。デフォルトは0です。マスタインスタンスをアップグレードする際にこのパラメータを指定できます。読み取り専用インスタンスまたはディザスタリカバリインスタンスをアップグレードする際にこのパラメータを指定しても意味がありません。対応値：0-今すぐ切り替える、1-タイムウィンドウの切り替え。この値は1の場合、アップグレード過程中で新しいインスタンスへのアクセスに切り替えるプロセスはタイムウィンドウで行われるか、またはユーザーが[新しいインスタンスへのアクセスに切り替える](https://cloud.tencent.com/document/product/236/15864) APIを呼び出しこのプロセスをトリガーします |
| BackupZone | いいえ | String | スレーブデータベース2のAvailability Zone ID。デフォルトは0です。マスタインスタンスをアップグレードする際にこのパラメータを指定できます。読み取り専用インスタンスまたはディザスタリカバリインスタンスをアップグレードする際にこのパラメータを指定しても意味がありません |
| InstanceRole | いいえ | String | インスタンスタイプ。デフォルトはmaster、対応値：master-マスタインスタンス、dr-ディザスタリカバリインスタンス、ro-読み取り専用インスタンス |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| DealIds | Array of String | 注文ID|
| AsyncRequestId | String | 非同期タスクのリクエストID、このIDで非同期タスクの実行結果を照合できます|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 データベースインスタンスのアップグレード

#### 入力例

```
https://cdb.tencentcloudapi.com/?Action=UpgradeDBInstance
&InstanceId=cdb-6si6qy6p
&Memory=1000
&Volume=50
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "DealIds":[
            "20171204110077"
        ],
        "AsyncRequestId":"a6040589-3b098df5-b551d9e5-81c6bfdc"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=UpgradeDBInstance)

### SDK

クラウドAPI 3.0は、API呼び出しを容易にするために複数のプログラミング言語をサポートする、関連開発ツールセット（SDK）を提供します。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. エラーコード

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](/document/api/236/15835#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| FailedOperation.StatusConflict | タスク状態競合。 |
| InternalError.DatabaseAccessError | データベース内部エラー。 |
| InternalError.TradeError | 取引システムエラー。 |
| InvalidParameter | パラメータエラー。 |

