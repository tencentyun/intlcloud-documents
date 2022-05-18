## Overview

DataHub offers data distribution capabilities. You can distribute CKafka data to ClickHouse for further storage, query, and analysis.

## Prerequisites

- To use CDWCH, you need to activate it in advance. In addition, data distribution to self-built ClickHouse is also supported.
- Create a table in ClickHouse and specify a column and type during table creation.

## Directions

### Creating task

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar, select the region, and click **Create Task**.
3. Select **ClickHouse** as the **Target Type**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/491af4f90cf7371429b5feeeb92fe17e.png)

### Configuring CKafka data source
On the settings page, set the following CKafka configuration items:
1. **Task Name**: It can only contain letters, digits, underscores, or symbols ("-" and ".").
2. **CKafka Instance**: Select the source CKafka instance.
3. **Source Topic**: Select a topic under the instance. A data distribution task supports up to five source topics. Data in this topic can be successfully dumped only if it is in the same format.

### Parsing message
After completing the above settings, click **Preview Data**, and the first message from the specified **Source Topic** will be obtained and parsed.
>? Currently, message parsing must meet the following requirements:
>- The message is a JSON string.
>- The message after parsing is a single-level JSON string. Currently, JSON strings with a nested structure cannot be parsed.
> 
> If the message is not a single-level JSON string, we recommend you use [**data processing**](https://console.intl.cloud.tencent.com/ckafka/datahub-process) for message format conversion first. 
> 
Click **Preview Topic Message**, and the parsed message fields will be displayed in the console. You can modify the `type` attribute in the preview result to set the type of the target column for data delivery.
When you select `Date` or `DateTime` as the `type`, if the source message format is integer, the `unix timestamp` format will be used for parsing; if it is string, a common time format pattern string will be used for parsing.

### Configuring data distribution
Supported ClickHouse database types for data distribution include [**CDWCH**](https://console.intl.cloud.tencent.com/cdwch) and **self-built ClickHouse** databases.
<dx-tabs>
::: CDWCH [](id:UseCDWClickHouseSink)
As a **CDWCH** instance has been encapsulated with a private connection during creation, you can directly select the corresponding **CDWCH** instance in the console, and the data distribution feature will automatically connect to the instance's VPC.
:::

::: Self-built or EMR ClickHouse [](id:UseSelfHostOrEMRClickHouseSink)
As the CKafka instance is a managed instance and EMR ClickHouse creates a public network route on the purchased CVM instance directly, you need to manually create a CLB instance to connect to the VPC. The following steps use EMR ClickHouse as an example to create a CLB instance:
Go to the [EMR console](https://console.intl.cloud.tencent.com/emr), select the target cluster, click **Cluster Resource** > **Node Status**, and find the ClickHouse node IP on the status page.
Go to the [CLB](https://console.intl.cloud.tencent.com/clb) console, create a CLB instance, click **Listener Management** on the top, click **TCP/UDP/TCP SSL Listener** on the page, and enter the **port used during data distribution** as the port.
After creating a listener, click **Bind Backend Service** and enter the TCP port of ClickHouse, which is 9000 by default.
After binding, you can select the created CLB instance and enter the port listened on by the **CLB** instance on the data distribution page in the CKafka console.

>? Currently, you can create a data distribution to ClickHouse task only in the same region as the CLB instance.
>
:::
</dx-tabs>

After the network is connected, you need to set the following configuration items of the data distribution target instance:
- Username: Target ClickHouse username, which is `default` by default.
- Password: Target ClickHouse password.
>!For security reasons, the ClickHouse password is required for data distribution.
> Currently, the password after instance creation may be empty, in which case you need to modify the password in the `user.xml` configuration file. For detailed directions, see [User Settings](https://clickhouse.com/docs/en/operations/settings/settings-users/). 
- Cluster: ClickHouse cluster name, which is `default_cluster` by default.
- Database: Database name set in ClickHouse.
- Table: Name of the table created in the database. Currently, no table will be created automatically during data distribution to ClickHouse, **so you need to manually create the current target table in ClickHouse**.
- Discard Message with Parsing Failure: A message parsing failure may occur if the message field type differs from that of the target database. If you don't discard the message that can't be parsed, exceptions may occur and data dumping will be stopped.

Click **Submit**.

## Configuring Monitoring


1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar and click the **ID** of the target task to enter its basic information page.
3. At the top of the task details page, click **Monitoring**, select the resource to be viewed, and set the time range to view the corresponding monitoring data.


## Restrictions and Billing

The dump speed is subject to the limit of the peak bandwidth of the CKafka instance. If the consumption is too slow, check the peak bandwidth settings or increase the number of CKafka partitions.
