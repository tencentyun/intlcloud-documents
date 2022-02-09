If you have multiple users managing the RUM service, and they all share your Tencent Cloud account access key, you may face the following problems:
- The risk of your key being compromised is high since multiple users are sharing it.
- Your users might introduce security risks from maloperations due to the lack of user access control.

You can avoid the above problems by allowing different users to manage different services through sub-accounts. By default, sub-accounts have no permissions to use RUM. Therefore, you need to create a policy to grant different permissions to sub-accounts.

## Overview
[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/zh/document/product/598) is a web-based Tencent Cloud service that helps you securely manage and control access permissions of your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).

## Authorization Method


**RUM supports two authorization methods: resource-level authorization and authorization by tag.**

- Resource-Level authorization: you can use policy syntax or the default policy to grant sub-accounts permissions to manage individual resources. For more information, see [Policy Syntax](https://intl.cloud.tencent.com/document/product/1131/44511) and [Granting Policy](https://intl.cloud.tencent.com/document/product/1131/44512).
- Authorization by tag: you can tag resources and grant sub-accounts permissions to manage resources with particular tags. For more information, see [Resource Tag](https://intl.cloud.tencent.com/document/product/1131/44513).

You can skip this section if you don't need to manage permissions of RUM resources for sub-accounts. This won't affect your understanding and use of the other sections of the document.
