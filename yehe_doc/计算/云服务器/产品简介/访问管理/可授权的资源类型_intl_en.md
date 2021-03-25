Resource-level permission refers to the ability to specify which resources users are allowed to operate on. Cloud Virtual Machine(CVM) has partial support for resource-level permission. This means that for certain CVMs, you can control when users are allowed to operate on them, and what specific resources users are allowed to use. For example, you [authorize users to perform operations on specific CVMs in Guangzhou](https://intl.cloud.tencent.com/document/product/213/10312).
The types of resources can be authorized in Cloud Access Management (CAM) are as follows:

| Resource Type | Resource Description Method in Authorization Policy |
| :-------- | -------------- |
| [CVM Instance](#CVMCorrelation) |  ` qcs::cvm:$region::instance/* `|
| [CVM Key](#KeyCorrelation) |   `qcs::cvm:$region::keypair/*`  |
| [CVM Image](#ImageCorrelation) |   `qcs::cvm:$region:$account:image/*` |

[CVM Instance](#CVMCorrelation), [CVM Key](#KeyCorrelation) and [CVM Image](#ImageCorrelation) introduce CVM API operations that currently support resource-level permission, as well as resources and condition keys supported by these CVM API operations. **When configuring the resource path,** you need to change variable parameters such as `$ region`, ` $ account` into your actual parameter information. You can also use wildcard \* in the path. For more information, see [Operation Examples](https://intl.cloud.tencent.com/document/product/213/10312).
> CVM API operations not listed in the table do not support resource-level permission. You can still authorize a user to perform these operations, but you must specify \* as the resource element in the policy statement.
>

<span id="CVMCorrelation"></span>
#### CVM Instance

| API Operation | Resource Path | Condition Key |
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
#### CVM Key

| API Operation | Resource Path | Condition Key |
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
#### CVM Image

| API Operation | Resource Path | Condition Key |
| :-------- | :--------| :------ |
| [CreateImage](https://intl.cloud.tencent.com/document/product/213/33276)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br> `qcs::cvm:$region:$account:image/*` | cvm:region |
| [DeleteImages](https://intl.cloud.tencent.com/document/product/213/33275)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
|[DescribeImages](https://intl.cloud.tencent.com/document/product/213/33272)| `qcs::cvm:$region:$account:image/*`|cvm:region|
| DescribeImagesAttribute|  `qcs::cvm:$region:$account:image/*`<br>` qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [DescribeImageSharePermission](https://intl.cloud.tencent.com/document/product/213/33273)	|  `qcs::cvm:$region:$account:image/*` | cvm:region |
| [ModifyImageAttribute](https://intl.cloud.tencent.com/document/product/213/33269)|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [ModifyImageSharePermission](https://intl.cloud.tencent.com/document/product/213/33268)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [SyncImages](https://intl.cloud.tencent.com/document/product/213/33267)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |







