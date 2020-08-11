
## Overview

You can grant a user the permission to view and use specific resources in the Game Server Engine (GSE) Console by using CAM policies. The examples below show how to do so.

## Directions

### Full access policy for GSE

To grant a user full permission to create and manage all GSE resources, associate the `QcloudGSEFullAccess` policy with the user.
The detailed steps are as follows:
1. Go to the [Policies](https://console.cloud.tencent.com/cam/policy) page in the console, and click **Service Type**.
2. Search for this policy by selecting **Game Server Engine** from the drop-down list, or by directly using the search box in the top right corner.

![](https://main.qcloudimg.com/raw/fe654b37e2fd44deac52743c77ecc477.png)

The policy syntax is as follows:

```
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "gse:*"
      ],
      "resource": "*",
      "effect": "allow"
    }
  ]
}
```

The above policy allows the user full access permission to GSE, including activating service, viewing statistics, and accessing asset packages, aliases, fleets, game server session queues, and any other resources.

### Read-only policy for GSE

To grant a user permission to query any GSE resources, but not create, delete, or modify them, associate the `QcloudCDBInnerReadOnlyAccess` policy with the user.
The detailed steps are as follows:
1. Go to the [Policies](https://console.cloud.tencent.com/cam/policy) page in the console, and click **Service Type**.
2. Search for this policy by selecting **Game Server Engine** from the drop-down list, or by directly using the search box in the top right corner.

![](https://main.qcloudimg.com/raw/2368902dfcb590dd60e51b1720c0c07f.png)

The policy syntax is as follows:

```
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "gse:Get*",
        "gse:Describe*",
        "gse:List*",
        "gse:Resolve*",
        "gse:Search*",
        "gse:Check*"
      ],
      "resource": "*",
      "effect": "allow"
    }
  ]
}
```

### Policy for querying GSE service status

To grant a user the permission to query the status of GSE service, you can include the following operation in your policy, and then associate the policy with the user.

| Name | Description |
| --------------- | ---------------- |
| CheckOpenStatus | Checks whether the service is activated or not |

The detailed steps are as follows:
1. Create a custom policy for querying GSE service status as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601). The example policy syntax is as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:CheckOpenStatus"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

2. Find the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.

>!To initiate a GSE API request always requires the permission to the `CheckOpenStatus` API. Therefore, you must have `CheckOpenStatus` included in your custom policy. To do so, you can manually add it to each of your custom policies, or create a separate custom policy for this API like the example above, and associate it with any specific user.

### Policy for activating GSE service

To grant a user the permission to activate GSE service, you can include the following operation in your policy, and then associate the policy with the user.

| Name | Description |
| ------------- | ---------------- |
| SetOpenStatus | Activates GSE service |

The detailed steps are as follows:

1. Create a custom policy for activating GSE service as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601). The example policy syntax is as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:SetOpenStatus"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

2. Find the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.

### Policy for viewing GSE statistics

To grant a user the permission to view GSE statistics, you can include the following operations in your policy, and then associate the policy with the user.

| Name | Description |
| ----------------------------- | -------------------- |
| DescribeFleetStatisticDetails | Queries details on fleet statistics     |
| DescribeFleetStatisticFlows | Queries fleet usage statistics    |
| DescribeFleetStatisticSummary | Queries a summary of fleet statistics |
| ListFleets                    | Retrieves a fleet list        |

The detailed steps are as follows:

1. Create a custom policy for viewing GSE statistics as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601). The example policy syntax is as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:ListFleets",
                "gse:DescribeFleetStatisticDetails",
                "gse:DescribeFleetStatisticFlows",
                "gse:DescribeFleetStatisticSummary"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

2. Find the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.

### Policy for GSE matching

To grant a user the permission for matching on GSE, you can include the following operation in your policy, and then associate it with the user.

| Name | Description |
| ------------------- | -------------------------- |
| StartMatchPlacement | Starts to match and place a game server session |


The detailed steps are as follows:

1. Create a custom policy for matching on GSE as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601). The example policy syntax is as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": "gse:StartMatchPlacement",
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

2. Find the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.

### Policy for listing GSE resources

To grant a user the permission to retrieve GSE resources lists, you can include the following operations in your policy, and then associate the policy with the user.

| Name | Description |
| ------------------------------- | ------------------------------ |
| DescribeAssets                  | Retrieves a list of asset packages                 |
| DescribeGameServerSessionQueues | Queries game server session queues         |
| DescribeFleetAttributes         | Retrieves fleet attributes (including status) |
| DescribeFleetCapacity           | Retrieves the current fleet capacity settings       |
| DescribeFleetUtilization        | Retrieves fleet utilization statistics     |
| DescribeInstanceTypes           | Retrieves a list of server instance types        |
| DescribeUserQuotas              | Retrieves quotas for modules         |
| ListAliases                     | Retrieves an alias list                   |
| ListFleets                      | Retrieves a fleet list                  |

