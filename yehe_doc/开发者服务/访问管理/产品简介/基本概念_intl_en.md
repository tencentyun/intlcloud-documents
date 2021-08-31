Before using CAM, you need to understand some related concepts first, such as root account, sub-account, sub-user, collaborator, and user group. This helps you better understand and use CAM.

### Root Account

When you sign up for a Tencent Cloud account, the system creates a root account identity for you to log in to Tencent Cloud services. Tencent Cloud records your usage and bills you based on the root account. The root account has full access to the resources under it by default and can create sub-accounts and set permissions for them.


### Sub-account

A sub-account is an entity you create in Tencent Cloud with a specific ID and credentials. It is divided into sub-user, collaborator, and message recipient. The difference between a sub-user and a collaborator is that a sub-user is fully owned by the root account, while a collaborator is a previously registered Tencent Cloud root account. In other words, a collaborator can have two identities: root account of its own account or collaborator of another root account. For more information, please see [User Types](https://intl.cloud.tencent.com/document/product/598/32633).

### Admin User

An admin user is a sub-account with the permissions of the `AdministratorAccess` policy. It is created by the root account or another admin user and can manage all users and their permissions, financial information, and Tencent Cloud service assets under your Tencent Cloud account.

### User Group

A user group is a collection of multiple users (sub-accounts) with the same functions. You can create different user groups based on your business needs and associate them with appropriate policies to grant them different permissions.

### Role

A role in CAM can be seen as a virtual user, which is different from physical users such as sub-accounts, collaborators, or message recipients. Roles can also be granted policies.
A role can be assumed by any Tencent Cloud account and is not exclusively associated with one single account. Although a root account uses persistent credentials such as a password or access keys when creating a role, the role does not have persistent credentials associated with it. When you assume a role, temporary credentials are created for you to access related resources. Specifically, you can use roles through the console and APIs.


### Permission

A permission describes whether to allow or refuse execution of certain operations to access certain resources under certain conditions. By default, a root account is the resource owner and has full access to all resources under it, while a sub-account does not have access to any resources. A resource creator does not automatically possess the access to the created resource and should be authorized by the resource owner instead.

### Policy

A policy is a syntax rule that defines and describes one or more permissions. Tencent Cloud policy types include preset policy and custom policy.

- **Preset policy**
A preset policy is a set of some common permissions created and managed by Tencent Cloud that are frequently used by users, such as admin permission (AdministratorAccess) and full access to CVM (QcloudCVMFullAccess). Preset policies cover a wide range of operation objects at a coarse operation granularity. They are preset by the system and cannot be edited by users.


- **Custom policy**
A custom policy is user-defined permission sets that describe resource management in a more refined way. It allows fine-grained permission division and can flexibly meet your differentiated permission management needs. For example, you can associate a policy with a database admin so that the admin has the permissions to manage TencentDB instances but not CVM instances.
