### qGPU overview

qGPU is a GPU sharing technology launched by Tencent Cloud. It can share a GPU card among multiple containers and isolate the vRAM and computing resources among containers. In this way, it ensures business security by using GPU cards at a smaller granularity to increase GPU utilization and reduce costs.
Based on TKE's open-source Nano GPU framework, qGPU can schedule GPU computing power and vRAM at a fine granularity, share a GPU card among multiple containers, and allocate GPU resources across GPU cards. Plus, relying on the powerful underlying isolation technology, it can strongly isolate vRAM and computing power to ensure that business performance and resource use are not affected by GPU sharing.

>? qGPU is currently in beta test. To try it out, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder).

### Solution framework diagram

![](https://qcloudimg.tencent-cloud.cn/raw/671b1e90838586feaeccbbfdf6ed8507.png)
