## Overview

You can grant a user the permissions to view and use specific resources in the TKE console by using a CAM policy. This document describes how to configure the CAM policy of a single cluster in the console.

## Directions

### Configuring full read/write permission for a single cluster

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. In the left sidebar, click [Policies](https://console.cloud.tencent.com/cam/policy) to go to the policy management page.
3. Click **Create Custom Policy** and select the "[Create by Policy Syntax](https://console.cloud.tencent.com/cam/policy/createV2)" method.
4. Select the "Blank template" type and click **Next**.
5. Enter a custom policy name and replace "Edit policy content" with the following content.
```json
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "ccs:*"
            ],
            "resource": [
                "qcs::ccs:sh::cluster/cls-XXXXXXX",
                "qcs::cvm:sh::instance/*"
            ],
            "effect": "allow"
        },
        {
            "action": [
                "cvm:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "clb:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "monitor:*",
                "cam:ListUsersForGroup",
                "cam:ListGroups",
                "cam:GetGroup",
                "cam:GetRole"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
6. In "Edit policy content", modify `qcs::ccs:sh::cluster/cls-XXXXXXX` to the cluster in the specified region for which you want to grant permissions, as shown below:
For example, if you need to grant full read/write permission for the cls-69z7ek9l cluster in Guangzhou, modify `qcs::ccs:sh::cluster/cls-XXXXXXX` to `"qcs::ccs:gz::cluster/cls-69z7ek9l"`.
![Edit Policy Content](https://main.qcloudimg.com/raw/79850c72fb3e5b33994a21d0f2601578.png)
<dx-alert infotype="notice" title="">
Replace with the ID of the cluster in the specified region for which you want to grant permissions. If you want to allow sub-accounts to scale the cluster, you also need to configure the user payment permission for the sub-accounts.
</dx-alert>
7. Click **Create a policy** to complete the configuration of full read/write permission for a single cluster.

### Configuring read-only permission for a single cluster

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. In the left sidebar, click [Policies](https://console.cloud.tencent.com/cam/policy) to go to the policy management page.
3. Click **Create Custom Policy** and select the "[Create by Policy Syntax](https://console.cloud.tencent.com/cam/policy/createV2)" method.
4. Select the "Blank template" type and click **Next**.
5. Enter a custom policy name and replace "Edit policy content" with the following content.
```json
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "ccs:Describe*",
                "ccs:Check*"
            ],
            "resource": "qcs::ccs:gz::cluster/cls-1xxxxxx",
            "effect": "allow"
        },
        {
            "action": [
                "cvm:Describe*",
                "cvm:Inquiry*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:Describe*",
                "vpc:Inquiry*",
                "vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "clb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": [
                "monitor:*",
                "cam:ListUsersForGroup",
                "cam:ListGroups",
                "cam:GetGroup",
                "cam:GetRole"
            ],
            "resource": "*"
        }
    ]
}
```
6. In "Edit policy content", modify `qcs::ccs:gz::cluster/cls-1xxxxxx` to the cluster in the specified region for which you want to grant permissions, as shown below:
For example, if you need to grant ready-only permission for the cls-19a7dz9c cluster in Beijing, modify `qcs::ccs:gz::cluster/cls-1xxxxxx` to `qcs::ccs:bj::cluster/cls-19a7dz9c`.
![Edit Policy Content 2](https://main.qcloudimg.com/raw/048d53fc264edaf3e36446bcabfd05f7.png)
7. Click **Create a policy** to complete the configuration of read-only permission for a single cluster.




