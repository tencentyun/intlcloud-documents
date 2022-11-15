>!If you do not need to manage permissions to International Partners resources for sub-accounts, you can skip this section, and this won’t affect your understanding and use of other documents.

If you use multiple Tencent Cloud services such as Cloud Virtual Machine (CVM), VPC, and TencentDB that are managed by different users sharing your cloud account key, you may face the following problems:
- Your key will be easily compromised because it is shared by several users.
- You cannot restrict the access from other users and your service will be vulnerable to the security risks caused by their misoperations.

You can avoid the problems above by allowing different users to manage different services through sub-accounts. By default, a sub-account has no access to International Partners. Therefore, you need to create a policy to grant different permissions to the sub-accounts.

Cloud Access Management (CAM) is a Tencent Cloud web service that helps you securely manage and control access to your Tencent Cloud resources. CAM allows you to create, manage or terminate users (groups), and control who have access to which Tencent Cloud resources based on identity and policy management.

You can use CAM to bind a user or user group to a policy that allows or denies their access to specified resources to complete specified tasks.

- For more information on CAM sub-users, see [Creating Sub-User](https://intl.cloud.tencent.com/document/product/598/13674).

- For more information on CAM policies, see [Policies](https://www.tencentcloud.com/document/product/598/32668).
