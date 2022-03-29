>!Since the product logic no longer meets the technical development of game industry, Game Player Matching GPM will be deprecated on June 1st, 2022. Please complete service migration before May 31 , 2022.

Tencent Cloud CAM is a web service that helps customers securely manage and control access to their Tencent Cloud resources. CAM provides identity management and policy management for you to create, manage or terminate users (groups), and to control who is allowed to access and use your Tencent Cloud resources.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, see [Syntax Logic](https://intl.cloud.tencent.com/document/product/598/10603). For more information on the use of CAM policies, see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).

If you use multiple Tencent Cloud services such as GPM and GSE that are managed by different users sharing your cloud account key, the following problems may arise:
- The risk of your key being compromised is high since multiple users are sharing it.
- Your users might introduce security risks from misoperations due to the lack of user access control.

You can avoid the problems above by allowing different users to manage different services through sub-accounts. By default, a sub-account does not have permissions to use GPM service or related resources. Therefore, you need to create a policy to grant different permissions to the sub-accounts. You can skip this section if you do not need to manage permissions to GPM resources for sub-accounts. This will not affect your understanding and use of the other sections of the document.

## Notes

A CAM policy is used to allow or deny one or more GPM operations. When configuring a policy, you must specify the target resources of the operations, which can be all resources or specified resources. A policy can also include conditions where the resources can be used.

Some GPM APIs do not support resource-level permissions, which means that you cannot specify resources when using those APIs.

| Task | Reference Documents |
| -------------------- | ------------------------------------------------------------ |
| Basic policy structure | [Policy Syntax](https://intl.cloud.tencent.com/document/product/1072/39213) |
| Define operations in a policy | [GPM Operations](https://intl.cloud.tencent.com/document/product/1072/39213) |
| Define resources in a policy | [GPM Resource Path](https://intl.cloud.tencent.com/document/product/1072/39213) |
| Resource-level permissions for GPM | [Authorizable Resource Types](https://intl.cloud.tencent.com/document/product/1072/39212) |
| View console examples | [Access Management Examples](https://intl.cloud.tencent.com/document/product/1072/39211) |



