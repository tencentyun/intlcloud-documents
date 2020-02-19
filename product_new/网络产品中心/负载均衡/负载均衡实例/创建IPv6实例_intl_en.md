>
>- IPv6 NAT64 CLB can only be created in three regions: Beijing, Shanghai, and Guangzhou.
>- IPv6 NAT64 CLB does not support classic CLB.
>- IPv6 NAT64 CLB does not support obtaining client IPs.
>- IPv6 implementations are still at the primary stage across the internet. In case of access failure, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1). SLA is not guaranteed during the beta test period.

CLB supports creating IPv6 NAT64 CLB instances. Tencent Cloud will assign an IPv6 public IP address, i.e., VIP of the IPv6 edition, to an instance, and the VIP will forward requests from IPv6 clients to the real IPv4 CVM instance.

## What Is an IPv6 NAT64 CLB Instance?
An IPv6 NAT64 CLB instance is a load balancer implemented based on the IPv6 NAT64 transition technology. Through an IPv6 NAT64 CLB instance, real servers can be quickly accessed by IPv6 users without any IPv6 modification required.

## IPv6 NAT64 CLB Architecture
The IPv6 NAT64 CLB architecture is as shown below.
![](https://main.qcloudimg.com/raw/caae8ad5e6a49ce24aeaa3fc0a6fd0c7.svg)
When IPv6 NAT64 CLB is accessed from an IPv6 network, CLB can smoothly convert IPv6 addresses to IPv4 addresses to adapt to existing services and quickly implement IPv6 transformation.

## IPv6 NAT64 CLB Advantages
Tencent Cloud IPv6 NAT64 CLB has the following advantages when helping your business quickly connect to IPv6:
- **Quick connection:** CLB enables connection to IPv6 in a matter of seconds and is available upon purchase.
- **Smooth business transition:** in order to smoothly transit your business to IPv6, you only need to transform the client with no modifications required for real servers. IPv6 NAT64 CLB supports access from IPv6 clients and converts IPv6 messages into IPv4 messages. IPv6 transition is imperceptible to applications on real servers, which still work in their original way.
- **Ease of use:** IPv6 NAT64 CLB is compatible with IPv4 CLB operation process and easy to use with no additional learning costs incurred.

## Operation Guide
### Creating an IPv6 NAT64 CLB instance
1. Log in to the Tencent Cloud's official website and enter the [CLB purchase page](https://buy.cloud.tencent.com/lb).
2. Select options for the following parameters correctly:
 - Region: only Beijing, Shanghai, and Guangzhou are supported.
 - Instance Type: CLB.
 - Network Type: public network.
 - IP version: IPv6 NAT64.
 - Network: VPC.
 - Other configurations are the same as general instance configurations.
3. After setting the configuration items on the purchase page, click **Buy Now** to return to the [CLB instance list page](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1), where you can view the IPv6 NAT64 CLB instance you just purchased.
![](https://main.qcloudimg.com/raw/d55b34c80b12ac6effa806d969ef74a0.png)

### Using IPv6 NAT64 CLB
Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1) and click an instance ID to enter the details page. On the "Listener Management" tab, you can configure listeners and forwarding rules and bind CVM instances. For more information, please see [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975).
![](https://main.qcloudimg.com/raw/37295edc8457d19babd3b6b9f2785de5.png)
