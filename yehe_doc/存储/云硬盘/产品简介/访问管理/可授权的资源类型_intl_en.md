Resource-level permissions refer to the permissions granted to users at the level of resources. Resource-level permission control allows you to specify the resources that can be operated on by users. Cloud Block Storage (CBS) partially supports resource-level permission control. For CBS operations that support resource-level permission control, you can control when to allow users to perform the operations or use specific resources.
In Cloud Access Management (CAM), the types of resources that can be granted are shown below.

| Resource Type | Resource Description Method in Authorization Policies |
| :-------- | -------------- |
| [CBS instance resources](#CBSCorrelation) | `qcs::cvm:$region::volume/*` |

[CBS instance resources](#CBSCorrelation) describe CBS API operations that support resource-level permission control, and their resources and condition keys. **When setting a resource path**, you need to change the values of parameters such as `$region` and `$account` to your actual values. You can also use the wildcard `*` in a path. For operation examples, see [CAM Examples](https://intl.cloud.tencent.com/document/product/213/10312).
> Any CBS API operation that is not listed in the table does not support resource-level permission control. You can still authorize a user to perform these operations, but you must specify `*` as the resource element in the policy statement.
>

<span id="CBSCorrelation"></span>
### CBS instance resources

| API Operation | Resource Path | Condition Key |
| :-------- | :--------| :------ |
| [AttachDisks](https://intl.cloud.tencent.com/document/product/362/16313) | `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId` | cvm:region<br>cvm:zone<br>cvm:disk_type |
| [CreateDisks](https://intl.cloud.tencent.com/document/product/362/16312) | `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId` | cvm:region<br>cvm:zone<br>cvm:disk_type |
| [DescribeDiskOperationLogs](https://intl.cloud.tencent.com/document/product/362/32170) | `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId` | cvm:region<br>cvm:zone<br>cvm:disk_type |
| [DescribeDisks](https://intl.cloud.tencent.com/document/product/362/16315) | `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId` | cvm:region<br>cvm:zone<br>cvm:disk_type |
| [DetachDisks](https://intl.cloud.tencent.com/document/product/362/16316) | `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId` | cvm:region<br>cvm:zone<br>cvm:disk_type |
| [ModifyDiskAttributes](https://intl.cloud.tencent.com/document/product/362/15659) | `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId` | cvm:region<br>cvm:zone<br>cvm:disk_type |
| ModifyDisksChargeType | `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId` | cvm:region<br>cvm:zone<br>cvm:disk_type |
| ModifyDisksRenewFlag | `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId` | cvm:region<br>cvm:zone<br>cvm:disk_type |
| RenewDisk | `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId` | cvm:region<br>cvm:zone<br>cvm:disk_type |
| [ResizeDisk](https://intl.cloud.tencent.com/document/product/362/16310) | `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId` | cvm:region<br>cvm:zone<br>cvm:disk_type |
| [TerminateDisks](https://intl.cloud.tencent.com/document/product/362/16321) | `qcs::cvm:$region:$account:volume/*`<br>`qcs::cvm:$region:$account:volume/$diskId` | cvm:region<br>cvm:zone<br>cvm:disk_type |







