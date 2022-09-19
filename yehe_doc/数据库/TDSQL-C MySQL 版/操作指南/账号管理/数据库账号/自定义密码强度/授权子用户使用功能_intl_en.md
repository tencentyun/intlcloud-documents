This document describes how to use the root account to grant a sub-user the permissions of the custom password strength feature.

## Overview
Your root account has all permissions of the custom password strength feature with no additional settings needed. By default, sub-users don't have permissions of this feature. Therefore, you need to create policies to allow the target sub-user to use the feature.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web service provided by Tencent Cloud that helps you securely manage access to the resources under your Tencent Cloud account. CAM allows you to create, manage, or terminate users or user groups and control who is allowed to use your Tencent Cloud resources through identity and policy management.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603).

## Directions
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) with the root account, locate the target sub-user in the user list, and click **Authorize**.
![img](https://qcloudimg.tencent-cloud.cn/raw/db1ece1fffaf7cfbaa67dd73fb55f57c.png)
2. Set the following permissions based on the account's needs. Note that no matter whether the sub-user needs to use the custom password strength feature, we recommend you always add `cynosdb:DescribeClusterPasswordComplexity` to the sub-user, so that they can view the detailed password strength settings configured by the root account in the console and set compliant passwords accordingly.

## CAM permission description

| Permission | Purpose |
|---------|---------|
| cynosdb:DescribeClusterPasswordComplexity | Displays the detailed settings and enablement status of the custom password strength feature |
| cynosdb:CloseClusterPasswordComplexity | (Batch) disables the custom password strength feature |
| cynosdb:CopyClusterPasswordComplexity | Syncs the custom password strength parameters to other clusters under the current account |
| cynosdb:ModifyClusterPasswordComplexity | Modifies the detailed settings of the custom password strength feature |
| cynosdb:OpenClusterPasswordComplexity | Enables the custom password strength feature |

