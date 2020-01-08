リソースレベル権限とは、ユーザーがどのリソースを操作できるかを指定する機能のことです。CVMはリソースレベル権限を部分的にサポートしています。つまり、リソースレベル権限をサポートするCVM操作に対して、いつ操作を実行することを許可するかまたは特定のリソースを利用できるかを制御します。例えば、[ユーザーに広州リージョンのCVMの操作権限を許可する](https://intl.intl.cloud.tencent.com/document/product/213/10312)。
Cloud Access Management（CAM）で、操作権限を許可できるリソースの種類は以下の通り：

| リソース種類 | 許可ポリシーのリソース記述方法 |
| :-------- | -------------- |
| [CVMインスタンス関連](#CVMCorrelation) |  ` qcs::cvm:$region::instance/* `|
| [CVMキー関連](#KeyCorrelation) |   `qcs::cvm:$region::keypair/*`  |
| [CVMイメージ関連](#ImageCorrelation) |   `qcs::cvm:$region:$account:image/*` |

[CVMインスタンス関連](#CVMCorrelation)、[CVMキー関連](#KeyCorrelation) と[CVMイメージ関連](#ImageCorrelation) は現在リソースレベル権限をサポートするCVM API操作及び各操作がサポートするリソースと条件キーを説明します。**リソースパスを設定する時、**`$region`、`$account`等の変数パラメータを実際のパラメータ情報に修正する必要があり、同時にパスの中にワイルドカード \* を利用できます。関連する操作事例は [Cloud Access Management事例](https://intl.cloud.tencent.com/document/product/213/10312)をご参照ください。
> 表にリストされていないCVM API操作とは、このAPIがリソースレベル権限をサポートしていないことを示します。リソースレベル権限をサポートしていないCVM API操作に対して、ユーザーにこの操作を利用する権限を許可できますが、ポリシーステートメントのリソース要素を\*に指定する必要があります。
>

<span id="CVMCorrelation"></span>
#### CVMインスタンス関連

| API 操作 | リソースパス | 条件キー |
| :-------- | :--------| :------ |
|[DescribeInstanceInternetBandwidthConfigs](https://cloud.tencent.com/document/product/213/15734)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|ModifyInstanceInternetChargeType	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ModifyInstancesAttribute](https://cloud.tencent.com/document/product/213/15739)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`  | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ModifyInstancesProject](https://cloud.tencent.com/document/product/213/15746)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ModifyInstancesRenewFlag](https://cloud.tencent.com/document/product/213/15752)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[RebootInstances](https://cloud.tencent.com/document/product/213/15742)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[RenewInstances](https://cloud.tencent.com/document/product/213/15740)	|  `qcs::cvm:$region:$account:instance/* `<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstance](https://cloud.tencent.com/document/product/213/15724)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`<br>`qcs:::cvm:$region:$account:systemdisk/*` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstancesInternetMaxBandwidth](https://cloud.tencent.com/document/product/213/15721)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstancesPassword](https://cloud.tencent.com/document/product/213/15736)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstancesType](https://cloud.tencent.com/document/product/213/15744)	|  `qcs::cvm:$region:$account:instance/* `<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResizeInstanceDisks](https://cloud.tencent.com/document/product/213/15731)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[RunInstances](https://cloud.tencent.com/document/product/213/15730)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`<br>`qcs::cvm:$region:$account:sg/*`<br>`qcs::cvm:$region:$account:sg/$sgId`<br>`qcs::vpc:$region:$account:subnet/* `<br>`qcs::vpc:$region:$account:subnet/$subnetId`<br>`qcs:::cvm:$region:$account:systemdisk/*`<br>`qcs::cvm:$region:$account:datadisk/*`<br>`qcs::vpc:$region:$account:vpc/* `<br>`qcs::vpc:$region:$account:vpc/$vpcId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[StartInstances](https://cloud.tencent.com/document/product/213/15735)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[StopInstances](https://cloud.tencent.com/document/product/213/15743)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[TerminateInstances](https://cloud.tencent.com/document/product/213/15723)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|


<span id="KeyCorrelation"></span>
#### CVMキー関連

| API 操作 | リソースパス | 条件キー |
| :-------- | :--------| :------ |
|[AssociateInstancesKeyPairs](https://cloud.tencent.com/document/product/213/15698)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`  | -|
|[CreateKeyPair](https://cloud.tencent.com/document/product/213/15702)	|  `qcs::cvm:$region:$account:keypair/*` | -|
|[DeleteKeyPairs](https://cloud.tencent.com/document/product/213/15700)	|  `qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|
|[DescribeKeyPairs](https://cloud.tencent.com/document/product/213/15699)	|  `qcs::cvm:$region:$account:keypair/*` | -|
|DescribeKeyPairsAttribute	|  `qcs::cvm:$region:$account:keypair/*`<br>` qcs::cvm:$region:$account:keypair/$keyId` | -|
| [DisassociateInstancesKeyPairs](https://cloud.tencent.com/document/product/213/15697)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|
|[ImportKeyPair](https://cloud.tencent.com/document/product/213/15703)	|  `qcs::cvm:$region:$account:keypair/*` | -|
|[ModifyKeyPairAttribute](https://cloud.tencent.com/document/product/213/15701)	|  `qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|

<span id="ImageCorrelation"></span>
#### CVMイメージ関連

| API 操作 | リソースパス | 条件キー |
| :-------- | :--------| :------ |
| [CreateImage](https://cloud.tencent.com/document/product/213/16726)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br> `qcs::cvm:$region:$account:image/*` | cvm:region |
| [DeleteImages](https://cloud.tencent.com/document/product/213/15716)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
|[DescribeImages](https://cloud.tencent.com/document/product/213/15715)| `qcs::cvm:$region:$account:image/*`|cvm:region|
| DescribeImagesAttribute	|  `qcs::cvm:$region:$account:image/*`<br>` qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [DescribeImageSharePermission](https://cloud.tencent.com/document/product/213/15712)	|  `qcs::cvm:$region:$account:image/*` | cvm:region |
| [ModifyImageAttribute](https://cloud.tencent.com/document/product/213/15713)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [ModifyImageSharePermission](https://cloud.tencent.com/document/product/213/15710)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [SyncImages](https://cloud.tencent.com/document/product/213/15711)|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |







