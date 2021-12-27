## Basic CAM Concepts

A root account authorizes sub-accounts by binding policies. The policy settings can be specific to the level of **API, Resource, User/User Group, Allow/Deny, and Condition**.

#### Account

- **Root account**: it owns all Tencent Cloud resources and can access any of its resources.
- **Sub-account**: it includes sub-users and collaborators.
- **Sub-user**: it is created and fully owned by a root account.
- **Collaborator**: it has the identity of a root account. After it is added as a collaborator of the current root account, it becomes one of the sub-accounts of the current root account and can switch back to its root account identity.
- **Identity credential**: it includes login credentials and access certificates. **Login credential** refers to a user's login name and password. **Access certificate** refers to Tencent Cloud API keys (`SecretId` and `SecretKey`).

#### Resource and permission

- **Resource**: it is an object manipulated in Tencent Cloud services. TDMQ resources include clusters, namespaces, topics, and groups.
- **Permission**: it is an authorization that allows or forbids users to perform certain operations. By default, **a root account has full access to all resources under it**, while **a sub-account does not have access to any resources under its root account**.
- **Policy**: it is a syntax rule that defines and describes one or more permissions. The **root account** performs authorization by **associating policies** with users/user groups.

[View CAM documentation >>](https://intl.cloud.tencent.com/document/product/598/10583)

## Relevant Documents

| Document Description | Link |
| ------------------------ | ------------------------------------------------------------ |
| Relationship between policy and user | [Policy](https://intl.cloud.tencent.com/document/product/598/10601) |
| Basic policy structure | [Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10603) |
| CAM-Enabled products | [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588) |

## List of APIs Supporting Resource-Level Authorization

TDMQ supports resource-level authorization. You can grant a specified sub-account the API permission of a specified resource.

APIs supporting resource-level authorization include:

| API                       | Description                            | Resource Type         | Six-Segment Example of Resource                                               |
| ---------------------------------------- | ------------------------------------ | --------- | ------------------------------------------------------------ |
| ResetRocketMQConsumerOffSet              | Resets RocketMQ consumption offset                 | consumer  | qcs::tdmq:${region}:uin/${uin}:consumer/${clusterId}/${namespaceId}/${topic}/${groupId} |
| DescribeRocketMQClusters                 | Gets the list of RocketMQ clusters                 | cluster   | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |
| DeleteRocketMQCluster                    | Deletes RocketMQ cluster                     | cluster   | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |
| DescribeRocketMQCluster                  | Gets the information of specific RocketMQ cluster             | cluster   | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |
| CreateRocketMQNamespace                  | Creates RocketMQ namespace                 | cluster   | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |
| ModifyRocketMQNamespace                  | Updates RocketMQ namespace                 | namespace | qcs::tdmq:${region}:uin/${uin}:namespace/${clusterId}/${namespace} |
| DeleteRocketMQNamespace                  | Deletes RocketMQ namespace                 | namespace | qcs::tdmq:${region}:uin/${uin}:namespace/${clusterId}/${namespace} |
| CreateRocketMQGroup                      | Creates RocketMQ consumer group                   | namespace | qcs::tdmq:${region}:uin/${uin}:namespace/${clusterId}/${namespace} |
| ModifyRocketMQGroup                      | Updates RocketMQ consumer group               | group     | qcs::tdmq:${region}:uin/${uin}:group/${clusterId}/${namespaceId}/${groupId} |
| DescribeRocketMQGroups                   | Gets the list of RocketMQ consumer groups               | group     | qcs::tdmq:${region}:uin/${uin}:group/${clusterId}/${namespaceId}/${groupId} |
| DeleteRocketMQGroup                      | Deletes RocketMQ consumer group                   | group     | qcs::tdmq:${region}:uin/${uin}:group/${clusterId}/${namespaceId}/${groupId} |
| CreateRocketMQTopic                      | Creates RocketMQ topic                     | namespace | qcs::tdmq:${region}:uin/${uin}:namespace/${clusterId}/${namespace} |
| ModifyRocketMQTopic                      | Updates RocketMQ topic                 | topic     | qcs::tdmq:${region}:uin/${uin}:topic/${clusterId}/${namespaceId}/${topicName} |
| DeleteRocketMQTopic                      | Deletes RocketMQ topic                     | topic     | qcs::tdmq:${region}:uin/${uin}:topic/${clusterId}/${namespaceId}/${topicName} |
| DescribeRocketMQTopics                   | Gets the list of RocketMQ topics                 | topic     | qcs::tdmq:${region}:uin/${uin}:topic/${clusterId}/${namespaceId}/${topicName} |
| DescribeRocketMQTopicsByGroup            | Gets the list of topics subscribed to specified consumer group       | topic     | qcs::tdmq:${region}:uin/${uin}:topic/${clusterId}/${namespaceId}/${topicName} |
| DescribeRocketMQConsumerConnections      | Gets the current client connection status under specified consumer group | group     | qcs::tdmq:${region}:uin/${uin}:group/${clusterId}/${namespaceId}/${groupId} |
| DescribeRocketMQConsumerConnectionDetail | Gets the details of online consumers                   | group     | qcs::tdmq:${region}:uin/${uin}:group/${clusterId}/${namespaceId}/${groupId} |
| ModifyRocketMQCluster                    | Modifies RocketMQ cluster                 | cluster   | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |

## List of APIs Not Supporting Resource-Level Authorization

| API Name | Description | Six-Segment Resource |
| --------------------- | ---------------- | ---------- |
| CreateRocketMQCluster | Creates RocketMQ cluster | *          |

## Authorization Scheme Examples

### Full access policy

Grant a sub-user full access to the TDMQ for RocketMQ service (for creating, managing, etc.).

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. Click **[Policy](https://console.cloud.tencent.com/cam/policy)** on the left sidebar.
3. In the policy list, click **Create Custom Policy**.
4. In the **Select Policy Creation Method** pop-up window, select **Create by Policy Generator**.
5. On the **Edit Policy** page, click **Import Policy Syntax** in the top-right corner.
6. On the **Import Policy Syntax** page, search for **TDMQ**, select **QcloudTDMQFullAccess** in the search results, and click **OK**.
7. On the **Edit Policy** page, click **Next**, enter the policy name and description, and select the user/user group you want to associate.
8. Click **Complete**.

### Read-Only access policy

The following uses granting the read-only permission of a cluster as an example.

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. Click **[Policy](https://console.cloud.tencent.com/cam/policy)** on the left sidebar.
3. In the policy list, click **Create Custom Policy**.
4. In the **Select Policy Creation Method** pop-up window, select **Create by Policy Generator** and enter the policy information.


   | Parameter              | Description                                                         |
   | ----------------- | ------------------------------------------------------------ |
   | Effect    | Select **Allow**                                                 |
   | Service   | Select **TDMQ**                                 |
   | Action    | Select **Read operation**                                               |
   | Resource  | Select **Specific resources** and click **Add six-segment resource description**<li>Region: select the resource region</li><li>Account: it is automatically populated</li><li>Resource Prefix: clusterId</li><li>Enter the ID of the cluster you want to authorize</li> |
   | Condition | Allow access to specified operations only when the request is from the specified IP range           |

5. Click **Next**, enter the policy name and description, and select the user/user group you want to associate.
6. Click **Complete**.
