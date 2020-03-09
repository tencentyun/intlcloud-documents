CLB routes requests to real server instances that are running normally. This document describes how to add or delete real servers as needed or when you use CLB for the first time.

>
>- Unbinding a real server will unbind the CLB instance from the CVM instance, and CLB will immediately stop forwarding requests to it.
>- Unbinding a real server will not affect the lifecycle of your CVM instance, which can also be added to the real server cluster again.
>- If a CLB instance is associated with an auto scaling group, CVMs in the group will be automatically added to the real servers of CLB. When a CVM instance is removed from the auto scaling group, it will be automatically deleted from the real servers of CLB.

## CLB
### Adding a real server to CLB
1. Log into the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. In the listener corresponding to the CLB instance, add a real server.
 - **TCP/UDP listener**
 When adding a real server, select the listener to be bound in the left column and click **Bind**. Read the following instruction for operating details.
![](https://main.qcloudimg.com/raw/64a10e9154b135dfd37e74365cbd4442.png)
 - **HTTP/HTTPS listener**
 When adding a real server, select the listener and rule to be bound in the left column and click **Bind**. Read the following instruction for operating details.
![](https://main.qcloudimg.com/raw/347bc0cbe6afa7314ac7572d8722d145.png)
3. In the pop-up window, select the CVM to be bound, enter the port and weight, and click **OK**.
>The pop-up window only displays available CVMs that are not isolated nor expired, in the same region, in the same network environment, and have peak bandwidth greater than 0.
>
 ![](https://main.qcloudimg.com/raw/99ff99e6001cab18a259f5147df5fcbe.png)
4. To bind CVMs that have the same preset port value in batches, enter the preset port value in the "Default Port" field, select the corresponding CVMs, configure the weights, and click **OK** to bind them in batches.
![](https://main.qcloudimg.com/raw/7c2191001d1edb0b66e4251c55179aea.png)
>If you need to use API to add real servers, please see [RegisterInstancesWithLoadBalancer API](https://intl.cloud.tencent.com/document/api/214/1265).

### Modifying real server weights for CLB
The real server weight determines the number of CVM requests to be forwarded. When binding a real server, you need to preset its weight. To modify the weight, refer to the steps below. For more information on CLB real server weight, please see [CLB Polling Method](/doc/product/214/6153).
1. Log into the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. Select the instance and listener rule, select the corresponding CVM from the list, click **Edit**, enter the new weight, and click **Submit** to modify the weight of the CVM.
3. To modify the weight in batches, select all relevant CVMs, click **Modify Weight**, enter the new weight, and then click **Submit**.
![](https://main.qcloudimg.com/raw/e08f226ba159369524c098f285768717.png)

>If you need to use an API to modify real server weights, please see [ModifyLoadBalancerBackends API](https://intl.cloud.tencent.com/document/api/214/1264).

### Modifying real server ports for CLB
1. Log into the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. Select the instance and listener rule, select the corresponding CVM from the list, click **Edit**, enter the new port, and click **Submit** to modify the port of the CVM.
3. To modify the port in batches, select all relevant CVMs, click **Modify Port**, enter the new port, and then click **Submit**.
![](https://main.qcloudimg.com/raw/c1fe26d1bcd8ecdfa69349c2ed985c6c.png)

>If you need to use API to modify real server ports, please see [ModifyTargetPort](https://intl.cloud.tencent.com/document/product/214/33812).

### Unbinding real servers from CLB
1. Log into the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. Select the listener and rule, select from the list on the right the CVM to be unbound, click **Unbind**, and then click **Submit** in the pop-up window.
3. To unbind CVM instances in batches, select all CVMs to be unbound, click **Unbind**, and then click **Submit** in the pop-up window.
![](https://main.qcloudimg.com/raw/6bf6671605ce6e04387bb54bc573e348.png)

>If you need to use API to unbind real servers, please see [DeregisterTargets API](https://intl.cloud.tencent.com/document/product/214/33832).

## Classic CLB
### Adding a real server to CLB
1. Log into the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. For classic CLB, you need to specify the real server port during **listener creation**. Click **Create**, enter the port value in the "Backend Port" field, and then click **Next**.
![](https://main.qcloudimg.com/raw/f8f36253ef0c86108a189180c4a9b5a8.png)
3. Click **Bind**, select the CVMs to be bound, enter the weights, and click **OK** (the pop-up window only displays available CVM instances that are not isolated nor expired, in the same region, in the same network environment, and have peak bandwidth greater than 0).
![](https://main.qcloudimg.com/raw/a285308e527df5c435fcdc1c949313a3.png)
 
>If you need to use an API to add a real server, please see [RegisterTargetsWithClassicalLB API](https://intl.cloud.tencent.com/document/product/214/33802).

### Modifying real server weights for CLB
1. Log into the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. Select the corresponding CVM from the list below the listener, click **Modify Weight**, enter the new weight, and click **Submit** to modify the weight of the CVM.
3. To modify the weight in batches, select all relevant CVMs, click **Modify Weight**, enter the new weight, and then click **Submit**.
![](https://main.qcloudimg.com/raw/5311658177f3302780f62a50718007cc.png)

>Currently, real server weight cannot be modified via APIs.

### Unbinding real servers from CLB
1. Log into the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. Select the corresponding CVMs from the list below the listener, click **Unbind**, and click **Submit** in the pop-up window.
3. To unbind CVMs in batches, select all CVMs to be unbound, click **Unbind**, and then click **Submit** in the pop-up window.
![](https://main.qcloudimg.com/raw/0d84fadaaf9dc0ac4310c0e0ba6a1bac.png)

>If you need to use API to unbind real servers, please see [DeregisterTargetsFromClassicalLB API](https://intl.cloud.tencent.com/document/product/214/33807).
