## Basic CAM Concepts

A root account authorizes sub-accounts by binding policies. The policy settings can be specific to the level of **API, Resource, User/User Group, Allow/Deny, and Condition**.

#### Account

- **Root account**: it owns all Tencent Cloud resources and can access any of its resources.
- **Sub-account**: it includes sub-users and collaborators.
- **Sub-user**: it is created and fully owned by a root account.
- **Collaborator**: it has the identity of a root account. After it is added as a collaborator of the current root account, it becomes one of the sub-accounts of the current root account and can switch back to its root account identity.
- **Identity credential**: it includes login credentials and access certificates. **Login credential** refers to a user's login name and password. **Access certificate** refers to Tencent Cloud API keys (`SecretId` and `SecretKey`).

#### Resource and permission

- **Resource**: it is an object manipulated in Tencent Cloud services. TDMQ for CMQ resources include topics and queues.
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

TDMQ for CMQ supports resource-level authorization. You can grant a specified sub-account the API permission of a specified resource.

APIs supporting resource-level authorization include:

| API                       | Description                            | Resource Type         | Six-Segment Example of Resource                                               |
| --------------------------------- | ----------------------- | -------- | ------------------------------------------------------------ |
| ModifyCmqTopicAttribute           | Modifies TDMQ for CMQ topic         | Topic     | qcs::tdmq:${region}:uin/${uin}:topic/${topicName}            |
| CreateCmqSubscribe                | Creates TDMQ for CMQ subscription         | Topic     | qcs::tdmq:${region}:uin/${uin}:topic/${topicName}            |
| ModifyCmqSubscriptionAttribute    | Modifies TDMQ for CMQ subscription         | Subscription     | qcs::tdmq:${region}:uin/${uin}:subscription/${topicName}/${subscriptionName} |
| RewindCmqQueue                    | Rewinds TDMQ for CMQ queue             | Queue     | qcs::tdmq:${region}:uin/${uin}:queue/${queueName}            |
| ModifyCmqQueueAttribute           | Modifies TDMQ for CMQ queue         | Queue     | qcs::tdmq:${region}:uin/${uin}:queue/${queueName}            |
| ClearCmqSubscriptionFilterTags    | Clears message subscription tags in TDMQ for CMQ   | Subscription      | qcs::tdmq:${region}:uin/${uin}:subscription/${topicName}/${subscriptionName} |
| ClearCmqQueue                     | Clears messages in TDMQ for CMQ queue | Queue     | qcs::tdmq:${region}:uin/${uin}:queue/${queueName}            |
| DeleteCmqSubscribe                | Deletes TDMQ for CMQ subscription             | Subscription     | qcs::tdmq:${region}:uin/${uin}:subscription/${topicName}/${subscriptionName} |
| DeleteCmqTopic                    | Deletes TDMQ for CMQ topic             | Topic    | qcs::tdmq:${region}:uin/${uin}:topic/${topicName}            |
| UnbindCmqDeadLetter               | Unbinds TDMQ for CMQ dead letter queue         | Queue     | qcs::tdmq:${region}:uin/${uin}:queue/${sourceQueueName}      |
| DescribeCmqDeadLetterSourceQueues | Enumerates dead letter source queues in TDMQ for CMQ   | Dead letter queue | qcs::tdmq:${region}:uin/${uin}:dlq/${sourceQueueName}/${deadLetterQueueName} |
| DescribeCmqTopics                 | Enumerates all TDMQ for CMQ topics         | Topic     | qcs::tdmq:${region}:uin/${uin}:topic/${topicName}            |
| DescribeCmqSubscriptionDetail     | Queries the details of TDMQ for CMQ subscription         | Topic     | qcs::tdmq:${region}:uin/${uin}:topic/${topicName}/${subscriptionName} |
| DescribeCmqQueues                 | Queries all TDMQ for CMQ queues         | Queue     | qcs::tdmq:${region}:uin/${uin}:queue/${queueName}            |
| PublishCmqMsg                     | Sends message to topic in TDMQ for CMQ         | Topic     | qcs::tdmq:${region}:uin/${uin}:topic/${topicName}            |
| SendCmqMsg                        | Sends message in TDMQ for CMQ             | Queue     | qcs::tdmq:${region}:uin/${uin}:queue/${queueName}            |
| DescribeCmqTopicDetail            | Queries the details of TDMQ for CMQ topic         | Topic     | qcs::tdmq:${region}:uin/${uin}:topic/${topicName}qcs::tdmq:${region}:uin/${uin}:queue/${queueName} |
| DescribeCmqQueueDetail            | Queries the details of TDMQ for CMQ queue         | Queue     | qcs::tdmq:${region}:uin/${uin}:queue/${queueName}            |
| DeleteCmqQueue                    | Deletes TDMQ for CMQ queue             | Queue     | qcs::tdmq:${region}:uin/${uin}:queue/${queueName}            |

## List of APIs Not Supporting Resource-Level Authorization

| API Name | Description | Six-Segment Resource |
| -------------- | --------------- | ---------- |
| CreateCmqTopic | Creates TDMQ for CMQ topic     | *          |
| CreateCmqQueue | Creates TDMQ for CMQ queue |   *          |

## Authorization Scheme Examples

### Full access policy

Grant a sub-user full access to the TDMQ for CMQ queue service (for creating, managing, etc.).

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. Click **Policy** on the left sidebar.
3. In the policy list, click **Create Custom Policy**.
4. In the **Select Policy Creation Method** pop-up window, select **Create by Policy Generator**.
5. On the **Edit Policy** page, click **Import Policy Syntax** in the top-right corner.
6. On the **Import Policy Syntax** page, search for **TDMQ**, select **QcloudTDMQFullAccess** in the search results, and click **OK**.
7. On the **Edit Policy** page, click **Next**, enter the policy name and description, and select the user/user group you want to associate.
8. Click **Complete**.

### Read-Only access policy

The following uses granting the read-only permission of a queue service as an example.

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. Click **Policy** on the left sidebar.
3. In the policy list, click **Create Custom Policy**.
4. In the **Select Policy Creation Method** pop-up window, select **Create by Policy Generator** and enter the policy information.


   | Parameter              | Description                                                         |
   | ----------------- | ------------------------------------------------------------ |
   | Effect    | Select **Allow**                                                 |
   | Service   | Select **TDMQ**                                 |
   | Action    | Select **Read operation**                                               |
   | Resource  | Select **Specific resources** and click **Add six-segment resource description**<li>Region: select the resource region</li><li>Account: it is automatically populated</li><li>Resource Prefix: queue</li><li>Enter the name of the queue service you want to authorize</li> |
   | Condition | Allow access to specified operations only when the request is from the specified IP range           |

5. Click **Next**, enter the policy name and description, and select the user/user group you want to associate.
6. Click **Complete**.

