资源级权限指的是能够指定用户对哪些资源具有执行操作的能力。云服务器（Cloud Virtual Machine，CVM）部分支持资源级权限，即表示针对支持资源级权限的 CVM 操作，控制何时允许用户执行操作或是允许用户使用的特定资源。例如，您 [授权用户拥有广州地域的 CVM 操作权限](https://intl.cloud.tencent.com/document/product/213/10312)。
在访问管理（Cloud Access Management，CAM）中可授权的资源类型如下：

| 资源类型 | 授权策略中的资源描述方法 |
| :-------- | -------------- |
| [云服务器实例相关](#CVMCorrelation) |  ` qcs::cvm:$region::instance/* `|
| [云服务器密钥相关](#KeyCorrelation) |   `qcs::cvm:$region::keypair/*`  |
| [云服务器镜像相关](#ImageCorrelation) |   `qcs::cvm:$region:$account:image/*` |

[云服务器实例相关](#CVMCorrelation)、[云服务器密钥相关](#KeyCorrelation) 和 [云服务器镜像相关](#ImageCorrelation) 分别介绍了当前支持资源级权限的 CVM API 操作，以及每个操作支持的资源和条件密钥。**设置资源路径时，**您需要将`$region`、`$account`等变量参数修改为您实际的参数信息，同时您也可以在路径中使用 \* 通配符。相关操作示例可参见 [访问管理示例](https://intl.cloud.tencent.com/document/product/213/10312)。
> 表中未列出的 CVM API 操作即表示该 CVM API 操作不支持资源级权限。针对不支持资源级权限的 CVM API 操作，您仍可以向用户授予使用该操作的权限，但是策略语句的资源元素必须指定为 \*。
>

<span id="CVMCorrelation"></span>
#### 云服务器实例相关

| API 操作 | 资源路径 | 条件密钥 |
| :-------- | :--------| :------ |
|DescribeInstanceInternetBandwidthConfigs	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|ModifyInstanceInternetChargeType	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ModifyInstancesAttribute](https://intl.cloud.tencent.com/document/product/213/33246)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`  | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ModifyInstancesProject](https://intl.cloud.tencent.com/document/product/213/33245)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|ModifyInstancesRenewFlag	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[RebootInstances](https://intl.cloud.tencent.com/document/product/213/33243)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|RenewInstances	|  `qcs::cvm:$region:$account:instance/* `<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstance](https://intl.cloud.tencent.com/document/product/213/33242)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`<br>`qcs::cvm:$region:$account:systemdisk/*` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstancesInternetMaxBandwidth](https://intl.cloud.tencent.com/document/product/213/33241)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstancesPassword](https://intl.cloud.tencent.com/document/product/213/33240)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstancesType](https://intl.cloud.tencent.com/document/product/213/33239)	|  `qcs::cvm:$region:$account:instance/* `<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResizeInstanceDisks](https://intl.cloud.tencent.com/document/product/213/33238)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[RunInstances](https://intl.cloud.tencent.com/document/product/213/33237)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`<br>`qcs::cvm:$region:$account:sg/*`<br>`qcs::cvm:$region:$account:sg/$sgId`<br>`qcs::vpc:$region:$account:subnet/* `<br>`qcs::vpc:$region:$account:subnet/$subnetId`<br>`qcs::cvm:$region:$account:systemdisk/*`<br>`qcs::cvm:$region:$account:datadisk/*`<br>`qcs::vpc:$region:$account:vpc/* `<br>`qcs::vpc:$region:$account:vpc/$vpcId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[StartInstances](https://intl.cloud.tencent.com/document/product/213/33236)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[StopInstances](https://intl.cloud.tencent.com/document/product/213/33235)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[TerminateInstances](https://intl.cloud.tencent.com/document/product/213/33234)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|


<span id="KeyCorrelation"></span>
#### 云服务器密钥相关

| API 操作 | 资源路径 | 条件密钥 |
| :-------- | :--------| :------ |
|[AssociateInstancesKeyPairs](https://intl.cloud.tencent.com/document/product/213/33232)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`  | -|
|[CreateKeyPair](https://intl.cloud.tencent.com/document/product/213/33231)	|  `qcs::cvm:$region:$account:keypair/*` | -|
|[DeleteKeyPairs](https://intl.cloud.tencent.com/document/product/213/33230)	|  `qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|
|[DescribeKeyPairs](https://intl.cloud.tencent.com/document/product/213/33229)	|  `qcs::cvm:$region:$account:keypair/*` | -|
|DescribeKeyPairsAttribute	|  `qcs::cvm:$region:$account:keypair/*`<br>` qcs::cvm:$region:$account:keypair/$keyId` | -|
| [DisassociateInstancesKeyPairs](https://intl.cloud.tencent.com/document/product/213/33228)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|
|[ImportKeyPair](https://intl.cloud.tencent.com/document/product/213/33227)	|  `qcs::cvm:$region:$account:keypair/*` | -|
|[ModifyKeyPairAttribute](https://intl.cloud.tencent.com/document/product/213/33226)	|  `qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|

<span id="ImageCorrelation"></span>
#### 云服务器镜像相关

| API 操作 | 资源路径 | 条件密钥 |
| :-------- | :--------| :------ |
| [CreateImage](https://intl.cloud.tencent.com/document/product/213/33276)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br> `qcs::cvm:$region:$account:image/*` | cvm:region |
| [DeleteImages](https://intl.cloud.tencent.com/document/product/213/33275)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
|[DescribeImages](https://intl.cloud.tencent.com/document/product/213/33272)| `qcs::cvm:$region:$account:image/*`|cvm:region|
| DescribeImagesAttribute	|  `qcs::cvm:$region:$account:image/*`<br>` qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [DescribeImageSharePermission](https://intl.cloud.tencent.com/document/product/213/33273)	|  `qcs::cvm:$region:$account:image/*` | cvm:region |
| [ModifyImageAttribute](https://intl.cloud.tencent.com/document/product/213/33269)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [ModifyImageSharePermission](https://intl.cloud.tencent.com/document/product/213/33268)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [SyncImages](https://intl.cloud.tencent.com/document/product/213/33267)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |







