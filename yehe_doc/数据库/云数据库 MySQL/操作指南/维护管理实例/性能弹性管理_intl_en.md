TencentDB for MySQL supports manual expansion of the CPU upper limit of the current instance, and can also automatically scale based on the configured average CPU utilization threshold and observation period. In this way, it can better alleviate the performance pressure caused by sudden requests and adapt to business peaks traffic to ensure the stability of online business. This document describes the elastic performance management feature.
## Prerequisites
- TencentDB for MySQL instances are on the following architectures: two-node on general edition, three-node on general edition, or single-node on local disk edition (read-only instance).
- Computing specifications cannot exceed 32 cores.
- There must be sufficient balance in the Tencent Cloud account to support expansion.

## How It Works
## Billing Formula
The elastic performance management feature is pay-as-you-go. It is billed by minute and deducted once every hour.
**Billing formula = (single-core fee x increased number of CPU cores) x expansion duration (minutes)/60**
**Examples**
1. The CPU specification of a two-node instance in the Guangzhou region is 4 cores. After the automatic performance expansion is triggered, it will be increased to 8 cores. The expansion time is 1 hour. The unit price in the Guangzhou region is 0.08 USD/core/hour, then the billing is: 0.08 (unit price ) x 4 (additional number of CPU cores) x 1 (expansion time) = 0.32 USD.
2. The CPU specification of a two-node instance in the Guangzhou region is 2 cores. After the automatic performance expansion is triggered, it will be increased to 4 cores. The expansion time is 30 minutes. The unit price in the Guangzhou region is 0.08 USD/core/hour, then the billing is: 0.08 (unit price ) x 2 (additional number of CPU cores) x 30/60 (expansion time) = 0.08 USD.

## Single-Core Unit Price
<dx-tabs>
::: Single-Node on Local Disk Edition (Read-Only Instance)
| Region | Price (USD/Core/Hour) |
|---------|---------|
| Chengdu, Chongqing | 0.03 |
| Guangzhou, Shanghai, Beijing, and Nanjing | 0.04 |
| Hong Kong (China), Tokyo, Seoul, Mumbai, Bangkok | 0.0495 |
| Frankfurt, São Paulo | 0.0365 |
| Singapore, Jakarta, Toronto, Silicon Valley, Virginia | 0.061 |
:::
::: Two-Node Instance
| Region | Price (USD/Core/Hour) |
|---------|---------|
| Chengdu, Chongqing | 0.06 |
| Guangzhou, Shanghai, Beijing, and Nanjing | 0.08 |
| Hong Kong (China), Tokyo, Seoul, Mumbai, Bangkok | 0.099 |
| Frankfurt, São Paulo | 0.073 |
| Singapore, Jakarta, Toronto, Silicon Valley, Virginia | 0.122 |
:::
::: Three-Node Instance
| Region | Price (USD/Core/Hour) |
|---------|---------|
| Chengdu, Chongqing | 0.09 |
| Guangzhou, Shanghai, Beijing, and Nanjing | 0.12 |
| Hong Kong (China), Tokyo, Seoul, Mumbai, Bangkok | 0.1485 |
| Frankfurt, São Paulo | 0.1095 |
| Singapore, Jakarta, Toronto, Silicon Valley, Virginia | 0.183 |
:::
</dx-tabs>

## Feature Impact
Automatic expansion will be performed on the source database and the replica database at the same time. If the source-replica switch is triggered after the expansion of the source database, the replica database will still have the expanded CPU resources. The system will automatically reduce to the original computing specifications when the trigger conditions for reduction are met.
## Automatic Expansion
After **Elastic Performance Management** > **Automatic Expansion** is enabled, when the average CPU utilization of the database instance reaches the set threshold during the observation period, the number of CPU cores will be doubled, for example, from original 4 to new 8, and IOPS will increase by 1000 for each additional CPU core. If there are not enough CPU resources in the host, the expansion will not be performed, and the expansion failure event will be sent immediately.
>?The number of CPU cores can only be doubled based on the original computing specifications and cannot be increased further after the expansion. For example, the number of CPU cores has been expanded to 8 and cannot be increased further to 16.
## Automatic Reduction
After **Elastic Performance Management** > **Automatic Expansion** is enabled, when the CPU utilization is lower than the set threshold during the set observation period of automatic scaling, the system will automatically reduce the number of CPU cores and IOPS to the original computing specifications.
>?After **Elastic Performance Management** > **Automatic Expansion** is enabled, the system will monitor the database instance based on the latest configuration parameters. When the database instance meets the automatic reduction conditions, the system will automatically reduce the specifications of the database instance.

