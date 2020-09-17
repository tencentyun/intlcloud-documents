リソースレベル権限とは、ユーザーがどのリソースを操作できるかを指定する機能のことです。CVMはリソースレベル権限を部分的にサポートしています。つまり、リソースレベル権限をサポートするCVM操作に対して、いつ操作を実行することを許可するかまたは特定のリソースを利用できるかを制御します。
Cloud Access Management（CAM）で、操作権限を許可できるリソースの種類は以下の通り：

| リソース種類 | 許可ポリシーのリソース記述方法 |
| :-------- | -------------- |
| CVMインスタンス関連 |  ` qcs::cvm:$region::instance/* `|
| CVMキー関連 |   `qcs::cvm:$region::keypair/*`  |
| CVMイメージ関連 |   `qcs::cvm:$region:$account:image/*` |
| セキュリティグループ関連 |   `qcs::cvm:$region:$account:sg/*` |


現在リソースレベル権限をサポートするCVM API操作及び各操作がサポートするリソースと条件キーを説明します。**リソースパスを設定する時、**`$region`、`$account`等の変数パラメータを実際のパラメータ情報に修正する必要があり、同時にパスの中にワイルドカード \* を利用できます。
> 表にリストされていないCVM API操作とは、このAPIがリソースレベル権限をサポートしていないことを示します。リソースレベル権限をサポートしていないCVM API操作に対して、ユーザーにこの操作を利用する権限を許可できますが、ポリシーステートメントのリソース要素を\*に指定する必要があります。
>

<span id="CVMCorrelation"></span>
#### CVMインスタンス関連

| API 操作 | リソースパス | 条件キー |
| :-------- | :--------| :------ |
|DescribeInstanceInternetBandwidthConfigs	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|ModifyInstanceInternetChargeType	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|ModifyInstancesAttribute	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`  | cvm:region<br>cvm:zone<br>cvm:instance_type|
|ModifyInstancesProject	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|ModifyInstancesRenewFlag	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|RebootInstances	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|RenewInstances	|  `qcs::cvm:$region:$account:instance/* `<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|ResetInstance	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`<br>`qcs::cvm:$region:$account:systemdisk/*` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|ResetInstancesInternetMaxBandwidth	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|ResetInstancesPassword	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|ResetInstancesType	|  `qcs::cvm:$region:$account:instance/* `<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|ResizeInstanceDisks	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|RunInstances	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`<br>`qcs::cvm:$region:$account:sg/*`<br>`qcs::cvm:$region:$account:sg/$sgId`<br>`qcs::vpc:$region:$account:subnet/* `<br>`qcs::vpc:$region:$account:subnet/$subnetId`<br>`qcs::cvm:$region:$account:systemdisk/*`<br>`qcs::cvm:$region:$account:datadisk/*`<br>`qcs::vpc:$region:$account:vpc/* `<br>`qcs::vpc:$region:$account:vpc/$vpcId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|StartInstances	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|StopInstances	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|TerminateInstances	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
<span id="KeyCorrelation"></span>




#### CVMキー関連

| API 操作 | リソースパス | 条件キー |
| :-------- | :--------| :------ |
|AssociateInstancesKeyPairs	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`  | -|
|CreateKeyPair	|  `qcs::cvm:$region:$account:keypair/*` | -|
|DeleteKeyPairs	|  `qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|
|DescribeKeyPairs	|  `qcs::cvm:$region:$account:keypair/*` | -|
|DescribeKeyPairsAttribute	|  `qcs::cvm:$region:$account:keypair/*`<br>` qcs::cvm:$region:$account:keypair/$keyId` | -|
| DisassociateInstancesKeyPairs	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|
|ImportKeyPair	|  `qcs::cvm:$region:$account:keypair/*` | -|
|ModifyKeyPairAttribute	|  `qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|


#### CVMイメージ関連

| API 操作 | リソースパス | 条件キー |
| :-------- | :--------| :------ |
| CreateImage	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br> `qcs::cvm:$region:$account:image/*` | cvm:region |
| DeleteImages	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
|DescribeImages| `qcs::cvm:$region:$account:image/*`|cvm:region|
| DescribeImagesAttribute	|  `qcs::cvm:$region:$account:image/*`<br>` qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| DescribeImageSharePermission	|  `qcs::cvm:$region:$account:image/*` | cvm:region |
| ModifyImageAttribute	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| ModifyImageSharePermission	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| SyncImages	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |


#### セキュリティグループ関連
| API 操作 | リソースパス | 条件キー |
| :-------- | :--------| :------ |
| ModifySecurityGroupPolicys	|  `qcs::cvm:$region:$account:sg/*`<br>`qcs::cvm:$region:$account:sg/$sgId`| `cvm:projectId`<br>`cvm:region` |
| ModifySingleSecurityGroupPolicy	|  `qcs::cvm:$region:$account:sg/*`<br>`qcs::cvm:$region:$account:sg/$sgId`| `cvm:projectId`<br>`cvm:region` |
| CreateSecurityGroupPolicy	|  `qcs::cvm:$region:$account:sg/*`<br>`qcs::cvm:$region:$account:sg/$sgId`| `cvm:projectId`<br>`cvm:region` |
| ModifySecurityGroupAttributes	|  `qcs::cvm:$region:$account:sg/*`<br>`qcs::cvm:$region:$account:sg/$sgId`| `cvm:projectId`<br>`cvm:region` |
| DeleteSecurityGroup	|  `qcs::cvm:$region:$account:sg/*`<br>`qcs::cvm:$region:$account:sg/$sgId`| `cvm:projectId`<br>`cvm:region` |
| DeleteSecurityGroupPolicy	|  `qcs::cvm:$region:$account:sg/*`<br>`qcs::cvm:$region:$account:sg/$sgId`| `cvm:projectId`<br>`cvm:region` |
