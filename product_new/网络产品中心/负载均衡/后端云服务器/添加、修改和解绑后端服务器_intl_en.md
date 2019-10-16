CLB routes requests to real servers’ that are running normally. This document describes how to add or delete real servers when you use CLB for the first time or based on your business needs.

>- Unbinding a real server will unbind the CLB instance from the CVM instance, and the CLB instance will stop forwarding requests to it immediately.
>- Unbinding a real server will not affect the lifecycle of your CVM instance. You can add it again to the real server cluster if necessary.
>- If a CLB instance is associated with an auto scaling group, the CVM instances in the group will be automatically added to the real server of the CLB instance, and when a CVM instance is removed from the scaling group, it will be automatically deleted from the real server of the CLB instance.

## CLB
### Adding a Real Server to a CLB Instance
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. In the listener corresponding to the CLB instance, add a real server.
 - **TCP/UDP listener**
 When adding a real server, select the listener to be bound to in the left column and click **Bind**. Read the following instruction on the operating details.
![](https://main.qcloudimg.com/raw/64a10e9154b135dfd37e74365cbd4442.png)
 - **HTTP/HTTPS Listener**
 When adding a real server, select the listener and rule to be bound to in the left column and click **Bind**. Read the following instruction on the operating details.
![](https://main.qcloudimg.com/raw/347bc0cbe6afa7314ac7572d8722d145.png)
3. In the pop-up window, select the target CVM instance, enter the port and weight, and click **OK**.
> The pop-up window only displays available CVM instances in the same region and same network environment that are not isolated and have not expired with peak bandwidth greater than 0.

 ![](https://main.qcloudimg.com/raw/99ff99e6001cab18a259f5147df5fcbe.png)
4. If the CVM instances that need to be bound in batches have the same preset port value, enter the preset port value into the "Default Port" field, select the corresponding CVM instances, set the weights, and click **OK** to bind them in batches.
![](https://main.qcloudimg.com/raw/7c2191001d1edb0b66e4251c55179aea.png)

> If you need to call APIs for real server addition, see [RegisterInstancesWithLoadBalancer API](https://intl.cloud.tencent.com/doc/api/244/1265).

### Modifying Real Server Weight for a CLB Instance
The real server weight determines the number of CVM requests to be forwarded. When binding a real server, you need to preset its weight. To modify the weight afterwards, refer to the steps below. For more information on CLB real server weight, see [CLB Polling Method](http://intl.cloud.tencent.com/document/product/214/6153).
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. Select the instance and listener rule, select the corresponding CVM in the server list, click **Edit**, enter the new weight, and click **Submit**.
3. To modify the weights in batches, select all relevant CVM instances, click **Modify Weight**, enter the new weight, and then click **Submit**.
![](https://main.qcloudimg.com/raw/e08f226ba159369524c098f285768717.png)

> If you need to call APIs for real server weights modification, see [ModifyLoadBalancerBackends API](https://intl.cloud.tencent.com/doc/api/244/1264).

### Modifying Real Server Port for a CLB Instance
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. Select the instance and listener rule, select the corresponding CVM in the CVM instance list, click **Edit**, enter the new port, and click **Submit**.
3. To modify the ports in batches, select all relevant CVMs, click **Modify Port**, enter the new port, and then click **Submit**.
![](https://main.qcloudimg.com/raw/c1fe26d1bcd8ecdfa69349c2ed985c6c.png)

### Unbinding a Real Server from a CLB Instance
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. Select the listener and rule, select the target CVM instance in the CVM instance list on the right, click **Unbind**, and then click **Submit** in the pop-up window.
3. To unbind CVM instances in batches, select all target CVM instances, click **Unbind**, and then click **Submit** in the pop-up window.
![](https://main.qcloudimg.com/raw/6bf6671605ce6e04387bb54bc573e348.png)

## Classic CLB
### Adding a Real Server to a CLB Instance
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. For Classic CLB, you need to specify the real server port during **listener creation** phrase. Click **Create**, enter the port value in the "Backend Port" field, and then click **Next**.
![](https://main.qcloudimg.com/raw/f8f36253ef0c86108a189180c4a9b5a8.png)
3. Click **Bind**, select the target CVM instance, enter the weight, and click **OK** to bind it (the pop-up window only displays available CVM instances with peak bandwidth greater than 0, in the same region, same network environment that are not isolated nor expired).
 ![](https://main.qcloudimg.com/raw/a285308e527df5c435fcdc1c949313a3.png)
### Modifying Real Server Weight for a CLB Instance
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. Select the corresponding CVM instance in the CVM instance list, under the listener, click **Edit**, enter the new weight, and click **Submit** to modify the CVM instance weight.
3. To modify the weights in batches, select all relevant CVM instances, click **Modify Weight**, enter the new weight, and then click **Submit**.
![](https://main.qcloudimg.com/raw/5311658177f3302780f62a50718007cc.png)

> Currently, real server weight cannot be modified through APIs.

### Unbinding a Real Server from a CLB Instance
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. Select the target CVM in the instance list under the listener list, click **Unbind**, and click **Submit** in the pop-up window.
3. To unbind CVM instances in batches, select all target CVMs, click **Unbind**, and then click **Submit** in the pop-up window.
![](https://main.qcloudimg.com/raw/0d84fadaaf9dc0ac4310c0e0ba6a1bac.png)
