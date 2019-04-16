Before you get started with roles, please get familiar with the basic terms, including role, service role, custom role, role entity and permission policy. To learn more about terms, see [Glossary](https://intl.cloud.tencent.com/document/product/598/18564).

### Role
A role refers to a virtual Tencent Clould identity that has specific permissions to determine what a role entity (See [Role Entity]) can do or cannot do in Tencent Cloud. Therefore, you create a role, instead of a user or a user group, to control access to your Tencent Cloud resources on you behalf.
CAM supports two types of roles:
- Service (preset) role: A predefined role that a service assumes to access your Tecent Cloud resources on your behalf. You must authorize a service role for the service to assume. 
- Custom roles: A role that you can customize the servie to assume. This allows you to flexibly create role entities and grant permissions to the role based on your needs.

Roles can be used by:

 * Tencent Cloud accounts that can serve as roles.
 * Tencent Cloud sub-users or collaborators that can serve as roles.

Besides, roles can be used by role-enabled Tencent Cloud products and services. To find out whether a Tencent Cloud product or service supports service roles, see [Cloud Services Supporting CAM](https://intl.cloud.tencent.com/document/product/598/10588).

### Service role
A service role is a unique type of predefined CAM role provided directly by each of Tencent Cloud product service. The permission associated with a service role are predefined according to the product or service. Once you give permission to a service role, it can call other Tencent Cloud product services within the scope on your behalf. Service roles make it easy for you to use services, because you don't need to manually adding permissions. Instead, you can determine whether or not to grant services permissions associated with  the service roles.
When a service assumes a service role, it defines the permissions and identity of that role. Unless you redefine the scope, service roles can only be assumed by their corresponding services. A service role comes with a predefined name, entity and permission policies.

### Custom role
A custom role is a CAM role that allows users to define based on their needs. You can define the name, entity and permissions of a custom role so that allows you to manage cloud access and allocate cloud resources more flexibly.
Objects that you grant a role to can only get the permissions while using the role. This helps prevent security problems caused by using persistent keys.
### Role Entity
A role entity is an object allowed to have the permissions of the role. You can edit a role entity, and add or delete objects to allow or prohibit them to assume roles to access your Tencent Cloud resources. Tencent Cloud supports two types of role entities: Tencent Cloud accounts and role-enabled Tencent Cloud services. To find out if the Tencent Cloud product or service supports service roles, see [Cloud Services Supporting CAM](https://intl.cloud.tencent.com/document/product/598/10588).

### Permission Policies
Permission policies are JSON-formatted, and they allow you can determine which operations a role can perform and what resources a role can  access. This document is written based on the language rule of CAM policy.

### Trust Polices
Trust policies are JSON-formatted, and they allow you to determine who assume a role and what condition need to be met when creating the role. This document is written based on the language rule of CAM policy.
