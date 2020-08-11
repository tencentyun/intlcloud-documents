
Game Server Engine (GSE) supports resource-level permissions, which means that for certain GSE operations, you can control when users are allowed to perform them, or which specific resources that users are allowed to use. The following will describe the types of resources for which GSE allows permissions.

>?Resource-level permissions specify which resources users can operate on.

You can grant permissions for the types of GSE resources below through Cloud Access Management (CAM):

| Resource Type                         | Resource Description Method in Access Policy                                     |
| :------------------------------------ | :---------------------------------------------------- |
| [GSE Asset Package](#test1)         | `qcs::gse:$region:$account:asset/* `                  |
| [GSE Alias](#test2)           | `qcs::gse:$region:$account:alias/* `                  |
| [GSE Fleet](#test3)           | `qcs::gse:$region:$account:fleet/* `                  |
| [GSE Game Server Session Queue](#test4) | `qcs::gse:$region:$account:gameServerSessionQueue/* ` |

[GSE Asset Package](#test1), [GSE Alias](#test2), and [GSE Fleet](#test3) list all GSE APIs that support resource-level permissions, and the resources supported by each API. To configure a resource path, you need to replace the variables such as `$region` and `$account` with your own parameters. You can also use the wildcard `*` in a resource path. For examples, see [Access Control Examples](https://intl.cloud.tencent.com/document/product/1055/37779).

>!The GSE APIs not listed below do not support resource-level permissions. For these APIs, you can grant their access permissions as well. However, please note that the `resource` element in their policy statement must be specified as `*`.

<span id="test1"></span>
### GSE Asset Package

| API      | Resource Path                                                   | Description             |
| :------------ | :----------------------------------------------------------- | :--------------- |
| DeleteAsset   | `qcs::gse:$region:$account:asset/*`<br>`qcs::gse:$region:$account:asset/$AssetId` | Deletes an asset package      |
| DescribeAsset | `qcs::gse:$region:$account:asset/*`<br>`qcs::gse:$region:$account:asset/$AssetId ` | Retrieves attributes of an asset package |
| UpdateAsset   | `qcs::gse:$region:$account:asset/*`<br>`qcs::gse:$region:$account:asset/$AssetId ` | Updates attributes of an asset package |

<span id="test2"></span>
### GSE Alias

| API      | Resource Path                                                    | Description                    |
| :------------ | :----------------------------------------------------------- | :---------------------- |
| DeleteAlias   | `qcs::gse:$region:$account:alias/*`<br>`qcs::gse:$region:$account:alias/$AliasId` | Deletes an alias                |
| DescribeAlias | `qcs::gse:$region:$account:alias/*`<br>`qcs::gse:$region:$account:alias/$AliasId` | Retrieves attributes of an alias       |
| ResolveAlias  | `qcs::gse:$region:$account:alias/*`<br>`qcs::gse:$region:$account:alias/$AliasId` | Retrieves fleet ID associated with an alias |
| UpdateAlias   | `qcs::gse:$region:$account:alias/*`<br>`qcs::gse:$region:$account:alias/$AliasId ` | Updates attributes of an alias     |

<span id="test3"></span>
### GSE Fleet

| API                     | Resource Path                                                     | Description                             |
| :--------------------------- | :----------------------------------------------------------- | :------------------------------- |
| AttachCcnInstances           | `qcs::gse:$region:$account:asset/*`<br>`qcs::gse:$region:$account:asset/$AssetId` | Associates CCN instances                   |
| CreateFleetDemo              | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Creates a fleet demo                     |
| DeleteFleet                  | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Deletes an empty fleet                    |
| DeleteScalingPolicy          | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Deletes a scaling policy             |
| DescribeFleetEvents          | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Retrieves entries from fleet event logs       |
| DescribeFleetPortSettings    | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Retrieves inbound connection permissions for a fleet          |
| DescribeInstances            | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Retrieves fleet instance information               |
| DescribeInstancesExtend      | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Retrieves expansion information on fleet instances           |
| DescribeRuntimeConfiguration | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Retrieves the runtime configuration of a fleet             |
| DescribeScalingPolicies      | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId ` | Retrieves all scaling policies of a fleet         |
| DetachCcnInstances           | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Unassociates CCN instances                |
| GetInstanceAccess            | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Requests remote access permission for instances on a specific fleet |
| PutScalingPolicy             | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Creates or updates a scaling policy             |
| SetServerWeight              | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Sets server weight                   |
| StartFleetActions            | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Starts auto-scaling activities on a fleet       |
| StopFleetActions             | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Suspends auto-scaling activities on a fleet        |
| UpdateDemoResource           | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Modifies the attributes of a service deployment demo           |
| UpdateFleetAttributes        | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Updates general attributes of a fleet                |
| UpdateFleetCapacity          | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Updates fleet capacity                    |
| UpdateFleetName              | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` |Updates a server fleet name |
| UpdateFleetPortSettings      | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Updates fleet port settings             |
| UpdateFleetVpc               | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Updates the VPC for a game server fleet           |
| UpdateRuntimeConfiguration   | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | Updates the regular fleet runtime configuration         |

<span id="test4"></span>
### GSE Game Server Session Queue

| API                        | Resource Path                                                     | Description                                                 |
| :------------------------------ | :----------------------------------------------------------- | :--------------------------------------------------- |
| DeleteGameServerSessionQueue    | `qcs::gse:$region:$account:game`<br>`ServerSessionQueue/*`<br>`qcs::gse:$region:$account:game`<br>`ServerSessionQueue/$Name` | Deletes a game server session queue                              |
| StartGameServerSessionPlacement | `qcs::gse:$region:$account:game`<br>`ServerSessionQueue/*`<br>`qcs::gse:$region:$account:game`<br>`ServerSessionQueue/$GameServer`<br>`SessionQueueName` | Starts sending a placement request for a game server session<br> to a game server session queue  |
| UpdateGameServerSessionQueue    | `qcs::gse:$region:$account:game`<br>`ServerSessionQueue/*`<br>`qcs::gse:$region:$account:game`<br>`ServerSessionQueue/$Name` | Updates the attributes of a game server session queue                           |
