If you use Tencent Kubernetes Engine (TKE), and have multiple users managing and sharing your Tencent Cloud account password, you may encounter the following issues:

- Your password is shared by multiple users, leading to high risk of compromise.
- You cannot restrict the access permissions of others, exposing the system to faulty operations that lead to security risks.

To resolve the problems described above, you can use different sub-accounts to implement the management of different projects by different people. By default, sub-accounts do not have permission to use TKE. To do so, you need to create a policy that permits sub-accounts to have all the permissions they need.

## Overview

Cloud Access Management (CAM) by Tencent Cloud is a permission and user management system designed for secure and precise products management and access. By using CAM, you can create, manage, and terminate users (groups), and control what actions users and roles can perform and what resources they can access by identity and policy management.

When you use CAM, you can associate a policy with a user or a user group. Policies can allow or forbid users to use the specified resources to complete the specified tasks. For more basic information about CAM policies, see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603). For more information about using CAM policies, see [Policies](https://intl.cloud.tencent.com/document/product/598/10601).
If you do not need to manage the access permission to CAM-related resources for sub-accounts, you can skip this chapter. This will not affect your understanding and usage of other parts in this document.

## Getting Started

A CAM policy allows or prohibit the use of one or more TKE operations, or must forbid the use of one or more TKE operations. At the same time, it is also necessary to specify the resources that can be operated (you can specify all resources, or some operations can specify some resources). Policies also can contain conditions for operating resources.

Some TKE APIs do not support resource-level permissions, meaning that, when calling these APIs, you cannot specify specific resources for the operations. Instead, you must specify all resources for the operations.

