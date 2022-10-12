## Overview
This document describes how to enable and bind ENI to Pods on CVM edge nodes to implement a high-availability network scheme.

- [Enabling ENI](#openEniNetwork)
- [Disabling ENI](#closeEniNetwork)



## Directions
[](id:openEniNetwork)
### Enabling ENI
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **Edge Clusters** on the left sidebar.
2. Click the ID of the target cluster to enter its details page.
3. Select **Basic Information** on the left to enter the **Basic Information** page of the cluster and toggle on the **Enable ENI** switch. The detailed directions are as follows:
      - 3.1 Click the **Access API key** hyperlink to enter the key information page.
      - 3.2 Copy the `ID` and `Key`, return to the **Confirm Key Information** pop-up window, and enter the information.
            ![](https://qcloudimg.tencent-cloud.cn/raw/ca8a929b58a5a2a71cf9ac5296682ec8.png)
      - 3.3 Click **OK**.
4. Select **Workload** > **Deployment** on the left to enter the Deployment list page. If Deployments exist in the list, skip this step; otherwise, create a Deployment as instructed in [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662).
5. Select **Node Management** > **Node** on the left to enter the node list page. If CVM nodes exist in the list, skip this step; otherwise, create a CVM node as instructed in [Node Management](https://intl.cloud.tencent.com/document/product/457/35386).
6. Configure the ENI in the Pods in the edge cluster.
   - The configuration is as follows:
    ![](https://qcloudimg.tencent-cloud.cn/raw/28b00f69d3aa4247102fa7b8e03cd72a.png)
   - The ENI capability of edge clusters is supported only by Tencent Cloud CVM node resources. Therefore, when deploying an application, you need to use the `nodeAffinity` capability to schedule the Pod mounted with the ENI to the real CVM edge node (you can enter multiple CVM node IDs).
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
### Disabling ENI
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **Edge Clusters** on the left sidebar.
2. Click the ID of the target cluster to enter its details page.
3. Select **Basic Information** on the left to enter the **Basic Information** page of the cluster and toggle off the **Enable ENI** switch.
    
