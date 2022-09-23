<dx-alert infotype="alarm" title="Note">
To provide better and more powerful product capabilities, TPS will be merged and upgraded into [Tencent Managed Service for Prometheus (TMP)](https://intl.cloud.tencent.com/document/product/457/46734). The new TMP service supports cross-region and cross-VPC monitoring and connecting a unified Grafana dashboard to multiple TMP instances for data display in one place. For more information on TMP billing, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156). For Tencent Cloud resource usage details, see [Billing Mode and Resource Usage](https://intl.cloud.tencent.com/document/product/457/46733). [Free metrics](https://intl.cloud.tencent.com/document/product/457/46735) for basic monitoring will not be billed.<br>
TPS will be deactivated on May 16, 2022. For more information, see [Announcements](https://intl.cloud.tencent.com/document/product/457/46999). Click [here](https://console.cloud.tencent.com/tke2/prometheus2) to try out the launched TMP service. TPS instances can no longer be created. You can use our quick [migration tool](https://intl.cloud.tencent.com/document/product/457/46736) to migrate your TPS instances to TMP. Before the migration, [streamline monitoring metrics](https://intl.cloud.tencent.com/document/product/457/46737) or reduce the collection frequency first; otherwise, higher costs may be incurred.
</dx-alert>

TPS supports quick migration to TMP, where you can migrate a single instance or a batch of instances in the same region. In general, it takes about ten minutes to migrate a TPS instance. **The new TMP instance will be named "old instance name (trans-from-prom-xxx)", where the "old instance name" is the TPS instance name and "xxx" is the TPS instance ID.** After the migration, you can view new monitoring data in the TMP instance and previous monitoring data in the TPS instance. Note that the TPS instance will be deleted upon the end of service.




The migration steps are as follows:
<dx-steps>
- Migrate the Grafana configuration.
- Create a Grafana instance.
- Create a TMP instance.
- Bind the TMP instance to the cluster associated with the TPS instance.
- Migrate the collection configuration.
- Migrate the alarm policy.
- Migrate the aggregation rule.
</dx-steps>

## Migration Notes

### Estimated costs after migration

The capability of **Billable Metric Collection Rate** has been launched for TPS and TMP, which helps you estimate the cost of monitoring by instance, cluster, target, and metric.

>! Costs will be incurred by TMP instances but not TPS instances.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **[Cloud Native Monitoring](https://console.cloud.tencent.com/tke2/prometheus)** on the left sidebar.
2. In the cloud native monitoring list, view the **Billable Metric Collection Rate**, which indicates the collection rate of billable metrics for migration to the TMP instance and is estimated based on your reported metric data volume and the collection frequency. This value multiplied by 86400 is the number of monitoring data points per day, and you can calculate the estimated published price as instructed in [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156).
You can also click **Quick Migration** on the right of the instance name to get the estimated price after a TPS instance is migrated to TMP. Or you can view the **Billable Metric Collection Rate** under different dimensions on various pages such as **Associate with Cluster**, **Data Collection Configuration**, and **Metric Details**.

### (Old) TPS' Prometheus data query address and Grafana address 

If you have application platforms or systems that depend on TPS' **Prometheus data query address and Grafana address**, replace them with the appropriate addresses in TMP promptly after the migration; otherwise, your **Prometheus data query address and Grafana address** will become invalid after the TPS instance is deleted upon the end of service.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **[Cloud Native Monitoring](https://console.cloud.tencent.com/tke2/prometheus)** on the left sidebar.
2. Click the ID of an instance to enter its **Basic Information** page.
![](https://qcloudimg.tencent-cloud.cn/raw/51f5fca693243b3f3ceb458c1294d72e.png)

### (New) TMP's Prometheus data query address and Grafana address 

>? TMP adds authentication to the query API. If you need to connect a TMP instance to your Grafana, use your Tencent Cloud account `APPID` as the username and the token below as the password. For more information, see [Querying Monitoring Data](https://intl.cloud.tencent.com/document/product/1116/43212).

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **[TMP](https://console.cloud.tencent.com/tke2/prometheus2)** on the left sidebar.
2. Click the ID of an instance to enter its **Basic Information** page.
![](https://qcloudimg.tencent-cloud.cn/raw/d4aa6a7a957a2cf9ef3e4ec851b4a1bb.png)

>! After the migration is completed, do not associate new clusters or collection rules with the old TPS instance, as these changes will not be automatically synced to the TMP instance.

## Directions

### Single instance migration

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **[Cloud Native Monitoring](https://console.cloud.tencent.com/tke2/prometheus)** on the left sidebar.
2. On the instance list page, select the region where the instance to be migrated resides.
3. Click **Quick Migration** on the right of the instance.
4. In the pop-up window, select the **Network** and **Data Storage Time** required for the TMP instance.
   - **Network**: The TMP instance has the same VPC and subnet as the TPS instance by default. If you want to select another VPC, make sure that the target VPC is connected to the VPC of the monitored cluster.
   - **Data Storage Time**: **15 days** by default. You can also select **30 days** or **45 days**.
   - **Tag**: Not required. You can select one as needed.
   - **Estimated Cost**: During the migration from the current TPS instance to TMP, it displays the **Billable Metric Collection Rate** and estimated daily cost that will take effect after the successful migration.

>! For more information on TMP billing, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156) and [Tencent Cloud Resource Usage](https://intl.cloud.tencent.com/document/product/457/46733). If the costs are too high, we recommend you [streamline monitoring metrics](https://intl.cloud.tencent.com/document/product/457/46737).
5. Click **OK**. The migration is successful when the TPS instance status changes to **Migrated**.
6. After the TPS migration is completed, the **[TMP console](https://console.cloud.tencent.com/tke2/prometheus)** will display **a new TMP instance named "old instance name (trans-from-xxx)" in the same region, where the "old instance name" is the TPS instance name and "xxx" is the TPS instance ID.** 
>? After the migration is completed, do not associate new clusters or collection rules with the TPS instance, as the association will not be automatically synced to the TMP instance.

### Batch instance migration

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **[Cloud Native Monitoring](https://console.cloud.tencent.com/tke2/prometheus)** on the left sidebar.
2. On the instance list page, select the region where the instances to be migrated reside.
3. Select the instances in the **Not migrated** status and click **Quick Migration** at the top.
>! 
>- You cannot specify the VPC or subnet for TMP instances if you select batch migration. If it is necessary, perform **single instance migration**.
>- Before the migration, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156) and [Tencent Cloud Resource Usage](https://intl.cloud.tencent.com/document/product/457/46733) for TMP billing. If the costs are too high, we recommend you [streamline monitoring metrics](https://intl.cloud.tencent.com/document/product/457/46737).
4. Click **OK**. The migration is successful when the TPS instance status changes to **Migrated**.
5. After the TPS migration is completed, the **[TMP](https://console.cloud.tencent.com/tke2/prometheus)** console will display **a new TMP instance named "old instance name (trans-from-xxx)" in the same region, where the "old instance name" is the TPS instance name, and "xxx" is the TPS instance ID.**

>? After the migration is completed, do not associate new clusters or collection rules with the TPS instance, as the association will not be automatically synced to the TMP instance.
