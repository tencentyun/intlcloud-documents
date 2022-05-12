If you have multiple users managing different Tencent Cloud services such as Lighthouse, VPC, and TencentDB, and they all share your Tencent Cloud account access key, you may face the following problems:
- The risk of your key being compromised is high since multiple users are sharing it.
- Your users might introduce security risks from maloperations due to the lack of user access control.

You can use [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) to allow different users to manage different services through sub-accounts so as to avoid the above problems. By default, a sub-account doesn't have the permission to use Lighthouse or its relevant resources. Therefore, you need to create a policy to grant the required permission to the sub-account. You can skip this section if you don't need to manage permissions to Lighthouse resources for sub-accounts, which will not affect your understanding and use of the other sections of the document.


## Features
CAM is a web-based Tencent Cloud service that helps you securely manage and control the access permissions of resources under your Tencent Cloud account. With CAM, you can create, manage, and terminate users or user groups and use identities and policies to control user access to Tencent Cloud resources. When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks.

Lighthouse has been connected to CAM, so you can use CAM to control the permissions of the Lighthouse resources.


## Concepts
#### CAM users

A CAM user is an entity you create in Tencent Cloud. Each CAM user is associated with one Tencent Cloud account. The identity of your registered Tencent Cloud account is the **root account**, and you can create **sub-accounts** with different permissions for collaboration through [user management](https://console.cloud.tencent.com/cam). The types of sub-accounts include [sub-user](https://intl.cloud.tencent.com/document/product/598/13674), [collaborator](https://intl.cloud.tencent.com/document/product/598/32639), and [message recipient](https://intl.cloud.tencent.com/document/product/598/13667).

#### Policies

A [policy](https://intl.cloud.tencent.com/document/product/598/10601) is the syntax rule used to define and describe one or more permissions. CAM supports two types of policies: preset policy and custom policy.

 - Preset policies: Policies created and managed by Tencent Cloud. These are some common permission sets that are frequently used by users, such as full read and write permissions for resources. Preset policies have a wide range of operation objects, coarse operation granularity, and are preset by the system. They cannot be edited by users.
 - Custom policies: Policies created by users. These permit fine-grained division of permissions. For example, a usage policy is associated with a sub-account that gives the sub-account management permissions for the scaling groups of Auto Scaling, but no management permissions for TencentDB instances.

#### Resources

[Resource](https://intl.cloud.tencent.com/document/product/598/10606) is an element of policies that describes one or multiple operation objects. For example, the launch configuration and scaling groups of Auto Scaling.



