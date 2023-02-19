CLB instances are available in two types: shared CLB instances and LCU-supported instances. You can upgrade shared CLB instances to LCU-supported CLB instances.


## Advantages of LCU-supported CLBs
- A shared instance can sustain up to 50,000 concurrent connections, 5,000 new connections per second, and 5,000 queries per second (QPS). It enjoys a dedicated forwarding performance within the guaranteed performance range and uses the shared cluster resources for excessive performance, which may cause performance preemption.
- Each LCU-supported CLB instance supports up to 1 million concurrent connections, 100,000 new connections, and 50,000 QPS. To increase the capability, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1).


## Upgrade Impact
-	**Rate limiting**
	- During the upgrade, the default bandwidth of a private network LCU-supported instance is 10 Gbps and can be adjusted, while that of a public network LCU-supported instance stays the same and cannot be adjusted (which can be adjusted in the console after the upgrade).
	- The maximum capability will be 1 million concurrent connections, 100k new connections/second, and 50k QPS. Rate limiting and packet loss occur if the upper limits are exceeded. For the rate liming metrics of LCU-supported instances, see below. For more information, see [Monitoring Metrics](https://intl.cloud.tencent.com/document/product/214/32389).
		- ClientConcurConn (Client-to-CLB concurrent connections)
		- ClientNewConn (Client-to-CLB new connections)
		- TotalReq (Queries per second)
		- ClientOuttraffic (Client-to-CLB outbound bandwidth)
		- ClientIntraffic (Client-to-CLB inbound bandwidth)
	- Existing connections will not be affected if the maximum capability of upgraded instances is not exceeded.

-	**Billing**
	- The billing mode remains unchanged.
	- The LCU fee will be billed based on the number of LCUs used per hour. For more details, see [LCU Pricing](https://www.tencentcloud.com/document/product/214/41563).

-	**Network connection**
	 The upgrade doesn't interrupt network connections and can be completed within 1 minute.

-	**Rollback**
	 Degrading to shared CLB instances is not allowed.

## Limitations
- Currently, the LCU-supported instance type is in beta. To upgrade to or purchase one, [submit a ticket](https://console.tencentcloud.com/workorder/category) for application.
- Upgrading multiple pay-as-you-go shared CLB instances is supported.
- Upgrading Classic CLB instances is not allowed.
- Upgrading classic network CLB instances is not allowed.




## How to Upgrade
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb), and click **Instance Management** on the left sidebar.
2. Select a shared CLB instance from the list and click **Upgrade**.
![]()
3. Click **OK** in the **Upgrading to LCU-supported** pop-up.
![]()


## References
[LCU Pricing](https://www.tencentcloud.com/document/product/214/41563)
