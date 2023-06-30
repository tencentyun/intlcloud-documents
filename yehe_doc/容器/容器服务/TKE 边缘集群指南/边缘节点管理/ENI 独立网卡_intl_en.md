## Overview
If you add Tencent Cloud CVMs to the edge cluster as edge nodes, the platform allows you to enable ENIs and bind Pods on CVM nodes with independent ENIs to implement a high-availability network scheme.

The network architecture is as follows:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/jHRv177_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221213174629.png)

You can also use ENIs in the VPC where the CVMs reside to open Pods to external users and then bind different ENIs to the CLB to enable high-performance network forwarding.

- [Enabling the independent ENI](#openEniNetwork)
- [Disabling the independent ENI](#closeEniNetwork)


## Directions
[](id:openEniNetwork)
### Enabling the independent ENI
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. On the **Cluster Management** page, click the ID of the target cluster to enter its details page.
3. Select **Add-On Management** on the left of the page and click **Create** on the add-on list page.
4. On the **Create Add-On** page, select **EniNetwork (independent ENI add-on)** and click **Parameter Configurations** as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/u4y5540_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221215152903.png)
   - 4.1 In the **Independent ENI parameter settings** pop-up window, click **Access API key** to enter the key information page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/NLLQ837_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221215153236.png)
   - 4.2 Create a key and copy the `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
   - 4.3 In the **Independent ENI parameter settings** pop-up window, enter `SecretId` and `SecretKey` and click **Confirm**.
5. On the **Create Add-On** page, click **Done** to enable the ENI.
6. Select **Workload** > **Deployment** on the left of the page to enter the Deployment list page. If there is already a Deployment in the list, skip this step; otherwise, create one as instructed in [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662).
7. Select **Node Management** > **Node** on the left of the page to enter the node list page. If there is already a CVM node in the list, skip this step; otherwise, create one.
8. Configure the ENI in the Pod of the target edge cluster.
   - The configuration is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/28b00f69d3aa4247102fa7b8e03cd72a.png)
   - The ENI capability of edge clusters is supported only by Tencent Cloud CVM node resources. Therefore, when deploying an application, you need to use the `nodeAffinity` capability to schedule the Pod mounted with the ENI to the real CVM edge node (you can enter multiple CVM node IDs).
![](https://qcloudimg.tencent-cloud.cn/raw/38e0083ed702a65a2d95b9619364fc58.png)
   - Below is the actual code:
    ```
      template:
        metadata:
          annotations:
            tke.cloud.tencent.com/networks: tke-direct-eni,flannel
    ```
		```
   	 spec:
   	   affinity:
   	     nodeAffinity:
   	       requiredDuringSchedulingIgnoredDuringExecution:
   	         nodeSelectorTerms:
   	         - matchExpressions:
   	           - key: kubernetes.io/hostname
   	             operator: In
   	             values:
   	             - cvm-2cxgi4ow # CVM node ID of the access target
    ```
   

[](id:closeEniNetwork)
### Disabling the independent ENI
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. On the cluster management page, click the target cluster ID to enter its details page.
3. Select **Add-On Management** on the left of the page and click **Delete** on the right of the target add-on on the add-on list page.
4. In the **Delete Resource** pop-up window, click **Confirm**.
