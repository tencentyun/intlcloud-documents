## 1. API説明

APIリクエストドメイン名：as.tencentcloudapi.com 。

このAPI（CreateLaunchConfiguration）は新しい起動構成を作成するために使用されます。

* 起動構成は、`ModifyLaunchConfigurationAttributes`を通して少数のフィールドを変更することができます。新しい起動構成を使用する必要がある場合、起動構成を再作成することをお勧めします。

* 各プロジェクトは最大20個の起動構成を作成できます。詳細については、[使用制限](https://cloud.tencent.com/document/product/377/3120)を参照してください。


デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：as.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータについては、[共通リクエストパラメータ](/document/api/377/20426)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：CreateLaunchConfiguration |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-04-19 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| LaunchConfigurationName | はい | String | 起動構成の名前。この名前は、中国語、英語、数字、アンダースコア、区切り記号「-」、小数点のみをサポートし、最大長は60バイトを超えることはできません。 |
| ImageId | はい | String | 有効な[イメージ](https://cloud.tencent.com/document/product/213/4940)IDを指定します。`img-8toqc6s3`のような形をしています。イメージの種類は4種類あります。<br/><li>共通イメージ</li><li>カスタムイメージ</li><li>共有イメージ</li><li>サービスマーケットイメージ</li><br/>以下の方法で使用可能なイメージIDを取得できます。<br/><li>`共通イメージ`、`カスタムイメージ`、`共有イメージ`のイメージIDは、[コンソール](https://console.cloud.tencent.com/cvm/image?rid=1&imageType=PUBLIC_IMAGE)にログインして確認できます。`サービスイメージマーケット`のイメージIDは、[クラウドマーケット](https://market.cloud.tencent.com/list)で確認できます。</li><li>API [DescribeImages](https://cloud.tencent.com/document/api/213/15715)を呼び出して、返されたメッセージの`ImageId`フィールドを取ります。</li> |
| ProjectId | いいえ | Integer | インスタンスが属するプロジェクトID。このパラメータは[DescribeProject](https://cloud.tencent.com/document/api/378/4400)の戻り値の`projectId`フィールドを呼び出して取得できます。記入しない場合は、デフォルトプロジェクトが使用されます。 |
| InstanceType | いいえ | String | インスタンスモデル。異なるインスタンスモデルは異なるリソース仕様を指定します。具体的な値は、API [DescribeInstanceTypeConfigs](https://cloud.tencent.com/document/api/213/15749)を呼び出して最新の仕様書を取得するか、または[インスタンスタイプ](https://cloud.tencent.com/document/product/213/11518)の説明を参照してください。<br/>`InstanceType`と`InstanceTypes`パラメータは相互に排他的で、両方のいずれかを記入する必要があります。 |
| SystemDisk | いいえ | [SystemDisk](/document/api/377/20453#SystemDisk) | インスタンスシステムディスクの構成情報。このパラメータを指定しないと、システムのデフォルト値に従って割り当てられます。 |
| DataDisks.N | いいえ | Array of [DataDisk](/document/api/377/20453#DataDisk) | インスタンスデータディスクの構成情報。このパラメータを指定しない場合、デフォルトでデータディスクは購入されません。最大11個のデータディスクを指定できます。 |
| InternetAccessible | いいえ | [InternetAccessible](/document/api/377/20453#InternetAccessible) | パブリックネットワーク帯域幅の関連情報の設定。このパラメータが指定されていない場合、デフォルトのパブリックネットワーク帯域幅は0Mbpsです。 |
| LoginSettings | いいえ | [LoginSettings](/document/api/377/20453#LoginSettings) | インスタンスログイン設定。このパラメータを使用すると、インスタンスのログインパスワード、暗号鍵を設定でき、またはイメージの元のログイン設定を保持します。デフォルトでは、パスワードはランダムに生成され、サイト内メッセージでユーザーに通知されます。 |
| SecurityGroupIds.N | いいえ | Array of String | インスタンスが属するセキュリティグループ。このパラメータは[DescribeSecurityGroups](https://cloud.tencent.com/document/api/215/15808)の戻り値の`SecurityGroupId`フィールドを呼び出して取得できます。このパラメータを指定しないと、デフォルトでセキュリティグループはバインディングされません。 |
| EnhancedService | いいえ | [EnhancedService](/document/api/377/20453#EnhancedService) | 強化されたサービス。このパラメータを使用すると、クラウドセキュリティやCMなどのサービスを有効にするかどうかを指定できます。このパラメータが指定されていない場合、デフォルトでCMとクラウドセキュリティサービスは有効になります。 |
| UserData | いいえ | String | Base64エンコード後のカスタムデータ。最大長は16KB以下です。 |
| InstanceChargeType | いいえ | String | インスタンス課金タイプ。CVMのデフォルト値はPOSTPAID_BY_HOURに従って処理されます。<br/><br><li>POSTPAID_BY_HOUR：時間制後払い<br/><br><li>SPOTPAID：入札支払 |
| InstanceMarketOptions | いいえ | [InstanceMarketOptionsRequest](/document/api/377/20453#InstanceMarketOptionsRequest) | インスタンスマーケット関連オプション。入札インスタンスに関するパラメータを例として、指定したインスタンスの支払モードは入札支払であれば、このパラメータを転送する必要があります。 |
| InstanceTypes.N | いいえ | Array of String | インスタンスモデルのリスト。異なるインスタンスモデルは異なるリソース仕様を指定し、最大5つのインスタンスモデルをサポートします。<br/>`InstanceType`と`InstanceTypes`パラメータは相互に排他的で、両方のいずれかを記入する必要があります。 |
| InstanceTypesCheckPolicy | いいえ | String | インスタンスタイプ検証ポリシー。値はALLおよびANYがあり、デフォルト値はANYです。<br/><br><li> ALLは、すべてのインスタンスタイプ（InstanceType）が使用可能な場合は、検証に合格し、それ以外の場合は検証エラーが報告されます。<br/><br><li> ANYは、任意のインスタンスタイプ（InstanceType）が使用可能な場合は、検証に合格し、それ以外の場合は検証エラーが報告されます。<br/><br/>インスタンスタイプが使用できない一般的な原因は、インスタンスタイプの売り切れ、対応するクラウドディスクの売り切れなどです。<br/>InstanceTypesの1つのモデルが存在しないか既に無効だった場合、InstanceTypesCheckPolicyの値に関係なく、検証エラーが報告されます。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| LaunchConfigurationId | String | このAPIを介して起動構成を作成するときにこのパラメータが返され、起動構成IDを示します。|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1　簡単なパラメータ作成

必要な起動構成名、インスタンスモデル、イメージIDだけを渡します。それ以外はシステムデフォルト値を使用します。具体的な構成は次のとおりです。起動構成名はas_test、インスタンスモデルは標準2型1C1G（S2.SMALL1）、イメージIDはimg-8toqc6s3です。

#### 入力例

```
https://as.tencentcloudapi.com/?Action=CreateLaunchConfiguration
&LaunchConfigurationName=as_test
&InstanceType=S2.SMALL1
&ImageId=img-8toqc6s3
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "LaunchConfigurationId": "asc-23h37kyn",
        "RequestId": "d639dd64-9e46-4246-b13c-80954f81c11b"
    }
}
```

### 例2　詳細なパラメータ作成

起動構成名はas_test、イメージIDはimg-8toqc6s3、選択モデルは標準2型1C1G（S2.SMALL1）、システムディスクは50Gローカルディスク、データディスクは100G HDD Cloud Storageです。パブリックネットワーク支払いモードは、トラフィックに応じた時間制後払いです。パブリックネットワークの帯域幅は5 Mbpsに制限され、パブリックネットワークIPが割り当てられ、暗号鍵でログインされ、CMとクラウドセキュリティがインストールされます。

#### 入力例

```
https://as.tencentcloudapi.com/?Action=CreateLaunchConfiguration
&LaunchConfigurationName=as_test
&ImageId=img-8toqc6s3
&InstanceType=S2.SMALL1
&SystemDisk.DiskType=LOCAL_BASIC
&SystemDisk.DiskSize=50
&DataDisks.0.DiskType=CLOUD_BASIC
&DataDisks.0.DiskSize=100
&InternetAccessible.InternetChargeType=TRAFFIC_POSTPAID_BY_HOUR
&InternetAccessible.InternetMaxBandwidthOut=5
&InternetAccessible.PublicIpAssigned=TRUE
&LoginSettings.KeyIds.0=skey-k8eypc1l
&EnhancedService.SecurityService.Enabled=TRUE
&EnhancedService.MonitorService.Enabled=TRUE
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "LaunchConfigurationId": "asc-fdz8j7dh",
        "RequestId": "9a7209d3-2260-49d7-952a-dfa2001f8822"
    }
}
```

### 例3　入札インスタンス構成の作成

起動構成名はspot-test、モデルは標準2型2C4G（S2.MEDIUM4）、課金構成は入札（SPOTPAID）、最高入札は0.99元/時です。

#### 入力例

```
https://as.tencentcloudapi.com/?Action=CreateLaunchConfiguration
&LaunchConfigurationName=spot-test
&InstanceType=S2.MEDIUM4
&ImageId=img-8toqc6s3
&SystemDisk.DiskType=CLOUD_PREMIUM
&SystemDisk.DiskSize=50
&InternetAccessible.InternetChargeType=TRAFFIC_POSTPAID_BY_HOUR
&InternetAccessible.InternetMaxBandwidthOut=20
&InternetAccessible.PublicIpAssigned=true
&InstanceChargeType=SPOTPAID
&InstanceMarketOptions.MarketType=spot
&InstanceMarketOptions.SpotOptions.MaxPrice=0.99
&InstanceMarketOptions.SpotOptions.SpotInstanceType=one-time
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "LaunchConfigurationId": "asc-hpzwe3o2",
        "RequestId": "ccfe3052-e9c9-47ee-bf3d-5bc2dfd972c0"
    }
}
```

### 例4　起動構成を作成して複数のインスタンスモデルをサポート

2種類のインスタンスモデルをサポートします。それぞれはS2.SMALL2とS2.SMALL4です

#### 入力例

```
https://as.tencentcloudapi.com/?Action=CreateLaunchConfiguration
&LaunchConfigurationName=multi_instance_types
&InstanceTypes.0=S2.SMALL2
&InstanceTypes.1=S2.SMALL4
&ImageId=img-8toqc6s3
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "LaunchConfigurationId": "asc-77mh1cho",
        "RequestId": "2864c860-27a0-439e-a1e1-0003b76734e7"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CreateLaunchConfiguration)

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

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| AccountQualificationRestrictions | このリクエストアカウントは資格審査に合格しませんでした。 |
| CallCvmError | CVM APIの呼び出しが失敗しました。 |
| InvalidImageId.NotFound | このイメージが見つかりませんでした。 |
| InvalidLaunchConfiguration.NameDuplicate | 起動構成名が重複しています。 |
| InvalidParameter.Conflict | パラメータの競合：指定された複数のパラメータが競合しており、同時に存在することはできません。 |
| InvalidParameter.MustOneParameter | パラメーターが欠落しており、2つのパラメータのいずれかを指定する必要があります。 |
| InvalidParameterValue.CvmConfigurationError | CVMパラメータ検証が異常です。 |
| InvalidPermission | この操作はアカウントではサポートされていません。 |
| LaunchConfigurationQuotaLimitExceeded | 起動構成の割り当て量が制限を超えています。 |