## Enabling Automatic Expansion
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/instance). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance details page.
2. Select **Instance Details** > **Configuration Info** > **Elastic Performance Management**, and click **Configuration**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/zZgw709_2.png)
1 In the elastic performance management window, complete the following configurations, confirm the expansion fee, and click **Expand Now**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/7A5t230_3.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td>Performance Expansion Type</td><td>Select **Automatic Expansion**</td></tr>
<tr>
<td>Automatic CPU Elastic Expansion Threshold</td><td>Set the threshold for automatic elastic expansion triggered by the average CPU utilization. Available options are 70%, 80%, and 90%.</td></tr>
<tr>
<td>Observation Duration</td><td>Set the observation period. Available options are 1 minute, 3 minutes, 5 minutes, 10 minutes, 15 minutes, and 30 minutes. This parameter means that within the specified time period, the system will observe whether the average CPU utilization of the instance reaches the set expansion threshold. If yes, the system will trigger automatic elastic expansion.</td></tr>
<tr>
<td>Elastic CPU Reduction Threshold</td><td>Set the threshold for automatic elastic reduction triggered by the average CPU utilization. Available options are 30%, 20%, and 10%.</td></tr>
<tr>
<td>Observation Duration</td><td>Set the observation period. Available options are 5 minutes, 10 minutes, 15 minutes, and 30 minutes. This parameter means that within the specified time period, the system will observe whether the average CPU utilization of the instance reaches the set reduction threshold. If yes, the system will trigger automatic elastic reduction.</td></tr>
</tbody></table>
4 When the instance status/task changes from **Configuring elastic expansion policy…** to **Running**, automatic expansion is successfully enabled.
>? After automatic expansion is enabled, if you need to modify the elastic performance expansion policy, you can go to **Instance Details** > **Configuration Info** > **Elastic Performance Management** and click **Modify** to reconfigure.
>

## Disabling Automatic Expansion
>?After automatic expansion is disabled, the expanded CPU will be reduced after reaching the automatic reduction threshold, and then will no longer be expanded by the expansion threshold.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/instance). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance details page.
2. Select **Instance Details** > **Configuration Info** > **Elastic Performance Management**, and click **Disable**.
3. Click **OK** in the **Disable CPU Expansion** pop-up window.

## Enabling Manual Expansion
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/instance). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance details page.
2. Select **Instance Details** > **Configuration Info** > **Elastic Performance Management**, and click **Configuration**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/pwSQ074_5.png)
1 In the elastic performance management window, complete the following configurations, confirm the expansion fee, and click **Expand Now**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Qi7e375_6.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td>Performance Expansion Type</td><td>Select **Manual Expansion**</td></tr>
<tr>
<td>Additional CPU Cores</td><td>Set the number of additional CPU cores to be added manually. The upper limit is the number of CPU cores specified by the current specifications. For example, the maximum number of additional CPU cores for 8-core 16 GB MEM is 8.</td></tr>
<tr>
<td>Additional IOPS</td><td>IOPS will increase by 1000 for every additional CPU core.</td></tr>
</tbody></table>
4 When the instance status/task changes from **Configuring elastic expansion policy…** to **Running**, manual expansion is successfully enabled.
>?
>- After manual expansion is enabled, the CPU of the instance will be expanded immediately based on the additional number of CPU cores. On the **Configuration Info** > **Configuration**, you can see the CPU of the current instance.
>Before manual expansion:
>![](https://staticintl.cloudcachetci.com/yehe/backend-news/QdUb025_7.png)
>After manual expansion:
>![](https://staticintl.cloudcachetci.com/yehe/backend-news/xk9U552_8.png)
>- After enabling manual expansion, if you need to modify the number of additional CPU cores, you can go to **Instance Details** > **Configuration Info** > **Elastic Performance Management** and click **Modify** to reconfigure.
>![](https://staticintl.cloudcachetci.com/yehe/backend-news/HeZm869_9.png)

## Disabling Manual Expansion
>?After manual expansion is disabled, the expanded CPU will be reduced to the specifications before expansion.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/instance). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance details page.
2. Select **Instance Details** > **Configuration Info** > **Elastic Performance Management**, and click **Disable**.
3. Click **OK** in the **Disable CPU Expansion** pop-up window.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/63Te178_10.png)
