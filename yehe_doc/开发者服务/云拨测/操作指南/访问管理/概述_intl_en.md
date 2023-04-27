If you have multiple users managing the CAT service, and they all share your Tencent Cloud account access key, you may face the following problems:
- Your key will be easily compromised because it is shared by several users.
- You cannot restrict the access from other users and your service will be vulnerable to the security risks caused by their misoperations.

You can avoid the above problems by allowing different users to manage different services through sub-accounts. By default, sub-accounts have no permissions to use CAT. Therefore, you need to create a policy to grant different permissions to sub-accounts.
>?You can skip this section if you don't need to manage permissions of CAT resources for sub-accounts. This won't affect your understanding and use of the other sections of the document.

## Overview

[Cloud Access Management (CAM)](https://www.tencentcloud.com/document/product/598) is a Tencent Cloud web service that helps you securely manage and control access to your Tencent Cloud resources. CAM allows you to create, manage or terminate users (user groups), and control who have access to which Tencent Cloud resources based on identity and policy management.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, see [Policy Syntax](https://www.tencentcloud.com/document/product/1169/52015). For more information on how to use CAM policies, see [Concepts](https://intl.cloud.tencent.com/document/product/598/10600).

## Authorization method

**CAT supports two authorization methods: resource-level authorization and authorization by tag.**
- Resource-level authorization: You can use policy syntax or the default policy to grant sub-accounts permissions to manage individual resources. For more information, see [Policy Syntax](https://www.tencentcloud.com/document/product/1169/52015) and [Granting Policy](https://www.tencentcloud.com/document/product/1169/52016).
- Authorization by tag: You can tag resources and grant sub-accounts permissions to manage resources with particular tags. For more information, see [Resource Tag](https://www.tencentcloud.com/document/product/1169/52017).

