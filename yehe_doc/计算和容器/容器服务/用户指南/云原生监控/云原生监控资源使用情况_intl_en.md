

<dx-alert infotype="alarm" title="Note">
Tencent Prometheus Service (TPS) has been integrated into TMP, which supports cross-region monitoring in multiple VPCs, and provides a unified Grafana dashboard, allowing for checking of multiple monitoring instances. For more information on TMP billing, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/1116/43156).<br>
Click [here](https://console.cloud.tencent.com/tke2/prometheus2) to try out TMP. We will provide a **quick migration tool** to help you migrate your TPS instances to TMP. We will inform you of the TPS deactivation time and migration tool launch time via Message Center.
</dx-alert>


Currently, Tencent Prometheus Service is in beta test and free of charge. When you use Tencent Prometheus Service, storage resources such as [COS](https://intl.cloud.tencent.com/zh/document/product/436) and [CBS](https://intl.cloud.tencent.com/zh/document/product/362), as well as public and private network [CLB](https://intl.cloud.tencent.com/zh/document/product/214) resources will be created in your account and billed based on the actual usage. This document describes these resources and their billing methods.




## Resource List

### COS

The COS will be enabled in your account for persistent storage of metrics when a PROM instance is created. You can view the resource information in the [COS console](https://console.cloud.tencent.com/cos5).
![](https://qcloudimg.tencent-cloud.cn/raw/d904bacf9d372551db5732d92fa9092a.png)

This resource is billed based on the actual storage volume and period, which is defined by you at the time of instance creation. For more information about billing for COS, see [Pay-as-You-Go](https://intl.cloud.tencent.com/document/product/436/32534).

### CBS

Five Premium Cloud Storage will be purchased in your account for temporary storage of metrics when a PROM instance is created. You can view the information about CBS resource and specification in the [CBS console](https://console.cloud.tencent.com/cvm/cbs/index?rid=1).
![](https://qcloudimg.tencent-cloud.cn/raw/6137e43b4ed152234a41bfdaca6c0df3.png)

Where:
- Specification of the CBS used for Grafana is 10 GB.
- Specification of the CBS used for Thanos Rule component is 50 GB.
- Specification of the CBS used for Thanos Store component is 200 GB.
- Specification of the CBS used for AlertManager is 10 GB.
- Specification of the CBS used for Prometheus is varied depending on the actual metrics. 10 GB is used for about 30w series (about 30 nodes).

This resource is billed based on the actual usage. For billing details of CBS, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).


### CLB

Two private network LBs will be created in your account when a PROM instance is created. One LB will be added when one more cluster is associated. If you want to access Grafana via public network, you need to create a corresponding public network LB. This resource is charged. You can view the information about the LBs in the [CLB console](https://console.cloud.tencent.com/clb/instance?rid=1).
![](https://qcloudimg.tencent-cloud.cn/raw/37c899f564ca3fb9710402692e9f1425.png)

This resource is billed based on the actual usage. For billing details of CLB, see [Billing for Standard Account](https://intl.cloud.tencent.com/document/product/214/36998).



## Resource Termination

You cannot delete these resources in the corresponding consoles for now. You need to terminate the PROM instance in the [TPS console](https://console.cloud.tencent.com/tke2/prometheus/list?rid=1) to terminate all these resources. Tencent Cloud does not repossess PROM instances proactively. If you do not use Tencent Prometheus Service, you need to delete the PROM instances immediately to avoid additional charges.

