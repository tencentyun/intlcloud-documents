CLB routes requests to real server instances that are running normally. This document describes how to add or delete real servers as needed or when you use CLB for the first time.

## Prerequisites
You have created a CLB instance and configured a listener. For more information, see [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975).
## Directions
### Adding a real server to CLB
>?
>- If a CLB instance is associated with an auto scaling group, CVMs in the group will be automatically added to the real servers of CLB. When a CVM instance is removed from the auto scaling group, it will be automatically deleted from the real servers of CLB.
>- For details on how to add real servers using the API, see [RegisterInstancesWithLoadBalancer](https://intl.cloud.tencent.com/document/api/214/1265).
>- If you have a bill-by-CVM account and select a non-BGP ISP (China Mobile/China Unicom/China Telecom), you can only bind bill-by-traffic and bill-by-bandwidth package CVM instances. For more information about account and ISP types, see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246) and [Product Attribute Selection](https://intl.cloud.tencent.com/document/product/214/13629).
>
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. On the **Instance Management** page, click **Configure Listener** on the right of a CLB instance.
3. On the listener configuration page, select a listener to bind to the backend CVM.
 - **HTTP/HTTPS listener**[](id:http)
	 1. In the **HTTP/HTTPS Listener** section, click **+** on the left of the listener you select.
	 ![](https://main.qcloudimg.com/raw/5c123efc112957e25f51ab2f8a753063.png)
	 2. Click **+** on the left of the domain name displayed.
	 ![](https://main.qcloudimg.com/raw/816b003603e735d3d4f21e8891d9e279.png)
	 3. Select the URL displayed and click **Bind**.
![](https://main.qcloudimg.com/raw/05f2041acaced53d2ae8bc24a2f0662b.png)
 - **TCP/UDP/TCP SSL listener**
In the list on the left of the TCP/UDP/TCP SSL listener section, select a listener to bind with the backend CVM.
![](https://main.qcloudimg.com/raw/7dc44fc32104e533b512ab6c0b616e21.png)
4. Bind the CLB instance with a real server.[](id:CLB)
	- **Method 1**: In the **Bind with backend service** dialog, click **CVM**, select one or more CVM instances, enter the forwarding port and weight, and click **Confirm**. For more information on ports, please see [Server Common Port](https://intl.cloud.tencent.com/document/product/213/12451).
>?
>- The pop-up window only displays available CVMs that are not isolated nor expired, in the same region, in the same network environment, and have peak bandwidth greater than 0.
>- When the CLB instance is bound with multiple real servers, it use the hash algorithm to forward traffic.
>- The larger the weight is, the more the requests are forwarded. Value range is 0-100 (default: 10). If it is set to 0, the real server stops receiving new requests. If session persistence is enabled, the requests from the real server may be not evenly distributed. For more details, see [Algorithms and Weight Configuration](https://intl.cloud.tencent.com/document/product/214/5371).
>
 ![](https://main.qcloudimg.com/raw/a7f71557ff1812f777c9e989b916049f.png)
	- **Method 2**: If the CVM instances that need to be bound in batches have the same preset port value, in the pop-up dialog click **CVM**, enter the port value, select the corresponding CVM instances, set the weights, and click **OK** to bind them in batches. For more details on ports, see [Server Common Port](https://intl.cloud.tencent.com/document/product/213/12451).
![](https://main.qcloudimg.com/raw/118bfbab842d72e990d9ffe08c6379ff.png)



### Modifying real server weights for CLB
The real server weight determines the number of CVM requests to be forwarded. When binding a real server, you need to preset its weight. The following shows an example of how to change the real server weight when a HTTP/HTTPS listener is used (which is also applied to a TCP/UDP/TCP SSL listener).
>?
>- For details on how to modify the real server weight with the API, see [ModifyLoadBalancerBackends](https://intl.cloud.tencent.com/document/api/214/1264).
>- For more information on weight of the load balancing real server, refer to [Cloud Load Balancer Round-robin Method](https://intl.cloud.tencent.com/document/product/214/6153).
>
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. On the **Instance Management** page, click **Configure Listener** on the right of a CLB instance.
3. In the list on the left of the HTTP/HTTPS listener section, click the expand icon to show the instance and listener rules, and select a URL.
![](https://main.qcloudimg.com/raw/06d500104032de3edda51bdc368b0c4b.png)
4. In the server list on the right of the HTTP/HTTPS listener section, modify the corresponding server weight.
>?The larger the weight is, the more the requests are forwarded. Value range is 0-100 (default: 10). If it is set to 0, the real server stops receiving new requests. If session persistence is enabled, the requests from the real server may be not evenly distributed. For more details, see [Algorithms and Weight Configuration](https://intl.cloud.tencent.com/document/product/214/5371).
>
	- **Method 1**: Modify weight of a single backend CVM
		1. Locate the CVM instance you want to edit and click the <img src="https://main.qcloudimg.com/raw/4aae0dbec227f8fc18b4a35acf560f62.png" style="margin:0;"> icon on the left of the weight.
		![](https://main.qcloudimg.com/raw/519a69a1fab550879e92cdfc159a8fa1.png)
		2. In the pop-up window, enter a new weight and click **Submit**.
	- **Method 2**: Modify weights of multiple backend CVMs
>?After you perform batch modification, the backend CVMs will use the same weight.
>
		1. Click checkboxes in front of the CVM instances you want to edit, and click **Modify Weight**.
		![](https://main.qcloudimg.com/raw/09fdd5cb7a49f80bdc088632d7249f1e.png)
		2. In the pop-up window, enter a new weight and click **Submit**.



### Modifying real server ports for CLB
You can modify real server ports in the CLB console. The following shows an example of how to change the real server port when a HTTP/HTTPS listener is used (which is also applied to a TCP/UDP/TCP SSL listener).
>?For details on how to modify the real server port with the API, see [ModifyTargetPort](https://intl.cloud.tencent.com/document/product/214/33812).
>
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. On the **Instance Management** page, click **Configure Listener** on the right of a CLB instance.
3. In the list on the left of the HTTP/HTTPS listener section, click the expand icon to show the instance and listener rules, and select a URL.
![](https://main.qcloudimg.com/raw/06d500104032de3edda51bdc368b0c4b.png)
4. In the list on the right of the HTTP/HTTPS listener section, modify the corresponding server port. For more details on how to select ports, see [Server Common Port](https://intl.cloud.tencent.com/document/product/213/12451).
	- **Method 1**: Modify port of a single backend CVM
		1. Locate the CVM instance you want to edit and click the <img src="https://main.qcloudimg.com/raw/4aae0dbec227f8fc18b4a35acf560f62.png" style="margin:0;"> icon on the left of the port.
		![](https://main.qcloudimg.com/raw/923c439bedc4af2e6129d8ada459a1c5.png)
		2. In the pop-up window, enter a new port value and click **Submit**.
	- **Method 2**: Modify ports of multiple backend CVMs
>?After you perform batch modification, the backend CVMs will use the same port.
>
	1. Click checkboxes in front of the CVM instances you want to edit, and click **Modify Port**.
	![](https://main.qcloudimg.com/raw/07d40e5fcf1111a9141be83e41f67797.png)
	2. In the pop-up window, enter a new port value and click **Submit**.



### Unbinding real servers from CLB
You can unbind bound real servers in the CLB console. The following shows an example of how to unbind the real server when a HTTP/HTTPS listener is used (which is also applied to a TCP/UDP/TCP SSL listener).
>?
>- Unbinding a real server will unbind the CLB instance from the CVM instance, and CLB will immediately stop forwarding requests to it.
>- Unbinding a real server will not affect the lifecycle of your CVM instance, which can also be added to the real server cluster again.
>- For details on how to unbind real servers with the API, see [DeregisterTargets](https://intl.cloud.tencent.com/document/product/214/33832).
>
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. On the **Instance Management** page, click **Configure Listener** on the right of a CLB instance.
4. In the list on the left of the HTTP/HTTPS listener section, click the expand icon to show the instance and listener rules, and select a URL.
![](https://main.qcloudimg.com/raw/06d500104032de3edda51bdc368b0c4b.png)
5. In the list on right of the HTTP/HTTPS listener section, unbind the bound real server.
	- **Method 1**: Unbind a single backend CVM
		1. Select the target CVM instance and click **Unbind**.
		![](https://main.qcloudimg.com/raw/c995daabbf0b6a710b21389b17b7760b.png)
		2. In the pop-up window, check the CVM instance you select and click **Submit**.
	- **Method 2**: Unbind multiple backend CVMs
		1. Click checkboxes in front of the CVM instances you want to unbind, and click **Unbind**.
		![](https://main.qcloudimg.com/raw/b397ef434ce42cfaa9a48b9f4f08f09f.png)
		2. In the pop-up window, check the CVM instances you select and click **Submit**.

