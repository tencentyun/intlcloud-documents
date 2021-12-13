## Basic CAM Concepts

A root account authorizes sub-accounts by binding policies. The policy settings can be specific to the level of **API, Resource, User/User Group, Allow/Deny, and Condition**.

#### Account

- **Root account**: it owns all Tencent Cloud resources and can access any of its resources.
- **Sub-account**: it includes sub-users and collaborators.
- **Sub-user**: it is created and fully owned by a root account.
- **Collaborator**: it has the identity of a root account. After it is added as a collaborator of the current root account, it becomes one of the sub-accounts of the current root account and can switch back to its root account identity.
- **Identity credential**: it includes login credentials and access certificates. **Login credential** refers to a user's login name and password. **Access certificate** refers to Tencent Cloud API keys (`SecretId` and `SecretKey`).

#### Resource and permission

- **Resource**: it is an object manipulated in Tencent Cloud services. TDMQ for Pulsar resources include clusters, namespaces, topics, and subscriptions.
- **Permission**: it is an authorization that allows or forbids users to perform certain operations. By default, **a root account has full access to all resources under it**, while **a sub-account does not have access to any resources under its root account**.
- **Policy**: it is a syntax rule that defines and describes one or more permissions. The **root account** performs authorization by **associating policies** with users/user groups.

