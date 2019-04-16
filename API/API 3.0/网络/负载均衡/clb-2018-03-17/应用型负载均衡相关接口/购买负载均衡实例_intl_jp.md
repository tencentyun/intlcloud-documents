## 1. API説明

APIリクエストドメイン名：clb.tencentcloudapi.com。

CreateLoadBalancer APIは、ロードバランサーインスタンスを作成するために使用されます。CLBサービスを使用するために、1つまたは複数のロードバランサーインスタンスを購入しなければなりません。このAPIを成功に呼び出すことにより、ロードバランサーインスタンスの一意のIDが返されます。ユーザーが購入することができるロードバランサーインスタンスのタイプは、パブリックネットワーク（アプリケーション型）とプライベートネットワーク（アプリケーション型）に分かれます。製品説明の製品タイプを参照することができます。
このAPIが正常に返した後、ロードバランサーインスタンスリスト照合API DescribeLoadBalancersを使用してロードバランサーインスタンスのステータスを照合することができ、それにより作成できたか特定します。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互通信できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例：clb.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータのリストについては、[共通リクエストパラメータ](/document/api/214/30670)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：CreateLoadBalancer |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-03-17 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/214/30670#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| LoadBalancerType | はい | String | ロードバランサーインスタンスのネットワークタイプ。<br/>OPEN：パブリックネットワーク属性、INTERNAL：プライベートネットワーク属性。 |
| Forward | いいえ | Integer | ロードバランサーインスタンス。1：アプリケーション型、0：従来型。デフォルトはアプリケーション型ロードバランサーインスタンスです。 |
| LoadBalancerName | いいえ | String | ロードバランサーインスタンス名であり、1つだけ作成した時に有効になります。規則は、1～50の英語、日本語、数字、接続線「-」または下線「_」です。<br/>注意：名称がシステム中のロードバランサーインスタンス名と重複した場合、システムは今回作成されたロードバランサーインスタンスの名称を自動的に生成します。 |
| VpcId | いいえ | String | CLBバックエンドインスタンスが所属するネットワークIDであり、DescribeVpcEx APIを介して取得することができます。入力しない場合、デフォルトは基本ネットワークとなります。 |
| SubnetId | いいえ | String | VPCにおいてプライベートネットワークロードバランサーインスタンスを購入する時にサブネットIDを指定する必要があり、プライベートネットワークロードバランサーインスタンスのVIPはこのサブネットから生成します。その他の状況は、このフィールドを記入する必要はありません。 |
| ProjectId | いいえ | Integer | ロードバランサーインスタンスの所属するプロジェクトIDであり、DescribeProject APIを介して取得することができます。入力しない場合、デフォルトのプロジェクトに所属します。 |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| LoadBalancerIds | Array of String | ロードバランサーインスタンスの統一IDにより構成される配列。|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1 パブリックネットワークのアプリケーション型LBインスタンスの作成

#### 入力例

```
https://clb.tencentcloudapi.com/?Action=CreateLoadBalancer
&LoadBalancerType=OPEN
&Forward=1
&LoadBalancerName=test
&ProjectId=0
&<共通リクエストパラメータ>
```

#####　出力例

```
{
    "Response": {
        "LoadBalancerIds": [
            "lb-6efswuxa"
        ],
        "RequestId": "9b3f0b57-fb64-4918-8dd6-ce02604fb52c"
    }
}
```

### 例2 プライベートネットワークのアプリケーション型LBインスタンスの作成

#### 入力例

```
https://clb.tencentcloudapi.com/?Action=CreateLoadBalancer
&LoadBalancerType=INTERNAL
&Forward=1
&LoadBalancerName=test_internal
&VpcId=vpc-30xqxt9p
&SubnetId=subnet-k57djpow
&<共通リクエストパラメータ>
```

#####　出力例

```
{
    "Response": {
        "LoadBalancerIds": [
            "lb-kmfrnqci"
        ],
        "RequestId": "7ffa6830-cd1b-4bc4-8e24-1688885f594a"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールはオンライン呼び出し、署名の検証、SDKコード生成と高速検索APIなどの機能を提供し、クラウドAPI使用の難易度を大幅に低減することができるため、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=clb&Version=2018-03-17&Action=CreateLoadBalancer)

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

以下に、APIビジネスロジックに関連するエラーコードのみをリストします。その他のエラーコードについては、[共通エラーコード](/document/api/214/30673#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)を参照してください。

| エラーコード | 説明 |
|---------|---------|
| FailedOperation | 操作失敗 |
| InternalError | 内部エラー |
| InvalidParameter | パラメータエラー。 |
| InvalidParameterValue | パラメータ値エラー |
| LimitExceeded | 割り当て量の制限を超えました |
| ResourceInsufficient | リソースが足りません |
| UnauthorizedOperation | 操作が承認されていません |

