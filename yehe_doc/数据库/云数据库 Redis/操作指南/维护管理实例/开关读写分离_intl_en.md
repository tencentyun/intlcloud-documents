## Overview

TencentDB for Redis supports [read/write separation](https://intl.cloud.tencent.com/document/product/239/33132) for business scenarios with more reads but less writes. This can well sustain read requests to hotspot data.

## Billing

The read-only replica feature is currently in free trial.

## Overview

- Enabling read/write separation may cause data read inconsistency (the data on replica nodes are older than that on the master node). Therefore, you need to check whether your business can tolerate data inconsistency first.
- Disabling read/write separation may interrupt existing connections momentarily, so we recommend you do so during off-peak hours.

## Prerequisites

- The database instance is on v4.0 or later.
- The database instance is in **Running** status.

## Directions
### Enabling read/write separation
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the **instance list** on the right, select the region.
3. In the instance list, find the target instance.
4. Click the instance ID to enter the **Instance Details** page and click the **Node Management** tab.
5. In the top-right corner of the **Node Management** tab, click <img src="https://qcloudimg.tencent-cloud.cn/raw/3ce8bb2870c4ab539b9b721a6e8b0032.png" style="zoom: 33%;" /> next to **Read-Only Replica**.
![](https://main.qcloudimg.com/raw/1d66625e3868fa6850648bd1737f7435.png)
6. In the pop-up window, configure read-only replica nodes. The parameters are as detailed below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/518ee9eda54a17fa431dfc419cc2a899.png" style="zoom: 90%;" />
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Account Name</td>
<td>It is fixed to the <strong>Default account</strong>; that is, the system can enable read-only replicas only for the default account.</td></tr>
<tr>
<td>Command Permission</td>
<td>It is fixed to <strong>Read/Write</strong>; that is, the default account has the read/write permissions.</td></tr>
<tr>
<td>Read-Only Routing Policy</td>
<td>It is <b>Replica Node</b> by default. You can also select <b>Master Node</b> or select both <b>Replica Node</b> and <b>Master Node</b>. Read requests are automatically routed to the configured read-only nodes by load balancing.</td></tr>
<tr>
<td>Read Local Nodes Only</td>
<td>This parameter will be displayed if the instance is deployed in multiple AZs. It is fixed to <strong>Disabled</strong>. You can configure the `read-local-node-only` parameter on the <strong>Parameter Settings</strong> page in the console to enable/disable this feature.</td></tr>
<tr>
<td>Fees</td>
<td>This feature is current in free trial.</td></tr>
</tbody></table>
7. After confirming that the parameter settings are correct, click **OK**.
8. The **Instance Status** will change to **Processing**. Wait for it to change to **Running**. Then, in the **Specs Info** section on the **Instance Details** page, you can see that **Read-Only Replica** is **Enabled** and try out read/write separation.

### Disabling read/write separation

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the **instance list** on the right, select the region.
3. In the instance list, find the target instance.
4. Click the instance ID to enter the **Instance Details** page and click the **Node Management** tab.
5. In the top-right corner of the **Node Management** tab, click <img src="https://qcloudimg.tencent-cloud.cn/raw/1d39ae259604af20416d8f35ff0ae0a6.png" style="zoom:33%;" /> next to **Read-Only Replica**.
6. In the **Disable Read-Only Replica** window, read the note on the impact of disabling read-only replica and click **OK**.
7. The **Instance Status** will change to **Processing**. Wait for it to change to **Running**. Then, in the **Specs Info** section on the **Instance Details** page, you can see that **Read-Only Replica** is **Disabled**.

## Related APIs

| API | Description |
| :----------------------------------------------------------- | :----------- |
| [EnableReplicaReadonly](https://intl.cloud.tencent.com/document/product/239/32060) | Enables read/write separation |
| [DisableReplicaReadonly](https://intl.cloud.tencent.com/document/product/239/32061) | Disables read/write separation |

