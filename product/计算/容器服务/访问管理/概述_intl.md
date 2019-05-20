If you use the TKE service in Tencent Cloud, and the service is managed by different users who share your Tencent Cloud account and password, the following problems may exist:
- Your password is shared by multiple users, leading to high risk of compromise.
- You cannot restrict the access permissions of others; therefore, the system is prone to faulty operations that lead to security risks.

In this case, you can use sub-accounts to enable different users to manage different services to avoid such problems. By default, sub-accounts do not have permissions to use TKE. Therefore, you need to create policies to allow sub-accounts to have the permissions they need.

## Overview
CAM is a web-based permission and access management service offered by Tencent Cloud, helping you securely manage the access permissions to resources under your Tencent Cloud account. With CAM, you can create, manage and destroy users (groups) and use identity and policy management to control what users can use what Tencent Cloud resources.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more basic information about CAM policies, see [Policy Syntax](/doc/product/598/10603). For more information about how to use CAM policies, see [Policy](/doc/product/598/10601).
If you don't need to manage access to related resources for sub-accounts through CAM, you can skip this section. Doing so does not affect your understanding and use of the rest of the documentation.

## Getting Started
A CAM policy must authorize or deny the use of one or more TKE operations. At the same time, it must specify the resources that can be used for the operations (which can be all resources or partial resources for certain operations). A policy can also include the conditions set for the operation resources.

Certain TKE API operation support resource-level permissions, which means that for this type of API operations, you cannot specify a given resource for use when they are performed; instead, you must specify all resources for use.
