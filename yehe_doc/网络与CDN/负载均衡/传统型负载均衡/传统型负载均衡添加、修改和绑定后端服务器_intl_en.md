Classic CLB routes requests to real server instances that are running normally. This document describes how to add or delete real servers as needed or when you use Classic CLB for the first time.
## Prerequisites
You have created a Classic CLB instance and configured a listener. For more information, please see [Getting Started with Classic CLB](https://intl.cloud.tencent.com/document/product/214/6574).
## Directions
### Adding real server to Classic CLB instance
>?
>- If a Classic CLB instance is associated with an auto scaling group, CVM instances in the group will be automatically added to the real servers of the Classic CLB instance. When a CVM instance is removed from the auto scaling group, it will be automatically deleted from the real servers of the Classic CLB instance.
>- If you need to use API to add real servers, please see the [RegisterTargetsWithClassicalLB](https://intl.cloud.tencent.com/document/product/214/33802) API.
>
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. On the "Instance Management" page, select the **Classic Cloud Load Balancer** tab.
3. Click **Configure Listener** in the "Operation" column on the right of the target Classic CLB instance.
4. In the listener configuration module, click **Create**.
5. In the "Create Listener" pop-up window, enter the "backend port" (for more information on port selection, please see [Common Server Ports](https://intl.cloud.tencent.com/document/product/213/12451)) and other related fields and click **Next** to complete the configuration. For more information, please see [Configuring Classic CLB](https://intl.cloud.tencent.com/document/product/214/32462).
>?You need to specify the real server port for Classic CLB during **listener creation**.
>
![](https://main.qcloudimg.com/raw/b2d43b48851d5c021a95872613e359c3.png)
6. After the listener is created, click **Bind** in the real server binding module.
7. In the **Bind CVM** pop-up window, select the CVM instance to be bound, enter the weight, and click **OK**.
>?
>- The pop-up window only displays available CVM instances in the same region and same network environment that are not isolated and have not expired with peak bandwidth greater than 0.
>- When multiple real servers are bound, CLB will forward traffic according to the hash algorithm to balance the load.
>- The greater the weight of a server, the more the requests forwarded to it. The default value is 10, and the configurable value range is 0–100. If the weight is set to 0, the server will not accept new requests. If session persistence is enabled, it may cause uneven request distribution among real servers. For more information, please see [Algorithms and Weight Configuration](https://intl.cloud.tencent.com/document/product/214/5371).
>
 ![](https://main.qcloudimg.com/raw/d9d9becb83da5d34e913591b86132aa5.png)

### Modifying real server weight for Classic CLB instance
>?Currently, real server weight cannot be modified through APIs for Classic CLB.
>
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. On the "Instance Management" page, select the **Classic Cloud Load Balancer** tab.
3. Click **Configure Listener** in the "Operation" column on the right of the target Classic CLB instance.
4. In the real server binding module, modify the relevant server weight.
>?The greater the weight of a server, the more the requests forwarded to it. The default value is 10, and the configurable value range is 0–100. If the weight is set to 0, the server will not accept new requests. If session persistence is enabled, it may cause uneven request distribution among real servers. For more information, please see [Algorithms and Weight Configuration](https://intl.cloud.tencent.com/document/product/214/5371).
>
	- **Method 1**. Modify the weight of one single server.
		1. Find the server whose weight needs to be modified, hover over the corresponding weight, and click <img src="https://main.qcloudimg.com/raw/4aae0dbec227f8fc18b4a35acf560f62.png" style="margin:0;">.
		![](https://main.qcloudimg.com/raw/9230ac972fdd0f1b8c55c5188c0424fd.png)
		2. In the "Modify Weight" pop-up window, enter the new weight value and click **Submit**.
	- **Method 2**. Modify the weight of multiple servers in batches.
	>?After the batch modification, the servers will have the same weight.
		>
		1. Click the checkbox in front of the servers, select multiple servers, and click **Modify Weight** at the top of the list.
		![](https://main.qcloudimg.com/raw/6e58995f13d57fe0cd9ea0c92e32d931.png)
		2. In the "Modify Weight" pop-up window, enter the new weight value and click **Submit**.

### Unbinding real server from Classic CLB instance
>?
>- Unbinding a real server will unbind the Classic CLB instance from the CVM instance, and Classic CLB will stop forwarding requests to it immediately.
>- Unbinding a real server will not affect the lifecycle of your CVM instance, which can be added to the real server cluster again when necessary.
>- If you need to use API to unbind real servers, please see the [DeregisterTargetsFromClassicalLB](https://intl.cloud.tencent.com/document/product/214/33807) API.
>
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. On the "Instance Management" page, select the **Classic Cloud Load Balancer** tab.
3. Click **Configure Listener** in the "Operation" column on the right of the target Classic CLB instance.
4. In the real server binding module, unbind the bound server.
	- **Method 1**. Unbind one single server.
		1. Find the server that needs to be unbound and click **Unbind** in the **Operation** column on the right.
		![](https://main.qcloudimg.com/raw/f398806fd564c8b0ff9ed1610b76ce4e.png)
		2. In the "Unbind Real Server" pop-up window, confirm the server to be unbound and click **Submit**.
	- **Method 2**. Unbind multiple servers in batches.
		1. Click the checkbox in front of the servers, select multiple servers, and click **Unbind** at the top of the list.
		![](https://main.qcloudimg.com/raw/088d33fd06d677741f58b91ea05ab1a2.png)
		2. In the "Unbind Real Server" pop-up window, confirm the servers to be unbound and click **Submit**.


