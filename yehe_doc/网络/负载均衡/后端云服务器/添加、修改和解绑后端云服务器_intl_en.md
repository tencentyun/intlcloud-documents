CLB routes requests to real server instances that are running normally. This document describes how to add or delete real servers as needed or when you use CLB for the first time.

## Prerequisites
You have created a CLB instance and configured a listener. For more information, please see [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975).
## Directions
### Adding real server to CLB instance
>?
>- If a CLB instance is associated with an auto scaling group, CVM instances in the group will be automatically added to the real servers of the CLB instance. When a CVM instance is removed from the auto scaling group, it will be automatically deleted from the real servers of the CLB instance.
>- If you need to use API to add real servers, please see the [RegisterInstancesWithLoadBalancer](https://intl.cloud.tencent.com/document/api/214/1265) API.
>
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. On the "Cloud Load Balancer" tab of the "Instance Management" page, click **Configure Listener** in the "Operation" column on the right of the target CLB instance.
4. In the listener configuration module, select the listener to be bound to a real server.
<span id="http"></span>
 - **HTTP/HTTPS Listener**
	 1. In the HTTP/HTTPS listener area, click "+" on the left of the target listener.
	 ![](https://main.qcloudimg.com/raw/561cc0f6ee3c0bce9e051fb20b4ec7bd.png)
	 2. Click "+" on the left of the expanded domain name.
	 ![](https://main.qcloudimg.com/raw/c4bb770736b9e185a3ecaddb9591331d.png)
	 3. Select the expanded URL path and click **Bind**.
![](https://main.qcloudimg.com/raw/05f2041acaced53d2ae8bc24a2f0662b.png)
 -**TCP/UDP/TCP SSL listener**
In the list on the left of the TCP/UDP/TCP SSL listener module, select the listener to be bound to a real server and click **Bind**.
![](https://main.qcloudimg.com/raw/7dc44fc32104e533b512ab6c0b616e21.png)
<span id="CLB"></span>
5. Bind a real server to the CLB instance.
	- **Method 1**. In the "Bind Real Server" pop-up window, click **CVM**, select one or multiple CVM instances to be associated with, enter the port and weight, and click **OK**. For more information, please see [Common Server Ports](https://intl.cloud.tencent.com/document/product/213/12451).
>?
>- The "Bind Real Server" pop-up window only displays available CVM instances in the same region and same network environment that are not isolated and have not expired with peak bandwidth greater than 0.
>- When multiple real servers are bound, CLB will forward traffic according to the hash algorithm to balance the load.
>- The greater the weight of a server, the more the requests forwarded to it. The default value is 10, and the configurable value range is 0–100. If the weight is set to 0, the server will not accept new requests. If session persistence is enabled, it may cause uneven request distribution among real servers. For more information, please see [Algorithms and Weight Configuration](https://intl.cloud.tencent.com/document/product/214/5371).
>
 ![](https://main.qcloudimg.com/raw/a7f71557ff1812f777c9e989b916049f.png)
	- **Method 2**. If you need to bind servers in batches with the same preset port value, you can click **CVM** in the "Bind Real Server" pop-up window, enter the default port value (for more information on port selection, please see [Common Server Ports](https://intl.cloud.tencent.com/document/product/213/12451)), check the target servers, set the weight value, and click **OK**.
![](https://main.qcloudimg.com/raw/118bfbab842d72e990d9ffe08c6379ff.png)

### Modifying real server weight for CLB instance
The real server weight determines the number of CVM requests to be forwarded. When binding a real server, you need to preset its weight. The following describes how to modify the real server weight with "HTTP/HTTPS listeners" as an example (which can be modified for TCP/UDP/TCP SSL listeners in the same way).
>?
>- If you need to use an API to modify real server weights, please see the [ModifyLoadBalancerBackends](https://intl.cloud.tencent.com/document/api/214/1264) API.
>- For more information on CLB real server weight, please see [CLB Polling Method](/doc/product/214/6153).
>
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. On the "Cloud Load Balancer" tab of the "Instance Management" page, click **Configure Listener** in the "Operation" column on the right of the target CLB instance.
4. In the list on the left of the HTTP/HTTPS listener module, expand the instances and listener rules, and select a URL path.
![](https://main.qcloudimg.com/raw/06d500104032de3edda51bdc368b0c4b.png)
5. In the server list on the right of the HTTP/HTTPS listener module, modify the relevant server weight.
>?The greater the weight of a server, the more the requests forwarded to it. The default value is 10, and the configurable value range is 0–100. If the weight is set to 0, the server will not accept new requests. If session persistence is enabled, it may cause uneven request distribution among real servers. For more information, please see [Algorithms and Weight Configuration](https://intl.cloud.tencent.com/document/product/214/5371).
>
	- **Method 1**. Modify the weight of one single server.
		1. Find the server whose weight needs to be modified, hover over the corresponding weight, and click <img src="https://main.qcloudimg.com/raw/4aae0dbec227f8fc18b4a35acf560f62.png" style="margin:0;">.
		![](https://main.qcloudimg.com/raw/519a69a1fab550879e92cdfc159a8fa1.png)
		2. In the "Modify Weight" pop-up window, enter the new weight value and click **Submit**.
	- **Method 2**. Modify the weight of multiple servers in batches.
	>?After the batch modification, the servers will have the same weight.
		>
		1. Click the checkbox in front of the servers, select multiple servers, and click **Modify Weight** at the top of the list.
		![](https://main.qcloudimg.com/raw/09fdd5cb7a49f80bdc088632d7249f1e.png)
		2. In the "Modify Weight" pop-up window, enter the new weight value and click **Submit**.



### Modifying real server port for CLB instance
You can modify the real server port in the CLB Console. The following describes how to modify the real server weight with "HTTP/HTTPS listeners" as an example (which can be modified for TCP/UDP/TCP SSL listeners in the same way).
>?If you need to use API to modify real server ports, please see the [ModifyTargetPort](https://intl.cloud.tencent.com/document/product/214/33812) API.
>
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. On the "Cloud Load Balancer" tab of the "Instance Management" page, click **Configure Listener** in the "Operation" column on the right of the target CLB instance.
4. In the list on the left of the HTTP/HTTPS listener module, expand the instances and listener rules, and select a URL path.
![](https://main.qcloudimg.com/raw/06d500104032de3edda51bdc368b0c4b.png)
5. In the server list on the right of the HTTP/HTTPS listener module, modify the relevant server port. For more information on port selection, please see [Common Server Ports](https://intl.cloud.tencent.com/document/product/213/12451).
	- **Method 1**. Modify the port of one single server.
		1. Find the server whose port needs to be modified, hover over the corresponding port, and click <img src="https://main.qcloudimg.com/raw/4aae0dbec227f8fc18b4a35acf560f62.png" style="margin:0;">.
		![](https://main.qcloudimg.com/raw/923c439bedc4af2e6129d8ada459a1c5.png)
		2. In the "Modify Port" pop-up window, enter the new port value and click **Submit**.
	- **Method 2**. Modify the port of multiple servers in batches.
	>?After the batch modification, the servers will have the same port.
		>
		1. Click the checkbox in front of the servers, select multiple servers, and click **Modify Port** at the top of the list.
		![](https://main.qcloudimg.com/raw/07d40e5fcf1111a9141be83e41f67797.png)
		2. In the "Modify Port" pop-up window, enter the new port value and click **Submit**.



### Unbinding real server from CLB instance
You can unbind bound real servers in the CLB Console. The following describes how to unbind bound real servers with "HTTP/HTTPS listeners" as an example (which can be unbound from TCP/UDP/TCP SSL listeners in the same way).
>?
>- Unbinding a real server will unbind the CLB instance from the CVM instance, and CLB will stop forwarding requests to it immediately.
>- Unbinding a real server will not affect the lifecycle of your CVM instance, which can be added to the real server cluster again when necessary.
>- If you need to use API to unbind real servers, please see the [DeregisterTargets](https://intl.cloud.tencent.com/document/product/214/33832) API.
>
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. On the "Cloud Load Balancer" tab of the "Instance Management" page, click **Configure Listener** in the "Operation" column on the right of the target CLB instance.
4. In the list on the left of the HTTP/HTTPS listener module, expand the instances and listener rules, and select a URL path.
![](https://main.qcloudimg.com/raw/06d500104032de3edda51bdc368b0c4b.png)
5. In the server list on the right of the HTTP/HTTPS listener module, unbind the bound real server.
	- **Method 1**. Unbind one single server.
		1. Find the server that needs to be unbound and click **Unbind** in the **Operation** column on the right.
		![](https://main.qcloudimg.com/raw/c995daabbf0b6a710b21389b17b7760b.png)
		2. In the "Unbind" pop-up window, confirm the server to be unbound and click **Submit**.
	- **Method 2**. Unbind multiple servers in batches.
		1. Click the checkbox in front of the servers, select multiple servers, and click **Unbind** at the top of the list.
		![](https://main.qcloudimg.com/raw/b397ef434ce42cfaa9a48b9f4f08f09f.png)
		2. In the "Unbind" pop-up window, confirm the servers to be unbound and click **Submit**.

