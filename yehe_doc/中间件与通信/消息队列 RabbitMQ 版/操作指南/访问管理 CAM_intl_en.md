## Basic CAM Concepts

A root account authorizes sub-accounts by binding policies. The policy settings can be specific to the level of **API, Resource, User/User Group, Allow/Deny, and Condition**.

#### Account

- **Root account**: it owns all Tencent Cloud resources and can access any of its resources.
- **Sub-account**: it includes sub-users and collaborators.
- **Sub-user**: it is created and fully owned by a root account.
- **Collaborator**: it has the identity of a root account. After it is added as a collaborator of the current root account, it becomes one of the sub-accounts of the current root account and can switch back to its root account identity.
- **Identity credential**: it includes login credentials and access certificates. **Login credential** refers to a user's login name and password. **Access certificate** refers to Tencent Cloud API keys (`SecretId` and `SecretKey`).

#### Resource and permission

- **Resource**: it is an object manipulated in Tencent Cloud services. TDMQ for RabbitMQ resources include clusters, vhosts, exchanges, queues, and bindings.
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

TDMQ for RabbitMQ supports resource-level authorization. You can grant a specified sub-account the API permission of a specified resource.

APIs supporting resource-level authorization include:

| API                       | Description                            | Resource Type         | Six-Segment Example of Resource                                               |
| ---------------------------- | ------------------------ | ------------- | ------------------------------------------------------------ |
| DeleteAMQPCluster            | Deletes AMQP cluster             | cluster       | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |
| ModifyAMQPCluster            | Modifies AMQP cluster             | cluster       | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |
| CreateAMQPVHost              | Creates AMQP vhost           | cluster       | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |
| DescribeAMQPClusters         | Queries the list of AMQP clusters        | cluster       | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |
| DescribeAMQPCluster          | Gets the information of specific AMQP cluster     | cluster       | qcs::tdmq:${region}:uin/${uin}:cluster/${clusterId}          |
| CreateAMQPExchange           | Creates AMQP exchange        | vhost         | qcs::tdmq:${region}:uin/${uin}:vHost/${clusterId}/${vHostId} |
| ModifyAMQPVHost              | Modifies AMQP vhost           | vhost         | qcs::tdmq:${region}:uin/${uin}:vHost/${clusterId}/${vHostId} |
| DeleteAMQPVHost              | Deletes AMQP vhost           | vhost         | qcs::tdmq:${region}:uin/${uin}:vHost/${clusterId}/${vHostId} |
| CreateAMQPQueue              | Creates AMQP queue             | vhost         | qcs::tdmq:${region}:uin/${uin}:vHost/${clusterId}/${vHostId} |
| CreateAMQPRouteRelation      | Creates AMQP binding         | vhost         | qcs::tdmq:${region}:uin/${uin}:vHost/${clusterId}/${vHostId} |
| DescribeAMQPVHostConnections | Queries the list of AMQP vhost connections   | vhost         | qcs::tdmq:${region}:uin/${uin}:vHost/${clusterId}/${vHostId} |
| DescribeAMQPVHosts           | Queries the list of AMQP vhosts       | vhost         | qcs::tdmq:${region}:uin/${uin}:vHost/${clusterId}/${vHostId} |
| DeleteAMQPExchange           | Deletes AMQP exchange        | exchange      | qcs::tdmq:${region}:uin/${uin}:exchange/${clusterId}/${vHostId}/${exchangeName} |
| ModifyAMQPExchange           | Modifies AMQP exchange        | exchange      | qcs::tdmq:${region}:uin/${uin}:exchange/${clusterId}/${vHostId}/${exchangeName} |
| DescribeAMQPExchanges        | Queries the list of AMQP exchanges    | exchange      | qcs::tdmq:${region}:uin/${uin}:exchange/${clusterId}/${vHostId}/${exchangeName} |
| DeleteAMQPQueue              | Deletes AMQP queue             | queue         | qcs::tdmq:${region}:uin/${uin}:queue/${clusterId}/${vHostId}/${queueName} |
| DescribeAMQPQueueConsumers   | Gets the list of consumers in specified queue | queue         | qcs::tdmq:${region}:uin/${uin}:queue/${clusterId}/${vHostId}/${queueName} |
| ModifyAMQPQueue              | Modifies AMQP queue             | queue         | qcs::tdmq:${region}:uin/${uin}:queue/${clusterId}/${vHostId}/${queueName} |
| DescribeAMQPQueues           | Queries the list of AMQP queues         | queue         | qcs::tdmq:${region}:uin/${uin}:queue/${clusterId}/${vHostId}/${queueName} |
| DescribeAMQPRouteRelations   | Queries the list of AMQP bindings    | routeRelation | qcs::tdmq:${region}:uin/${uin}:routeRelation/${clusterId}/${vHostId}/${routeRelationId} |
| DeleteAMQPRouteRelation      | Deletes AMQP binding         | routeRelation | qcs::tdmq:${region}:uin/${uin}:routeRelation/${clusterId}/${vHostId}/${routeRelationId} |

## List of APIs Not Supporting Resource-Level Authorization

| API                  | Description     | Six-Segment Resource |
| ----------------------- | ------------ | ---------- |
| CreateAMQPCluster       | Creates AMQP cluster | *          |
| DescribeAMQPCreateQuota | Gets user quota | *          |

## Authorization Scheme Examples

### Full access policy

Grant a sub-user full access to the TDMQ for RabbitMQ service (for creating, managing, etc.).

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
2. Click **Policy** on the left sidebar.
3. In the policy list, click **Create Custom Policy**.
4. In the **Select Policy Creation Method** pop-up window, select **Create by Policy Generator** and enter the policy information.
   ![](https://main.qcloudimg.com/raw/a7aeab929146566a758eb85374758db8.png)


   | Parameter              | Description                                                         |
   | ----------------- | ------------------------------------------------------------ |
   | Effect    | Select **Allow**                                                 |
   | Service   | Select **TDMQ**                                 |
   | Action    | Select **Read operation**                                               |
   | Resource  | Select **Specific resources** and click **Add six-segment resource description**<li>Region: select the resource region</li><li>Account: it is automatically populated</li><li>Resource Prefix: clusterId</li><li>Enter the ID of the cluster you want to authorize</li> |
   | Condition | Allow access to specified operations only when the request is from the specified IP range           |

5. Click **Next**, enter the policy name and description, and select the user/user group you want to associate.
6. Click **Complete**.
