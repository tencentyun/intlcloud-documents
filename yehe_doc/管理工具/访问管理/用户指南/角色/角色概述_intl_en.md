

## Role Overview
A role in CAM is a virtual user, which is different from physical users such as sub-accounts, collaborators, or message recipients. Roles can also be granted policies.

A role can be assumed by any Tencent Cloud account and is not exclusively associated with one single account. Although a root account uses persistent credentials such as a password or access keys when creating a role, the role does not have persistent credentials associated with it. When you assume a role, temporary credentials are created for you to access related resources. Specifically, you can use temporary keys to call open TencentCloud APIs in order to access your Tencent Cloud resources.


## Use Cases
Those who can apply for a role are called role entities. Currently, Tencent Cloud role entities are divided into three categories: Tencent Cloud accounts, products and services that support the role feature, and identity providers. The corresponding use cases are as follows:

- You want to grant users under your account temporary access to resources or grant users under another Tencent Cloud root account the access to resources under your account.

- You may need to allow Tencent Cloud products and services to have access to your resources, but you don't want to embed persistent keys in them, because there may be security issues where it is difficult to rotate keys or keys are leaked after interception.

- If you already have an account system for your organization, you can use the Identity Provider (IdP) feature to allow your organization members to access Tencent Cloud resources. This eliminates the need to create a CAM sub-user for each member under your Tencent Cloud account.



