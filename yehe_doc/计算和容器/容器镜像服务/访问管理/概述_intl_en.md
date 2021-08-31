## Introduction to Cloud Access Management
Cloud access management (CAM) is a web service provided by Tencent Cloud. It helps users securely manage the permissions for accessing resources under their Tencent Cloud accounts. CAM allows you to create, manage, or terminate users (groups) and controls who can use Tencent Cloud resources through identity management and policy management.

When you use CAM, you can associate a policy with a user or a user group. The policy authorizes or refuses users to use the specified resource to complete the specified task. For more information on CAM policies, refer to [Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10603). For more information on how to use CAM policies, refer to [Policies](https://intl.cloud.tencent.com/document/product/598/10601).

If you do not need to perform access management of TCR resources for sub-accounts, you can skip this section. This does not affect your understanding and use of other sections of this document.

## CAM-based Resource-level Access Control of TCR
Resource-level permissions refer to the capabilities that can specify and allow users to perform specific operations on specific resources. TCR supports resource-level access control of CAM and controls the granularity to the repository level, that is, you can authorize sub-accounts to perform operations on resources in only the specified image repository or the Helm Chart repository by configuring the CAM policy.

Types of resources that can be authorized by TCR in CAM:

| Resource Type | Resource Description Method in Authorization Policy |
| :-------- | -------------- |
| Enterprise edition instance | `qcs::tcr:$region:$account:instance/*` |
| Enterprise edition repository | `qcs::tcr:$region:$account:repository/*` |
| Personal edition repository | `qcs::tcr:$region:$account:repo/*` |

- `$region`: the region information. For example, `ap-guangzhou` indicates the region of Guangzhou. If the value is null, the field indicates all regions. For the specific list of regions and abbreviations, refer to [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091).
- `$account`: the root account of the resource owner. The value is expressed as `uin/${uin}`, for example, `uin/12345678`. If the value is null, the field indicates the root account of the CAM user who creates the policy.
For details on resource description in the authorization policy, refer to [Resource Description](https://intl.cloud.tencent.com/document/product/598/10606).
