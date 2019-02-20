Before you get started with any role, get familiar with some basic terms, including role, service role, custom role, role entity and permission policy. To learn about more terms, see [Glossary](https://cloud.tencent.com/document/product/598/18564).

### Role
This refers to a virtual identity with a group of permissions. It is used to grant permissions to access services and resources and to perform operations in Tencent Cloud to the role entities. These permissions are granted to a role, instead of a user or user group.
CAM supports two types of roles:
- Service (preset) roles: Roles predefined by Tencent Cloud services. After a service role is authorized by a user, the service can access user resources by assuming that role.
- Custom roles: Roles customized by users. Users can freely define role entities and permissions.  

Roles can be used by:

 * Tencent Cloud accounts that can serve as roles
 * Tencent Cloud sub-users or collaborators that can serve as roles

Besides, roles can be used by Tencent Cloud product services supporting roles. To find out whether a Tencent Cloud product service supports service roles, see [Cloud Services Supporting CAM](https://cloud.tencent.com/document/product/598/10588).

### Service role
A service role is a unique type of predefined CAM role provided directly by each Tencent Cloud product service. The associated permissions of a service role are predefined by the relevant product service. Once a product service is granted a service role by you, it can on your behalf call any of the other Tencent Cloud product services that are within the scope the service role's permissions. A service role makes it easy for you to use services, because you just need to choose whether to grant a service role's permissions to a service, instead of adding permissions manually.

When a service role is to be granted to a service product, its relevant permissions and role identity have been predefined. Roles can only be introduced by this service, unless otherwise defined. A service role comes with predefined name, entity and permission policies.
### Custom role
A custom role is a CAM role that can be freely defined by the users themselves. The user can define the name, entity and permissions of a custom role. A custom role gives you more flexibility to assign the permissions to access and use your cloud resources.

Objects that you grant a role to can only get the permissions while using the role. This helps avoid security problems that may arise from giving persistent keys.
### Role Entity
A role entity is the object allowed to have the permissions of the role. You can edit a role entity, and add or delete objects to allow or forbid them to assume the roles to access your Tencent Cloud resources. Tencent Cloud supports two types of role entities: Tencent Cloud accounts and Tencent Cloud services supporting roles. To find out whether a Tencent Cloud product service supports service roles, see [Cloud Services Supporting CAM](https://cloud.tencent.com/document/product/598/10588).


### Permission Policies
Permission policies are created in a JSON-formatted permission document, where you can define the operations and resources that various roles have access to. This document is based on the language rules of CAM policies.

### Trust Policies
Trust policies are created in a JSON-formatted permission document, where you can define the objects that can assume the roles and the conditions to be met to assume the roles. This document is based on the language rules of CAM policies.