The detailed steps are as follows:

1. Create a custom policy for listing GSE resources as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601). The example policy syntax is as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:DescribeFleetUtilization",
                "gse:DescribeInstanceTypes",
                "gse:DescribeFleetAttributes",
                "gse:DescribeFleetCapacity",
                "gse:DescribeUserQuotas",
                "gse:DescribeAssets",
                "gse:DescribeGameServerSessionQueues"
                "gse:ListAliases",
                "gse:ListFleets"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

2. Find the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.

### Full access policy for GSE excluding setting service status and viewing statistics

To grant a user full access permission to GSE, excluding setting service status and viewing statistics, you can create a custom policy to associate with the user using a policy syntax as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "gse:SetOpenStatus",
                "gse:DescribeFleetStatisticDetails",
                "gse:DescribeFleetStatisticFlows",
                "gse:DescribeFleetStatisticSummary"
            ],
            "resource": "*",
            "effect": "deny"
        }
    ]
}
```

### Policy for accessing GSE asset packages

To grant a user the permission to access all asset packages on GSE in a specific account, e.g. 110702656, you can include the following operations in your policy, and then associate it with the user.

| Name | Description |
| ------------- | ---------------- |
| DeleteAsset   | Deletes an asset package       |
| DescribeAsset                  | Retrieves asset package attributes              |
| UpdateAsset   | Updates asset package attributes |


The detailed steps are as follows:

1. Create a custom policy for accessing all asset packages on GSE in account 110702656 as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601). The example policy syntax is as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:DeleteAsset",
                "gse:DescribeAsset",
                "gse:UpdateAsset"
            ],
            "resource": "qcs::gse::uin/110702656:asset/*",
            "effect": "allow"
        }
    ]
}
```

2. Find the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.

To allow the user access to a specific asset package, e.g. AssetId=asset-eiu39dki-3o0dk2dk, in account 110702656, configure the value of `resource` to:

```
qcs::gse::uin/110702656:asset/asset-eiu39dki-3o0dk2dk

```

### Policy for accessing GSE aliases

To grant a user the permission to access all aliases on GSE in a specific account, e.g. 110702656, you can include the following operations in your policy, and then associate it with the user.

| Name | Description |
| ------------- | ----------------------- |
| DeleteAlias   | Deletes an alias             |
| DescribeAlias | Retrieves alias attributes          |
| ResolveAlias  | Retrieves the fleet ID associated with an alias |
| UpdateAlias   | Updates alias attributes          |


The detailed steps are as follows:

1. Create a custom policy for accessing all aliases on GSE in account 110702656 as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601). The example policy syntax is as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:DeleteAlias",
                "gse:DescribeAlias",
                "gse:ResolveAlias",
                "gse:UpdateAlias"
            ],
            "resource": "qcs::gse::uin/110702656:alias/*",
            "effect": "allow"
        }
    ]
}

```

2. Find the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.

To allow the user access to a specific alias, e.g. AliasId=alias-wk30dke9-ovr93dk3, in account 110702656, configure the value of `resource` to:

```
qcs::gse::uin/110702656:asset/alias-wk30dke9-ovr93dk3

