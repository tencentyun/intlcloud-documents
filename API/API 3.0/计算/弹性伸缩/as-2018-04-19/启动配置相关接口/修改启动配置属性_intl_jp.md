## 1. API説明

APIリクエストドメイン名：as.tencentcloudapi.com 。

このAPI（ModifyLaunchConfigurationAttributes）は、起動構成の一部の属性を変更するために使用されます。

* 起動構成を変更した後、この起動構成を使用して拡張されたインベントリインスタンスは変更されず、その後、この起動構成を使用する新しいインスタンスは新しい構成に従って拡張されます。
* このAPIは一部の簡単なタイプの変更をサポートします。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：as.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータについては、[共通リクエストパラメータ](/document/api/377/20426)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：ModifyLaunchConfigurationAttributes |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-04-19 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| LaunchConfigurationId | はい | String | 起動構成ID |
| ImageId | いいえ | String | 有効な[イメージ](https://cloud.tencent.com/document/product/213/4940)IDを指定します。`img-8toqc6s3`のような形をしています。イメージの種類は4種類あります。<br/><li>共通イメージ</li><li>カスタムイメージ</li><li>共有イメージ</li><li>サービスマーケットイメージ</li><br/>以下の方法で使用可能なイメージIDを取得できます。<br/><li>`共通イメージ`、`カスタムイメージ`、`共有イメージ`のイメージIDは、[コンソール](https://console.cloud.tencent.com/cvm/image?rid=1&imageType=PUBLIC_IMAGE)にログインして確認できます。`サービスイメージマーケット`のイメージIDは、[クラウドマーケット](https://market.cloud.tencent.com/list)で確認できます。</li><li>API [DescribeImages](https://cloud.tencent.com/document/api/213/15715)を呼び出して、返されたメッセージの`ImageId`フィールドを取ります。</li> |
| InstanceTypes.N | いいえ | Array of String | インスタンスタイプのリスト。異なるインスタンスモデルは異なるリソース仕様を指定し、最大5つのインスタンスモデルをサポートします。<br/>起動構成。InstanceTypeを通して単一のインスタンスタイプを表し、InstanceTypesを通してマルチインスタンスタイプを表します。指定されたInstanceTypesが構成を成功的に起動した後、元のInstanceTypeは自動的に無効になります。 |
| InstanceTypesCheckPolicy | いいえ | String | インスタンスタイプ検証ポリシー。実際にInstanceTypesを変更する際に役割を果たします。値はALLおよびANYがあり、デフォルト値はANYです。<br/><br><li> ALLは、すべてのインスタンスタイプ（InstanceType）が使用可能な場合は、検証に合格し、それ以外の場合は検証エラーが報告されます。<br/><br><li> ANYは、任意のインスタンスタイプ（InstanceType）が使用可能な場合は、検証に合格し、それ以外の場合は検証エラーが報告されます。<br/><br/>インスタンスタイプが使用できない一般的な原因は、インスタンスタイプの売り切れ、対応するクラウドディスクの売り切れなどです。<br/>InstanceTypesの1つのモデルが存在しないか既に無効だった場合、InstanceTypesCheckPolicyの値に関係なく、検証エラーが報告されます。 |
| LaunchConfigurationName | いいえ | String | 起動構成の名前。この名前は、中国語、英語、数字、アンダースコア、区切り記号「-」、小数点のみをサポートし、最大長は60バイトを超えることはできません。 |
| UserData | いいえ | String | Base64エンコード後のカスタムデータ。最大長は16KB以下です。UserDataをクリアしたい場合は、空の文字列として指定します |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1　起動構成の指定とイメージ、インスタンスタイプ、名前の変更

#### 入力例

```
https://as.tencentcloudapi.com/?Action=ModifyLaunchConfigurationAttributes
&LaunchConfigurationId=asc-291kq6ku
&ImageId=img-8toqc6s3
&InstanceTypes.0=S2.SMALL1
&LaunchConfigurationName=updated_config
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "RequestId": "07022dcb-5bba-48f0-a2b0-800ad006d031"
    }
}
```

### 例2　UserDataのクリア

#### 入力例

```
https://as.tencentcloudapi.com/?Action=ModifyLaunchConfigurationAttributes
&LaunchConfigurationId=asc-291kq6ku
&UserData=
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "RequestId": "2c027f22-3a3b-489a-a77a-89c53fc15212"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyLaunchConfigurationAttributes)

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
| InvalidParameterValue.CvmConfigurationError | CVMパラメータ検証が異常です。 |

