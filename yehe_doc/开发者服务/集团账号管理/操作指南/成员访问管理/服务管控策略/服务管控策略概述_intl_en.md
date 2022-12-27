A service control policy in TCO is an access control policy based on a hierarchical structure (department and member). It can uniformly manage the access permission boundaries of resources at each level within an organization and thus establish global or local access control rules. It only defines the permission boundaries and does not actually grant permissions. You still need to set permissions in CAM for a member account to access certain resources.

## Use cases

After you create an organization and create members under each department, if you don't control the behaviors of members, the Ops rules will be violated, causing security risks and increasing costs. TCO provides the service control policy feature. You can centrally create management rules through account management and apply them to different structure levels such as departments and members. This enables you to better manage the access rules of resources for members, ensure the security compliance, and control costs. For example, you can use this feature to forbid a member from applying for domain names or deleting logs.

## Service control policy types

- System service control policy

This type refers to the service control policies that are preset in the system. You can view them but cannot create, modify, or delete them. After the service control policy feature is enabled, all departments and members in your organization are bound to the system policy `FullQcloudAccess` by default, which allows them to perform any operations on all your Tencent Cloud resources.

- Custom service control policy

This type refers to the service control policies that you customize. You can create, modify, and delete such policies. After creating a custom policy, you need to bind it to a department or member for it to take effect. You can also unbind it at any time.

## How a service control policy works

1. Enable the service control policy feature with the admin account as instructed in [Enabling Service Control Policy](https://www.tencentcloud.com/document/product/1031/51870).

2. After the service control policy feature is enabled, the system policy `FullQcloudAccess` will be bound to all departments and members in your organization by default. This policy allows all actions in order to avoid access failures caused by improper policy configuration.

3. Create a service control policy with the admin account as instructed in [Creating Custom Service Control Policy](https://www.tencentcloud.com/document/product/1031/51871).

4. Bind the service control policy to an organization node such as department or member with the admin account as instructed in [Binding Custom Service Control Policy](https://www.tencentcloud.com/document/product/1031/51875).

5. A service control policy can be bound to departments and members in the organization and can be inherited by lower nodes. For example, if you set service control policy A for the parent department and policy B for a child department, both policies A and B will take effect for the child department and its members.
<dx-alert infotype="notice" title="">
**Perform a local test first to ensure that the policy works as expected before binding it to all target nodes such as departments and members.**
</dx-alert>
6. When a CAM user or role among members accesses a Tencent Cloud service, Tencent Cloud will first check its associated service control policies and then check CAM permissions under the account as follows:

(1) Authentication with service control policies starts from the account of the accessed resource and continues upward level by level in the organization.

(2) If the action is denied by a service control policy at a level, the authentication result will be "Explicit Deny", the entire authentication process will end, authentication with the account's CAM permission policies won't be performed, and the request will be directly denied.

(3) If the action is neither denied nor allowed by a service control policy at a level, the authentication result will also be "Explicit Deny", authentication won't proceed to the next level, the entire authentication process will end, authentication with the account's CAM permission policies won't be performed, and the request will be directly denied.

(4) If the action hits an allow policy at a level, authentication will pass at this level and proceed to the parent node until the root. If authentication at the root level also passes, the entire authentication will pass, and authentication with the account's CAM permission policies will be performed.

(5) Service control policies don't take effect for the service's associated roles.

(6) Tencent Cloud will assess the service control policies of the accessed account as well as those bound to its nodes at each level, so as to ensure that the policies bound to nodes at a higher level can take effect for all accounts under it.