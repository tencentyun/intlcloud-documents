CLB supports creating IPv6 instances. Tencent Cloud will assign an IPv6 public IP address, i.e., VIP of the IPv6 edition, and the VIP forwards requests from IPv6 clients.

## What is IPv6?
Internet Protocol Version 6 (IPv6) is the latest version of the Internet Protocol (IP). It is the next-generation IP developed by the Internet Engineering Task Force (IETF) to replace the current IP version (IPv4). Compared with IPv4, IPv6 has the following features:
- IPv6 has a larger address space. IPv4 uses 32-bit addresses and has a limited number of addresses, restricting the development of the internet. By contrast, IPv6 uses 128-bit addresses, i.e., IPv6 supports 2<sup>128</sup>(approx. 3.4\*10<sup>38</sup>) addresses, an increase of about 7.9\*10<sup>28</sup> addresses compared with IPv4. It can be said that every grain of sand on the Earth can have an IPv6 address.
- IPv6 uses a smaller route table, which speeds up data packet forwarding.
- IPv6 features stronger support for multicast and bandwidth limit, and provides a good network platform for service quality control.
- IPv6 is securer. Its encryption and authentication options ensure group confidentiality and integrity, greatly enhancing network security.

## IPv6 CLB Architecture
The IPv6 CLB architecture is as shown below.
![](https://main.qcloudimg.com/raw/e86896cc8286b53e8198facc8d28076f.png)
When IPv6 CLB is accessed from an IPv6 network, CLB can smoothly convert IPv6 addresses to IPv4 addresses to adapt to existing services.

## IPv6 CLB Advantages
Tencent CLB has the following advantages when helping your business quickly connect to IPv6:
- **Quick connection:** CLB enables connection to IPv6 in a matter of seconds and is available upon purchase.
- **Smooth business transition:** In order to smoothly transit your business to IPv6, you only need to transform the client with no modifications required for your real server. IPv6 CLB supports access from IPv6 clients and converts IPv6 messages into IPv4 messages. IPv6 transition is imperceptible to applications on the real server, which still work in their original way.
- **Ease of use:** IPv6 CLB is compatible with IPv4 CLB traffic and easy to use with no additional learning costs incurred.

>
>- Currently, IPv6 CLB is available only in three regions: Beijing, Shanghai, and Guangzhou.
>- IPv6 CLB supports **CLB** but not Classic CLB.
>- IPv6 implementations are still at the primary stage across the internet. In case of access failure, you can submit a [ticket](https://console.cloud.tencent.com/workorder/category). SLA is not guaranteed during the beta test period.

## Operation Guide
### Creating an IPv6 CLB Instance
1. Log in at Tencent Cloud's official website and go to the [CLB purchase page](https://buy.cloud.tencent.com/lb).
2. Select **CLB** as instance type and **IPv6** as IP type. Other configurations are the same as general instance configurations.
3. After purchase, return to the [CLB instance list page](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1) where you can view the IPv6 CLB instance you just purchased.
![](https://main.qcloudimg.com/raw/9d3446c191de63911c40971ef6145264.png)

### Using an IPv6 CLB Instance
Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1) and click an instance ID to enter the details page. On the **Listener Management** tab, you can configure listeners and forwarding rules, and bind CVM instances. For more information, see [Getting Started with CLB](http://intl.cloud.tencent.com/document/product/214/8975).
![](https://main.qcloudimg.com/raw/68ba9471fbb0701fe1ddcfad982d6b44.png)
