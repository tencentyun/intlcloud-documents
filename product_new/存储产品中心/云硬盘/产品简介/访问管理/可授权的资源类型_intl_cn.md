资源级权限指的是能够指定用户对哪些资源具有执行操作的能力。云硬盘（CBS）支持资源级权限，即表示针对支持资源级权限的 CBS 操作，控制何时允许用户执行操作或是允许用户使用的特定资源。
在访问管理（Cloud Access Management，CAM）中可授权的资源类型如下：

| 资源类型 | 授权策略中的资源描述方法 |
| :-------- | -------------- |
| [云硬盘实例相关](#CBSCorrelation) |  ` qcs::cvm:$region::volume/* `|

[云硬盘实例相关](#CBSCorrelation) 介绍了当前支持资源级权限的 CBS API 操作，以及每个操作支持的资源和条件密钥。**设置资源路径时，**您需要将`$region`、`$account`等变量参数修改为您实际的参数信息，同时您也可以在路径中使用 `*` 通配符。相关操作示例可参见 [访问管理示例](https://intl.cloud.tencent.com/document/product/213/10312)。
> 表中未列出的 CBS API 操作即表示该 API 操作不支持资源级权限。针对不支持资源级权限的 API 操作，您仍可以向用户授予使用该操作的权限，但是策略语句的资源元素必须指定为 `*`。
>

<span id="CBSCorrelation"></span>
### 云硬盘实例相关

| API 操作 | 资源路径 | 条件密钥 |
| :-------- | :--------| :------ |
|[AttachDisks](https://intl.cloud.tencent.com/document/product/362/16313)	|  `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId`| cvm:region<br>cvm:zone<br>cvm:disk_type|
|[CreateDisks](https://intl.cloud.tencent.com/document/product/362/16312)	|  `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId`| cvm:region<br>cvm:zone<br>cvm:disk_type|
|[DescribeDiskOperationLogs](https://intl.cloud.tencent.com/document/product/362/32170)|  `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId`| cvm:region<br>cvm:zone<br>cvm:disk_type|
|[DescribeDisks](https://intl.cloud.tencent.com/document/product/362/16315)	|  `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId`| cvm:region<br>cvm:zone<br>cvm:disk_type|
|[DetachDisks](https://intl.cloud.tencent.com/document/product/362/16316)	|  `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId`| cvm:region<br>cvm:zone<br>cvm:disk_type|
|[ModifyDiskAttributes](https://intl.cloud.tencent.com/document/product/362/15659)	|  `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId`| cvm:region<br>cvm:zone<br>cvm:disk_type|
|ModifyDisksChargeType	|  `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId`| cvm:region<br>cvm:zone<br>cvm:disk_type|
|ModifyDisksRenewFlag	|  `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId`| cvm:region<br>cvm:zone<br>cvm:disk_type|
|RenewDisk	|  `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId`| cvm:region<br>cvm:zone<br>cvm:disk_type|
|[ResizeDisk](https://intl.cloud.tencent.com/document/product/362/16310)	|  `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId`| cvm:region<br>cvm:zone<br>cvm:disk_type|
|[TerminateDisks](https://intl.cloud.tencent.com/document/product/362/16321)	|  `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId`| cvm:region<br>cvm:zone<br>cvm:disk_type|







