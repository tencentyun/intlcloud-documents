## Overview
If you add Tencent Cloud CVMs to the edge cluster as edge nodes, the platform allows you to enable ENIs and bind Pods on CVM nodes with independent ENIs to implement a high-availability network scheme.

The network architecture is as follows:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/jHRv177_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221213174629.png)

You can also use ENIs in the VPC where the CVMs reside to open Pods to external users and then bind different ENIs to the CLB to enable high-performance network forwarding.

- [Enabling ENI](#openEniNetwork)
- [Disabling ENI](#closeEniNetwork)


## Directions
[](id:openEniNetwork)
### Enabling ENI
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. On the **Cluster Management** page, click the ID of the target cluster to enter its details page.
3. Select **Basic Information** on the left to enter the **Basic Information** page of the cluster and toggle on the **Enable ENI** switch. The detailed directions are as follows:
      - 3.1 Click **Access API key** to enter the key information page.
- 3.2 Create a key and copy the `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
      - 3.3 In the pop-up window for key information confirmation, click **OK**.
       
4. Select **Workload** > **Deployment** on the left to enter the Deployment list page. If Deployments exist in the list, skip this step; otherwise, create a Deployment as instructed in [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662).
5. Choose **Node Management** > **Node** in the left sidebar to go to the node list page. If the CVM nodes already exist in the node, skip this step. Otherwise, create the CVM nodes.
6. Configure the ENI in the Pods in the edge cluster.
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
   
    ```

[](id:closeEniNetwork)
### Disabling ENI
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. On the **Cluster Management** page, click the ID of the target cluster to enter its details page.
3. Select **Basic Information** on the left to enter the **Basic Information** page of the cluster and toggle off the **Enable ENI** switch.
