CLB instance specifications include shared and LCU-supported instances. By default, all instances are shared instances and can be upgraded to LCU-supported instances.


## Benefits of Upgrade
- A shared instance can sustain up to 50,000 concurrent connections, 5,000 new connections per second, and 5,000 queries per second (QPS). It enjoys a dedicated forwarding performance within the guaranteed performance range and uses the shared cluster resources for excessive performance, which may cause performance preemption.
- After being upgraded to an LCU-supported instance, a single instance can sustain up to 1 million concurrent connections, 100,000 new connections per second, and 50,000 QPS. For instances with higher specifications, [submit a ticket for application](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1).


## Impact of Upgrade
- After upgrade, LCU fees will be charged hourly by the actually consumed performance. For more information, see [LCU Pricing](https://intl.cloud.tencent.com/document/product/214/41563).
- After upgrade, the instance performance limits are 1 million concurrent connections, 100,000 new connections per second, and 50,000 QPS. If a limit is exceeded, speed throttling and packet loss may occur.
- After upgrade, if the actually consumed performance doesn't exceed any instance performance limit, existing connections will not be affected.
- Once upgraded, an instance cannot be downgraded to shared instance.
- The billing mode will not change after upgrade.
- The upgrade doesn't interrupt network connections and can be completed within 1 minute.

## Restrictions on Upgrade
- Currently, the LCU-supported instance type is in beta. To upgrade to or purchase one, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
- You can batch upgrade multiple pay-as-you-go shared instances.
- Classic CLB instances cannot be upgraded to LCU-supported instances.
- Classic network CLB instances cannot be upgraded to LCU-supported instances.
- Currently, you cannot purchase or upgrade to private network LCU-supported instances. For the specific release time, check the Tencent Cloud official website regularly.



## How to Upgrade
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb) and click **Instance Management** on the left sidebar.
2. In the CLB instance list, select the target shared instance and click **Upgrade** above the instance list.
![]()
3. In the **Instance Upgrade** pop-up window, click **OK**.
![]()


## References
[LCU Pricing](https://intl.cloud.tencent.com/document/product/214/41563)