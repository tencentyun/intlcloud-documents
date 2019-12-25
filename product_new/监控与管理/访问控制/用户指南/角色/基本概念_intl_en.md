Before you get started with roles, familiarize yourself with the basic terms, such as role, service role, custom role, role entity and permission policy. For more terms, see [Glossary] (https://intl.cloud.tencent.com/document/product/598/18564).

### Role
A virtual identity with a collection of permissions. It is used to grant permissions to role entities for them to access services and resources and perform operations in Tencent Cloud. Those permissions are granted to a role, instead of a user or user group.
CAM supports two types of roles:
- Service (preset) role: a role predefined by a Tencent Cloud service. Once you authorize a service role, the service can assume the role to access and perform operations on your resources.
- Custom roles: a role defined by yourself. You can decide which role entity you want to use and what permissions you want to grant the role.

Roles can be used by:

 * Tencent Cloud root accounts that can assume roles
 * Tencent Cloud sub-users or collaborators that can assume roles

Roles can also be used by Tencent Cloud services that support roles. To check whether a Tencent Cloud service supports service roles, see [CAM-enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

### Service role
A special preset CAM role provided directly by a Tencent Cloud service. The permissions associated with a service role are predefined by the corresponding service. Once you grant a service role to a service, it can call other Tencent Cloud services on your behalf within the scope of permissions. Service roles make it easier for you to use services, because you do not need to manually add permissions to create a role. Instead, you only need to decide whether you want to grant a service the permissions associated with a service role.

When you grant a service role to a service, the permissions and role entity corresponding to the service role have already been defined. Unless you redefine the information, a service role can only be assumed by its corresponding service. A service role comes with a predefined role name, role entity, and permission policies.
### Custom role
A CAM role defined by yourself. You can define the role name, role entity and permissions of a custom role which allows you to manage access to your resources in a more flexible way.

Objects that are granted a role can only have the corresponding permissions when using the role, avoiding the security risks caused by persistent keys.
### Role entity
An object allowed to have the permissions associated with a role. You can edit role entities by adding or deleting objects to allow them to assume roles to access your Tencent Cloud resources or prohibit them from doing so. Tencent Cloud supports two types of role entities: Tencent Cloud accounts and role-enabled Tencent Cloud services. To find out if a Tencent Cloud service supports service roles, see [CAM-enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).


### Permission policy
A JSON file on permissions in which you can define   which operations a role can perform and what resources a role can access. This file should conform  to the CAM policy language rule.

### Trust policy
A JSON file on permissions in which you can define which objects can assume a role and what conditions need to be met before an object assumes a role. This file should conform  to the CAM policy language rule.