```

### Policy for accessing GSE fleets

To grant a user the permission to access all fleets on GSE in a specific account, e.g. 110702656, you can include the following operations in your policy, and then associate it with the user.

| Name | Description |
| ---------------------------- | -------------------------------- |
| AttachCcnInstances           | Associates CCN instances                   |
| CreateFleetDemo              | Creates a fleet demo                     |
| DeleteFleet                  | Deletes an empty fleet                       |
| DeleteScalingPolicy          | Deletes a scaling policy              |
| DescribeFleetEvents          | Retrieves entries from fleet event logs       |
| DescribeFleetPortSettings    |Retrieves the inbound connection permissions for a fleet          |
| DescribeInstances            | Retrieves fleet instance information               |
| DescribeInstancesExtend      | Retrieves the scaling information of fleet instances         |
| DescribeRuntimeConfiguration | Retrieves a fleet runtime configuration             |
| DescribeScalingPolicies      | Retrieves all fleet scaling policies         |
|  DetachCcnInstances           | Unassociates CCN instances                   |
| GetInstanceAccess            | Requests remote access to the specified fleet instance |
| PutScalingPolicy             | Creates or updates a scaling policy             |
| SetServerWeight              | Sets server weight                   |
| StartFleetActions            | Starts auto-scaling activities on a fleet       |
| StopFleetActions            | Suspends auto-scaling activities on a fleet       |
| UpdateDemoResource           | Modifies the attributes of a service deployment demo           |
| UpdateFleetAttributes        | Updates general attributes of a fleet               |
| UpdateFleetCapacity          | Updates fleet capacity                   |
| UpdateFleetName | Updates a server fleet name |
| UpdateFleetPortSettings      | Updates fleet port settings               |
| UpdateFleetVpc               | Updates the VPC for a game server fleet            |
| UpdateRuntimeConfiguration   | Updates the regular fleet runtime configuration         |


The detailed steps are as follows:

1. Create a custom policy for accessing all fleets on GSE in account 110702656 as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601). The example policy syntax is as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
				"gse:AttachCcnInstances",
				"gse:CreateFleetDemo",
				"gse:DeleteFleet",
				"gse:DeleteScalingPolicy",
				"gse:DescribeFleetEvents",
				"gse:DescribeFleetPortSettings",
				"gse:DescribeInstances",
				"gse:DescribeInstancesExtend",
				"gse:DescribeRuntimeConfiguration",
				"gse:DescribeScalingPolicies",
				"gse:DetachCcnInstances",
				"gse:GetInstanceAccess",
				"gse:PutScalingPolicy",
				"gse:SetServerWeight",
				"gse:StartFleetActions",
				"gse:UpdateDemoResource",
				"gse:UpdateFleetAttributes",
				"gse:UpdateFleetCapacity",
				"gse:UpdateFleetName",
				"gse:UpdateFleetPortSettings",
				"gse:UpdateFleetVpc",
				"gse:UpdateRuntimeConfiguration"
            ],
            "resource": "qcs::gse::uin/110702656:fleet/*",
            "effect": "allow"
        }
    ]
}
```

2. Find the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.

To allow the user access to a specific fleet, e.g. FleetId=fleet-28a9refi-ur5pe34j, in account 110702656, configure the value of `resource` to:

```
qcs::gse::uin/110702656:fleet/fleet-28a9refi-ur5pe34j
```

### Policy for accessing GSE game server session queues

To grant a user the permission to access all game server session queues on GSE in a specific account, e.g. 110702656, you can include the following operations in your policy, and then associate it with the user.

| Name                           | Description                                                 |
| ------------------------------- | ---------------------------------------------------- |
| DeleteGameServerSessionQueue    | Deletes a game server session queue                             |
| StartGameServerSessionPlacement | Starts sending a game server session placement request to the game server session queue |
| UpdateGameServerSessionQueue    | Updates the attributes of a game server session queue                         |


The detailed steps are as follows:

1. Create a custom policy for accessing all game server session queues on GSE in account 110702656 as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601). The example policy syntax is as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:DeleteGameServerSessionQueue",
                "gse:StartGameServerSessionPlacement",
                "gse:UpdateGameServerSessionQueue"
            ],
            "resource": "qcs::gse::uin/110702656:gameServerSessionQueue/*",
            "effect": "allow"
        }
    ]
}
```

2. Find the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.

To allow the user access to a specific game server session queue in account 110702656, e.g. “GameServerSessionQueueName=queue-ciu3c0de-c09dk3do” in the `StartGameServerSessionPlacement` input parameters, or “Name=queue-ciu3c0de-c09dk3do” in the `DeleteGameServerSessionQueue/UpdateGameServerSessionQueue` input parameters, configure the value of `resource` to:

```
qcs::gse::uin/110702656:gameServerSessionQueue/queue-ciu3c0de-c09dk3do
```

### Policy for accessing Demo

To grant a user the permission to access the Demo for GSE, you can include the following operations in your policy, and then associate it with the user.

| Name | Description |
| -------------------------- | ------------------------------ |
| CreateAssetAuto            | Creates an asset package automatically                |
| CreateFleetDemo              | Creates a fleet demo                     |
| CreateGameServerSession    | Creates a game server session             |
| DescribeFleetAttributes         | Retrieves fleet attributes (including status) |
| DescribeGameServerSessions | Queries a list of game server sessions               |
| DescribeDemoResource       | Retrieves the attributes of a service deployment demo         |
| JoinGameServerSession     |Joins a game server session             |
| UpdateDemoResource           | Modifies the attributes of a service deployment demo           |

The detailed steps are as follows:
1. Create a custom policy for accessing the Demo for GSE as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601). The example policy syntax is as follows:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:CreateAssetAuto",
                "gse:UpdateDemoResource",
                "gse:CreateFleetDemo",
                "gse:DescribeDemoResource",
                "gse:DescribeFleetAttributes",
                "gse:DescribeGameServerSessions",
                "gse:CreateGameServerSession",
                "gse:JoinGameServerSession"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
2. Find the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.
