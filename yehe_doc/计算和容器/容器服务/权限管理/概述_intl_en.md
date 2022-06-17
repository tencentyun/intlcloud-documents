If you have multiple users managing the TKE service, and they all share your Tencent Cloud account access key, you may face the following problems:
- The risk of your key being compromised is high since multiple users are sharing it.
- Your users might introduce security risks from maloperations due to the lack of user access control.

To solve these problems, create sub-accounts for other users and these users use sub-accounts to log in and manage their services. By default, sub-accounts do not have permission to use TKE. You need to create a policy to grant the required permissions to sub-accounts.

## Overview 
Cloud Access Management (CAM) is a web-based Tencent Cloud service that helps you securely manage and control access permissions of your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, see [Element Reference](/doc/product/598/10603). For more information on how to use CAM policies, see [Policy](/doc/product/598/10601).
You can skip this section if you don't need to manage permissions to CAM resources for sub-accounts. This will not affect your understanding and use of the other sections of the document.

## Getting Started
A CAM policy must authorize or deny the use of one or more TKE operations. At the same time, it must specify the resources that can be used for the operations (which can be all resources or partial resources for certain operations). A policy can also include the conditions set for the manipulated resources.

Some TKE APIs do not support resource-level permissions. This means that you cannot specify certain resources when performing such API operations, and these operations are performed on all the resources.




