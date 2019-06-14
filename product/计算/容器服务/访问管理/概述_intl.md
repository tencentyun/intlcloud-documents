If you are a Tencent Kubernetes Engines (TKE) user, and have multiple users manage and share your Tencent Cloud account password, you may encounter the following issues:
- Your password is shared by multiple users with high vulnerability.
- You cannot restrict the access permissions of others; therefore, the system is prone to faulty operations that lead to security risks.

In this case, you can use sub-accounts to enable different users to manage different services to avoid such problems. By default, sub-accounts do not have permissions to use TKE. Therefore, you need to create policies to allow sub-accounts to have the permissions they need.

## Overview
Cloud Access Management (CAM) is a web-based Tencent Cloud service that helps you securely manage and control access to your Tencent Cloud resources. CAM provides identity management and policy management for you to create, manage or terminate users (groups), and to control who is allowed to access and use your Tencent Cloud resources.

CAM allows you to control users or user groups accessing specified resources by associating them with policies. For more basic information about CAM policies, see [Policy Syntax](/doc/product/598/10603). For more information about how to use CAM policies, see [Policy](/doc/product/598/10601).
If you do not need to manage sub-account access permissions via CAM, you can skip this section. Doing so does not affect your understanding and use of the rest of the documentation.

## Getting Started
A CAM policy must be practiced for authorizing or denying one or more TKE operations. At the same time, it must specify the resources available (all cloud resources or part of the resources) for the operation. A policy also defines the conditions of resource operation.

Some TKE APIs requires you to perform operations utilizing all of your cloud resources. That is, when calling these APIs, you cannot specify some resources for the operations; instead, you must specify all resources for the operations.


