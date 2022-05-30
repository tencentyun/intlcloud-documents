<dx-alert infotype="alarm" title="Note">
Tencent Prometheus Service (TPS) has been integrated into [TMP](https://intl.cloud.tencent.com/document/product/457/46734), which supports cross-region monitoring in multiple VPCs, and provides a unified Grafana dashboard, allowing for checking of multiple monitoring instances. For more information on TMP billing, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156). For cloud resource usage details, see [Billing Mode and Resource Usage](https://intl.cloud.tencent.com/document/product/457/46733). [Free metrics](https://intl.cloud.tencent.com/document/product/457/46735) for basic monitoring will not be billed.<br>
TPS will be discontinued soon. Click [here](https://console.cloud.tencent.com/tke2/prometheus2) to try out TMP. TPS instances can no longer be created, but you can use our quick [migration tool](https://intl.cloud.tencent.com/document/product/457/46736) to migrate your TPS instances to TMP. Before the migration, [streamline monitoring metrics](https://intl.cloud.tencent.com/document/product/457/46737) or reduce the collection frequency; otherwise, higher costs may be incurred.
</dx-alert>

TPS supports quick migration to TMP, where you can migrate a single instance or a batch of instances in the same region. In general, it takes about ten minutes to migrate a TPS instance. **The new TMP instance will be named "old instance name (trans-from-prom-xxx)", where "old instance name" is the TPS instance name and "xxx" is the TPS instance ID.** After the migration, you can view new monitoring data in the TMP instance and previous monitoring data in the TPS instance. Note that the TPS instance will be deleted upon the end of service.




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

If you have application platform or systems that depend on TPS' **Prometheus data query address and Grafana address**, replace them with the appropriate addresses in TMP promptly after the migration. Otherwise, your **Prometheus data query address and Grafana address** will become invalid when the TPS instance is deleted upon the end of service.

#### (Old) TPS Prometheus data query address and Grafana address 
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **[Cloud Native Monitoring](https://console.cloud.tencent.com/tke2/prometheus)** in the left sidebar.
2. Click the ID of an instance to enter its **Basic information** page.
![](https://qcloudimg.tencent-cloud.cn/raw/b5b9fc3ef9f9e60c952433dba3bbc7ba.png)

#### (New) TMP Prometheus data query address and Grafana address 
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **[TMP](https://console.cloud.tencent.com/tke2/prometheus2)** in the left sidebar.
2. Click the ID of an instance to enter its **Basic information** page.
![](https://qcloudimg.tencent-cloud.cn/raw/90393196785809a05e85dcb5ac172b24.png)

>? After the migration is completed, do not associate new clusters or collection rules with the TPS instance, as the association will not be automatically synced to the TMP instance.

## Directions

### Migrating a single instance

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **[Cloud Native Monitoring](https://console.cloud.tencent.com/tke2/prometheus)** in the left sidebar.
2. On the instance list page, select the region where the instance to be migrated resides.
3. Click **Quick migration** on the right of the instance.
4. In the pop-up window, select the **Network** and **Data storage time** required for the TMP instance.
	- **Network**: The TMP instance has the same VPC and subnet as the TPS instance by default. If you want to select another VPC, make sure that the target VPC is connected to the VPC where the monitored cluster resides.
	- **Data storage time**: 15 days by default.
>! See [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156) and [Cloud Resource Usage](https://intl.cloud.tencent.com/document/product/457/46733) for TMP billing. If costs are too high, we recommend you [streamline monitoring metrics](https://intl.cloud.tencent.com/document/product/457/46737).
>
5. Click **OK**. The migration is successful when the TPS instance status changes to **Migrated**.
6. After the TPS migration is completed, the **[TMP](https://console.cloud.tencent.com/tke2/prometheus)** console will display **a new TMP instance named "old instance name (trans-from-prom-xxx)" in the same region, where "old instance name" is the TPS instance name and "xxx" is the TPS instance ID**. 
>? After the migration is completed, do not associate new clusters or collection rules with the TPS instance, as the association will not be automatically synced to the TMP instance.

### Batch migrating instances

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **[Cloud Native Monitoring](https://console.cloud.tencent.com/tke2/prometheus)** in the left sidebar.
2. On the instance list page, select the region where the instances to be migrated reside.
3. Select the instances in the **Not migrated** status and click **Quick migration** on the top.
>! 
>- You cannot specify the VPC and subnet for TMP instances if you choose batch migration. Choose **single instance migration** if needed.
>! See [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156) and [Cloud Resource Usage](https://intl.cloud.tencent.com/document/product/457/46733) for TMP billing. If costs are too high, we recommend you [streamline monitoring metrics](https://intl.cloud.tencent.com/document/product/457/46737).
4. Click **OK**. The migration is successful when the TPS instance status changes to **Migrated**.
5. After the TPS migration is completed, the **[TMP](https://console.cloud.tencent.com/tke2/prometheus)** console will display **new TMP instances named "old instance name (trans-from-prom-xxx)" in the same region, where "old instance name" is the TPS instance name and "xxx" is the TPS instance ID**.
>? After the migration is completed, do not associate new clusters or collection rules with the TPS instance, as the association will not be automatically synced to the TMP instance.
