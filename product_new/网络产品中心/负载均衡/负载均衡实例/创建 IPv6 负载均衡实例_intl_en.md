>
>- IPv6 CLB is currently in beta test. If you want to use it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1) for application.
>- Currently, IPv6 CLB instances can be created in Beijing, Shanghai, and Guangzhou regions.
- IPv6 CLB does not support classic CLB.
- IPv6 CLB supports obtaining the client's IPv6 source address, which can be directly obtained by layer-4 IPv6 CLB or through the `X-Forwarded-For` header of HTTP layer-7 IPv6 CLB.
- IPv6 implementations are still at the primary stage across the internet. In case of access failure, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1). SLA is not guaranteed during the beta test period.

## Overview
IPv6 load balancing is implemented based on the IPv6 single stack technology. It can collaborate with IPv4 CLB to implement IPv6/IPv4 dual-stack communication. An IPv6 CLB instance is bound to an IPv6 address of a CVM instance and provides an IPv6 VIP address.
### IPv6 CLB Advantages
Tencent Cloud IPv6 CLB has the following advantages when helping your business quickly connect to IPv6:
- Quick connection: CLB enables connection to IPv6 in a matter of seconds and is available upon purchase.
- Ease of use: IPv6 CLB is compatible with IPv4 CLB operation process and easy to use with no additional learning costs incurred.
- End-to-end IPv6 communication: IPv6 CLB instances communicate with CVM instances over IPv6, which helps applications deployed on the CVM instances quickly upgrade to IPv6 and implement end-to-end IPv6 communication.

### IPv6 CLB Architecture
CLB supports creating IPv6 CLB instances. Tencent Cloud will assign an IPv6 public IP address, i.e., VIP of the IPv6 edition, to an IPv6 CLB instance, and the VIP will forward requests from IPv6 clients to the real IPv6 CVM instance.

An IPv6 CLB instance can support quick access of users from IPv6 public network and communicate with real servers over IPv6, which helps in-cloud applications quickly upgrade to IPv6 and implement end-to-end IPv6 communication.

The IPv6 CLB architecture is as shown below.
![](https://main.qcloudimg.com/raw/ca444992408e16390a46a3e2d9239bf5.svg)


## Operation Guide
### Step 1. Create an IPv6 CLB instance
1. Log in to the Tencent Cloud's official website and enter the [CLB purchase page](https://buy.cloud.tencent.com/lb).
2. Select options for the following parameters correctly:
 - Billing Mode: only pay-as-you-go billing is supported.
 - Region: Beijing, Shanghai, Guangzhou, Shanghai Finance, or Shenzhen Finance.
 - IP Version: IPv6.
 - ISP Type: BGP.
 - Network: please select a VPC and subnet that have already obtained IPv6 CIDR.
3. After setting the configuration items on the purchase page, click **Buy Now** to return to the [CLB instance list page](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1), where you can view the IPv6 CLB instance you just purchased.
![](https://main.qcloudimg.com/raw/b25a3156db7a73ffa1a3b835be0069e8.png)

### Step 2. Create an IPv6 CLB listener
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3) and click the IPv6 CLB instance ID to enter the details page.
2. Select the **Listener Management** tab and click **Create** to create a listener, e.g., a TCP listener.
> CLB supports creating layer-4 (TCP/UDP/TCP SSL) and layer-7 (HTTP/HTTPS) IPv6 CLB listeners. For more information, please see [CLB Listener Introduction](https://intl.cloud.tencent.com/document/product/214/6151).
>
3. In "Basic Configurations", configure the name, listening protocol port, and balancing method, and click **Next**.
![](https://main.qcloudimg.com/raw/815c00aa93b5f23408bd78791ea5b7c3.png)
4. Configure health check and click **Next**.
![](https://main.qcloudimg.com/raw/19fbf68edcb9d4f06102ae61c2228b67.png)
5. Configure session persistence and click **Submit**.
![](https://main.qcloudimg.com/raw/9743537a93828dc8c0c10e6c943f7673.png)
6. After the listener is created, select it and click **Bind** on the right.
>Before binding the listener to a CVM instance, please make sure that the CVM instance has obtained an IPv6 address.
>
![](https://main.qcloudimg.com/raw/edf72af61361da4f833f2424a548040e.png)
7. In the pop-up box, select the IPv6 CVM instance that needs to be communicated with, configure the server port and weight, and click **OK**.
![](https://main.qcloudimg.com/raw/7eb363ea3170bbe7a881762be7968210.png)