[View CAM documentation >>](https://intl.cloud.tencent.com/document/product/598/10583)

## CAM Documentation

| Document Description | Link |
| ------------------------ | ------------------------------------------------------------ |
| Relationship between policy and user | [Policy](https://intl.cloud.tencent.com/document/product/598/10601) |
| Basic policy structure | [Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10603) |
| CAM-Enabled products | [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588) |

## List of APIs Supporting Resource-Level Authorization

TDMQ for Pulsar supports resource-level authorization. You can grant a specified sub-account the API permission of a specified resource.

APIs supporting resource-level authorization include:

| API                       | Description                            | Resource Type         | Six-Segment Example of Resource                                               |
| ----------------------------- | ---------------------------------- | ---------------- | ------------------------------------------------------------ |
| DescribeClusterDetail         | Gets cluster details                   | cluster          | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |
| DescribeBindClusters          | Gets the list of dedicated clusters                   | cluster          | qcs::tdmq:${region}:uin/${uin}:cluster/${cluster}            |
| DescribeClusters              | Gets the list of clusters                       | cluster          | qcs::tdmq:${region}:uin/${uin}:cluster/${cluster}            |
| ModifyCluster                 | Modifies cluster                           | cluster          | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |
| DeleteCluster                 | Deletes cluster                           | cluster          | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |
| CreateRole                    | Creates role                           | cluster          | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |
| DeleteRoles                   | Deletes role                           | cluster          | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |
| CreateEnvironment             | Creates environment                           | cluster          | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |
| CreateTopic                   | Creates topic                           | environment      | qcs::tdmq:${region}:uin/${uin}:environment/${clusterId}/${environmentId} |
| ModifyEnvironmentAttributes   | Modifies environment attributes                       | environment      | qcs::tdmq:${region}:uin/${uin}:environment/${clusterId}/${environmentId} |
| DeleteEnvironments            | Deletes environment                           | environment      | qcs::tdmq:${region}:uin/${uin}:environment/${clusterId}/${environmentId} |
| DescribeEnvironments          | Gets the list of environments                       | environmentId    | qcs::tdmq:${region}:uin/${uin}:environmentId/${clusterId}/${environmentId} |
| DescribeEnvironmentAttributes | Gets environment attributes                       | environmentId    | qcs::tdmq:${region}:uin/${uin}:environmentId/${clusterId}/${environmentId} |
| DescribeEnvironmentRoles      | Gets the list of environment roles                   | environmentRoles | qcs::tdmq:${region}:uin/${uin}:environmentRoles/${clusterId}/${environmentId}/${roleName} |
| CreateEnvironmentRole         | Creates environment role                   | environmentRole  | qcs::tdmq:${region}:uin/${uin}:environmentRole/${clusterId}/${environmentId}/${roleName} |
| DeleteEnvironmentRoles        | Deletes environment role                   | environmentRole  | qcs::tdmq:${region}:uin/${uin}:environmentRole/${clusterId}/${environmentId}/${roleName} |
| ModifyEnvironmentRole         | Modifies environment role                   | environmentRole  | qcs::tdmq:${region}:uin/${uin}:environmentRole/${clusterId}/${environmentId}/${roleName} |
| DescribeMsgTrace              | Queries message trace                           | topic            | qcs::tdmq:${region}:uin/${uin}:topic/${clusterId}/${environmentId}/${topicName} |
| DescribeMsg                   | Queries message details                           | topic            | qcs::tdmq:${region}:uin/${uin}:topic/${clusterId}/${environmentId}/${topicName} |
| DescribeTopicMsgs             | Queries message                           | topic            | qcs::tdmq:${region}:uin/${uin}:topic/${clusterId}/${environmentId}/${topicName} |
| DescribeTopics                | Queries the list of topics                       | topic            | qcs::tdmq:${region}:uin/${uin}:topic/${clusterId}/${environmentId}/${topicName} |
| DescribeProducers             | Gets the list of producers                     | topic            | qcs::tdmq:${region}:uin/${uin}:topic/${clusterId}/${environmentId}/${topicName} |
| DeleteTopics                  | Batch deletes topics                     | topic            | qcs::tdmq:${region}:uin/${uin}:topic/${clusterId}/${environmentId}/${topicSets.topicName} |
| ModifyTopic                   | Modifies topic                           | topic            | qcs::tdmq:${region}:uin/${uin}:topic/${clusterId}/${environmentId}/${topicName} |
| CreateSubscription            | Creates subscription to topic            | topic            | qcs::tdmq:${region}:uin/${uin}:topic/${clusterId}/${environmentId}/${topicName} |
| ResetMsgSubOffsetByTimestamp  | Rewinds message by timestamp, accurate down to the millisecond | subscription     | qcs::tdmq:${region}:uin/${uin}:subscription/$clusterId/$environmentId/$topicName/$subscriptionName |
| DeleteSubscriptions           | Deletes subscription                       | subscription     | qcs::tdmq:${region}:uin/${uin}:subscription/${clusterId}/${environmentId}/${topicName}/${subscriptionName} |
| DescribeRealTimeSubscription  | Queries the list of real-time consumption subscriptions                   | subscription     | qcs::tdmq:${region}:uin/${uin}:subscription/${clusterId}/${environmentId}/${topicName}/${subscriptionName} |
| DescribeSubscriptions         | Queries the list of consumption subscriptions                       | subscription     | qcs::tdmq:${region}:uin/${uin}:subscription/${clusterId}/${environmentId}/${topicName}/${subscriptionName} |
| ModifyRole                    | Modifies role                           | role             | qcs::tdmq:${region}:uin/${uin}:role/${clusterId}/${roleName} |
| DescribeRoles                 | Gets the list of roles                       | role             | qcs::tdmq:${region}:uin/${uin}:role/${clusterId}/${roleName} |

## List of APIs Not Supporting Resource-Level Authorization

| API      | Description |
| ------------- | -------- |
| CreateCluster | Creates cluster |

## Authorization Scheme Examples

### Full access policy

Grant a sub-user full access to the TDMQ for Pulsar service (for creating, managing, etc.).

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. Click **[Policy](https://console.cloud.tencent.com/cam/policy)** on the left sidebar.
3. In the policy list, click **Create Custom Policy**.
4. In the **Select Policy Creation Method** pop-up window, select **Create by Policy Generator**.
5. On the **Edit Policy** page, click **Import Policy Syntax** in the top-right corner.
6. On the **Import Policy Syntax** page, search for **TDMQ**, select **QcloudTDMQFullAccess** in the search results, and click **OK**.
7. On the **Edit Policy** page, click **Next**, enter the policy name and description, and select the user/user group you want to associate.
8. Click **Complete**.

### Read-Only access policy

The following uses granting the read-only permission of a topic as an example.

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. Click **[Policy](https://console.cloud.tencent.com/cam/policy)** on the left sidebar.
3. In the policy list, click **Create Custom Policy**.
4. In the **Select Policy Creation Method** pop-up window, select **Create by Policy Generator** and enter the policy information.
![](https://qcloudimg.tencent-cloud.cn/raw/f906af44d09f73bd30caf692a9e2f414.png)

| Parameter              | Description                                                         |
| ----------------- | ------------------------------------------------------------ |
| Effect    | Select **Allow**                                                 |
| Service   | Select **TDMQ**                                 |
| Action    | Select **Read operation**                                               |
| Resource  | Select **Specific resources** and click **Add six-segment resource description**<li>Region: select the resource region</li><li>Account: it is automatically populated</li><li>Resource Prefix: topic</li><li>Enter the name of the topic you want to authorize</li> |
| Condition | Allow access to specified operations only when the request is from the specified IP range           |

5. Click **Next**, enter the policy name and description, and select the user/user group you want to associate.
6. Click **Complete**.
