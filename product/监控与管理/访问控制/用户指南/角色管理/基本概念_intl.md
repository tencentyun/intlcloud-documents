Before you get started with roles, please get familiar with the basic terms, including role, service role, custom role, role entity and permission policy. To learn more about terms, see [Glossary](https://cloud.tencent.com/document/product/598/18564).

### Role
A role refers to a virtual identity with a group of permissions, and it is used to grant permissions to access services and resources and to perform operations in Tencent Cloud to the role entities. These permissions are granted to a role, instead of a user or user group.
CAM supports two types of roles:
- Service (preset) role: A predefined role that a service assumes to access your Tecent Cloud resources on your behalf. You must authorize a service role for the service to assume. 
- CCustom roles: A role that you can customize the servie to assume.  This allows you to create role entities and grant permissions to the role based on your need.

Roles can be used by:

 * Tencent Cloud accounts that can serve as roles
 * Tencent Cloud sub-users or collaborators that can serve as roles

Besides, roles can be used by Tencent Cloud product services supporting roles. To find out whether a Tencent Cloud product service supports service roles, see [Cloud Services Supporting CAM](https://cloud.tencent.com/document/product/598/10588).

### Service role
A service role is a unique type of predefined CAM role provided directly by each of Tencent Cloud product service. The permission associated with a service role are predefined according to the product or service. Once you give permission to a service role, it can call other Tencent Cloud product services that are within the scope that service role's permissions on behalf of you. A service role makes it easy for you to use services, because you just need to choose whether or not to grant a service role's permissions to a service, instead of adding permissions manually.

The permissions and identity of a service role are predefined while a service assuming it. Unless you redefine the scope, service roles can only be assumed by their corresponding services. A service role comes with a predefined name, entity and permission policies.

### Custom role
A custom role is a CAM role that allows users to define based on their needs. You can define the name, entity and permissions of a custom role so that gives you more flexibility managing clound access and allocating cloud resources.

Objects that you grant a role to can only get the permissions while using the role. This helps prevent security problems caused by using persistent keys.
### Role Entity
A role entity is an object allowed to have the permissions of the role. You can edit a role entity, and add or delete objects to allow or prohibit them to assume roles to access your Tencent Cloud resources. Tencent Cloud supports two types of role entities: Tencent Cloud accounts and role-enabled Tencent Cloud services. To find out the role-enabled Tencent Cloud product and service, see [Cloud Services Supporting CAM](https://cloud.tencent.com/document/product/598/10588).

### Permission Policies
Permission policies are JSON-formatted, and they allow you can determine which operations a role can perform and what resources a role can  access. This document is written based on the language rule of CAM policy.

### Trust Polices
Trust policies are JSON-formatted, and they allow you to determine who assume a role and what condition need to be met when creating the role. This document is written based on the language rule of CAM policy.
