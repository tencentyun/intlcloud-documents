<dx-alert infotype="alarm" title="Note">
Tencent Prometheus Service (TPS) has been integrated into [TMP](https://intl.cloud.tencent.com/document/product/457/46734), which supports cross-region monitoring in multiple VPCs, and provides a unified Grafana dashboard, allowing for checking of multiple monitoring instances. For more information on TMP billing, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156). For cloud resource usage details, see [Billing Mode and Resource Usage](https://intl.cloud.tencent.com/document/product/457/46733). [Free metrics](https://intl.cloud.tencent.com/document/product/457/46735) for basic monitoring will not be billed.<br>
TPS is discontinued from May 16, 2022 (UTC +8). For more information, see [Announcement](https://intl.cloud.tencent.com/document/product/457/46999). Click [here](https://console.cloud.tencent.com/tke2/prometheus2) to try out TMP. TPS instances can no longer be created, but you can use our quick [migration tool](https://intl.cloud.tencent.com/document/product/457/46736) to migrate your TPS instances to TMP. Before the migration, [streamline monitoring metrics](https://intl.cloud.tencent.com/document/product/457/46737) or reduce the collection frequency; otherwise, higher costs may be incurred.
</dx-alert>

TPS is currently in free beta test. When you use TPS, storage resources such as [COS](https://intl.cloud.tencent.com/document/product/436) and [CBS](https://intl.cloud.tencent.com/document/product/362), as well as public and private network [CLB](https://intl.cloud.tencent.com/document/product/214) resources will be created in your account and billed based on the actual usage. This document describes these resources and their billing methods.




## Resource List

### COS

The COS will be enabled in your account for persistent storage of metrics when a TPS instance is created. You can view the resource information in the [COS console](https://console.cloud.tencent.com/cos5).
![](https://qcloudimg.tencent-cloud.cn/raw/d904bacf9d372551db5732d92fa9092a.png)

This resource is billed based on the actual storage volume and period, which is defined by you at the time of instance creation. For more information about billing for COS, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/436/32534).

### CBS

Five Premium Cloud Storage will be purchased in your account for temporary storage of metrics when a TPS instance is created. You can view the information about CBS resource and specification in the [CBS console](https://console.cloud.tencent.com/cvm/cbs/index?rid=1).
![](https://qcloudimg.tencent-cloud.cn/raw/6137e43b4ed152234a41bfdaca6c0df3.png)

Where:
- Specification of the CBS used for Grafana is 10 GB.
- Specification of the CBS used for Thanos Rule component is 50 GB.
- Specification of the CBS used for Thanos Store component is 200 GB.
- Specification of the CBS used for AlertManager is 10 GB.
- Specification of the CBS used for Prometheus is varied depending on the actual metrics. 10 GB is used for about 30w series (about 30 nodes).

This resource is billed based on the actual usage. For billing details of CBS, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).


### CLB

Two private network LBs will be created in your account when a TPS instance is created. One LB will be added when one more cluster is associated. If you want to access Grafana via the public network, you need to create a corresponding public network LB. This resource is charged. You can view the information about the LBs in the [CLB console](https://console.cloud.tencent.com/clb/instance?rid=1).
![](https://qcloudimg.tencent-cloud.cn/raw/37c899f564ca3fb9710402692e9f1425.png)

This resource is billed based on the actual usage. For billing details of CLB, see [Billing for Standard Account](https://intl.cloud.tencent.com/document/product/214/36998).



## Resource Termination

You cannot delete these resources in the corresponding consoles. You need to terminate the TPS instances in the [TPS console](https://console.cloud.tencent.com/tke2/prometheus/list?rid=1) to terminate all these resources. Tencent Cloud does not repossess TPS instances proactively. If you do not use TPS anymore, you need to delete the TPS instances immediately to avoid additional charges.

