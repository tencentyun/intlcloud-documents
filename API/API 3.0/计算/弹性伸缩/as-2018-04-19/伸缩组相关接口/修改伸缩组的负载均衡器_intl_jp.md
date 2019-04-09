## 1. API説明

APIリクエストドメイン名：as.tencentcloudapi.com 。

このAPI（ModifyLoadBalancers）は、スケーリンググループのCLB装置を変更するために使用されます。

* このAPIは、スケーリンググループに新しいCLB装置の構成を指定するために使用され、「完全上書き」スタイルを採用し、以前の構成に関係なく、APIパラメータに従って新しいCLB装置に構成します。
* スケーリンググループのCLB装置をクリアしたい場合は、APIを呼び出す時にスケーリンググループIDのみを指定し、具体的なCLB装置を指定しません。
* このAPIは、スケーリンググループのCLB装置を即座に変更し、インベントリインスタンスのCLB装置を非同期的に変更するためのスケーリングアクティビティを生成します。

デフォルトのAPIリクエスト頻度制限：20回/秒。

注意：このAPIは金融区地域をサポートします。金融区と非金融区は分離されており、相互運用できないため、共通パラメータRegionが金融区地域（例えば、ap-shanghai-fsi）の場合は、金融区地域のドメイン名を同時に指定する必要があります。Region地域と一致するようにするのは一番です。例えば：as.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 入力パラメータ

次のリクエストパラメータリストには、APIリクエストパラメータと一部の共通パラメータのみがリストされています。完全な共通パラメータについては、[共通リクエストパラメータ](/document/api/377/20426)を参照してください。

| パラメータ名 | 必須項目 | タイプ | 説明 |
|---------|---------|---------|---------|
| Action | はい | String | 共通パラメータ、このAPIの値：ModifyLoadBalancers |
| Version | はい | String | 共通パラメータ、このAPIの値：2018-04-19 |
| Region | はい | String | 共通パラメータ、詳細については、製品がサポートする[地域リスト](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)を参照してください。 |
| AutoScalingGroupId | はい | String | スケーリンググループID |
| LoadBalancerIds.N | いいえ | Array of String | 伝統型CLB装置IDのリスト。現在の最大長は1です。LoadBalancerIdsとForwardLoadBalancersを同時に指定することはできません |
| ForwardLoadBalancers.N | いいえ | Array of [ForwardLoadBalancer](/document/api/377/20453#ForwardLoadBalancer) | アプリケーション型CLB装置リスト、現在の最大長は1です。LoadBalancerIdsとForwardLoadBalancersを同時に指定することはできません |

## 3. 出力パラメータ

| パラメータ名 | タイプ | 説明 |
|---------|---------|---------|
| ActivityId | String | スケーリングアクティビティID|
| RequestId | String | 唯一のリクエストID、リクエストごとに返します。問題を特定するときに、このリクエストのRequestIdが必要です。|

## 4. 例

### 例1　スケーリンググループのCLB装置を伝統型CLB装置lb-crhgatrfに変更します

#### 入力例

```
https://as.tencentcloudapi.com/?Action=ModifyLoadBalancers
&AutoScalingGroupId=asg-12wjuh0s
&LoadBalancerIds.0=lb-crhgatrf
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "ActivityId": "asa-67izy66g",
        "RequestId": "bd3c91e8-3051-4c02-ac58-54d47b9c9d63"
    }
}
```

### 例2　スケーリンググループのCLB装置をアプリケーション型CLB装置lb-23aejgcvに変更し、リスナーはlbl-ncw704snです

#### 入力例

```
https://as.tencentcloudapi.com/?Action=ModifyLoadBalancers
&AutoScalingGroupId=asg-12wjuh0s
&ForwardLoadBalancers.0.LoadBalancerId=lb-23aejgcv
&ForwardLoadBalancers.0.ListenerId=lbl-ncw704sn
&ForwardLoadBalancers.0.LocationId=loc-l3hmaev9
&ForwardLoadBalancers.0.TargetAttributes.0.Port=8080
&ForwardLoadBalancers.0.TargetAttributes.0.Weight=10
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "ActivityId": "asa-9asddelc",
        "RequestId": "8d78668d-61eb-456d-855b-f34f91371089"
    }
}
```

### 例3　スケーリンググループのCLB装置をクリアします

#### 入力例

```
https://as.tencentcloudapi.com/?Action=ModifyLoadBalancers
&AutoScalingGroupId=asg-12wjuh0s
&<共通リクエストパラメータ>
```

#### 出力例

```
{
    "Response": {
        "ActivityId": "asa-rp63a5q8",
        "RequestId": "7de5a82f-b781-4302-b723-e7a879c20767"
    }
}
```


## 5. 開発者リソース

### API Explorer

**このツールは、オンライン呼び出し、署名検証、SDKコードの生成、およびクイック検索APIなどの機能を提供し、クラウドAPIの使用難しさを大幅に軽減することができますので、お勧めします。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyLoadBalancers)

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
| InvalidParameterValue.ForwardLb | アプリケーション型CLB装置を誤って指定しました。 |
| InvalidParameterValue.LbProjectInconsistent | CLB装置のプロジェクトが一致しません。 |
| InvalidParameterValue.LbVpcInconsistent | CLB装置とスケーリンググループのVPCが一致しません。 |
| ResourceNotFound.AutoScalingGroupIdNotFound | スケーリンググループが存在しません。 |
| ResourceNotFound.LoadBalancerNotFound | 指定されたCLB装置が見つかりませんでした。 |
| ResourceUnavailable.AutoScalingGroupInActivity | スケーリンググループはアクティビティ中です。 |

