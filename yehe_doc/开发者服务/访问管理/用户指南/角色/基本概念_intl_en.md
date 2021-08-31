Before you get started with roles, familiarize yourself with the basic terms, such as role, service role, custom role, role entity, and permission policy. For more terms, please see [Glossary](https://intl.cloud.tencent.com/document/product/598/18564).

### Role
A role is a virtual identity with a collection of permissions. It is used to grant permissions to role entities for them to access services and resources and perform operations in Tencent Cloud. Those permissions are granted to a role instead of a user or user group.
CAM supports two types of roles:
- Service (preset) role: this is a role predefined by a Tencent Cloud service. Once you authorize a service role, the service can assume the role to access and perform operations on your resources.
- Custom role: this is a role defined by yourself. You can decide which role entity you want to use and what permissions you want to grant to the role.

Roles can be used by:

 * Tencent Cloud root accounts that can assume roles.
 * Tencent Cloud sub-users or collaborators that can assume roles.

Roles can also be used by Tencent Cloud services that support roles. To check whether a Tencent Cloud service supports service roles, please see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

### Service Role
A service role is a special preset CAM role provided directly by a Tencent Cloud service. The permissions associated with a service role are predefined by the corresponding service. Once you grant a service role to a service, it can call other Tencent Cloud services on your behalf within the scope of granted permissions. Service roles make it easier for you to use services, because you do not need to manually add permissions when creating a role. Instead, you only need to decide whether you want to grant a service the permissions associated with a service role.

When you grant a service role to a service, the permissions and role entity corresponding to the service role have already been defined. Unless you redefine the permissions, the service role can only be assumed by its corresponding service. A service role comes with a predefined role name, role entity, and permission policies.
### Custom Role
A custom role is a CAM role defined by yourself. You can define the role name, role entity, and permissions, which allows you to manage access to your resources in a more flexible way.

Objects that are granted a role can get the corresponding permissions only when using the role, avoiding the security risks caused by persistent keys.
### Role Entity
A role entity is an object allowed to have the permissions associated with a role. You can edit role entities by adding or deleting objects to allow them to assume roles to access your Tencent Cloud resources or prohibit them from doing so. Tencent Cloud supports two types of role entities: Tencent Cloud accounts and role-enabled Tencent Cloud services. To find out whether a Tencent Cloud service supports service roles, please see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).


### Permission Policy
A permission policy is a JSON file on permissions where you can define which operations a role can perform and what resources it can access. This file should conform to the CAM policy syntax rule.

### Trust Policy
A trust policy is a JSON file on permissions where you can define which objects can assume a role and what conditions must be met before they can assume a role. This file should conform to the CAM policy syntax rule.


