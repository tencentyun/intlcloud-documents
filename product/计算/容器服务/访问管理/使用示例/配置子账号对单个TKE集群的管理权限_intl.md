## Operation Scenario

You can grant a user the permissions to view and use specific resources in the TKE console by using a CAM policy. The examples in this document guide you through the process of configuring a single cluster in the console.

## Steps

### Configuring Full Read/write Permission for a Single Cluster

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. In the left navigation pane, click [Policies](https://console.cloud.tencent.com/cam/policy) to go to the policy management page.
3. Click **Create a custom policy** and select the "[Create by policy syntax](https://console.cloud.tencent.com/cam/policy/createV2)" method.
4. Select the "Blank template" type and click **Next**.
5. Enter a custom policy name and replace "Edit policy content" with the following.
```json
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "ccs:*"
            ],
            "resource": [
                "qcs::ccs:sh::cluster/cls-XXXXXXX", // Replace with the cluster in the specified region for which you want to grant permissions
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
6. In "Edit policy content", change `qcs::ccs:sh::cluster/cls-XXXXXXX` to the cluster in the specified region for which you want to grant permissions. See the figure below:
For example, if you need to grant full read/write permission for the cls-69z7ek9l cluster in Guangzhou, change `qcs::ccs:sh::cluster/cls-XXXXXXX` to `"qcs::ccs:gz::cluster/cls-69z7ek9l"`.
![Edit policy content](https://main.qcloudimg.com/raw/a9d1825ebe2986e4c8a019b1fcb74713.png)
>! Replace with the ID of the cluster ID in the specified region for which you want to grant permissions. If you want to allow sub-accounts to scale the cluster, you also need to configure the user payment permission for the sub-accounts.
7. Click **Create a policy** to complete the configuration of full read/write permission for a single cluster.

### Configuring Read-only Permission for a Single Cluster

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. In the left navigation pane, click [Policies](https://console.cloud.tencent.com/cam/policy) to go to the policy management page.
3. Click **Create a custom policy** and select the "[Create by policy syntax](https://console.cloud.tencent.com/cam/policy/createV2)" method.
4. Select the "Blank template" type and click **Next**.
5. Enter a custom policy name and replace "Edit policy content" with the following.
```json
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "ccs:Describe*",
                "ccs:Check*"
            ],
            "resource": "qcs::ccs:gz::cluster/cls-1xxxxxx", // Replace with the cluster in the specified region for which you want to grant permissions
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
6. In "Edit policy content", change `qcs::ccs:gz::cluster/cls-1xxxxxx` to the cluster in the specified region for which you want to grant permissions. See the figure below:
For example, if you need to grant ready-only permission for the cls-19a7dz9c cluster in Beijing, change `qcs::ccs:gz::cluster/cls-1xxxxxx` to `qcs::ccs:bj::cluster/cls-19a7dz9c`.
![Edit policy content 2](https://main.qcloudimg.com/raw/0689ed1ad85aa4d8fc8960e258b9bd1b.png)
>! Replace with the ID of the cluster ID in the specified region for which you want to grant permissions.
7. Click **Create a policy** to complete the configuration of read-only permission for a single cluster.
