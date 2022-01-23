This document describes how to change the source IP of CLB health check from the default CLB [VIP](https://intl.cloud.tencent.com/document/product/214/32394) to the `100.64` IP range.

>?This feature is currently in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Use Cases
1. **Aggregating real server security groups**
The health check source IP is aggregated into the `100.64.0.0/10` IP range.

2. **Solving the problem of private network loopback in self-built Kubernetes cluster**
The K8s service needs to be exposed both inside and outside the cluster. The former is implemented through the cluster's internal load balancing (IPVS), and the latter is implemented through private network CLB. IPVS will bind the IP address of the private network CLB instance to a local interface, so that access to the instance address in the cluster is actually to use the IPVS load balancing in the cluster.
In the TKE service, the private network CLB uses the CLB VIP as the health check source IP, which conflicts with the address bound to the IPVS in the native K8s implementation, resulting in the failure of private network CLB health check.
Setting the health check source IP to the `100.64` IP range can avoid address conflicts and solve the problem of health check failures.

## Directions
This document takes a TCP listener as an example to describe how to change the source IP of CLB health check from the default CLB VIP to the `100.64` IP range.
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb).
2. Select a region in the top-left corner of the **Instance Management** page, find the target instance in the instance list, and click **Configure Listener** in the **Operation** column.
3. On the **Listener Management** tab, find the target listener, and click the ![](https://qcloudimg.tencent-cloud.cn/raw/11430ef75d92ba13520f8e05ed6d429b.svg) icon on its right to edit it.
4. In the **Edit Listener** pop-up window, click **Next** to enter the **Health Check** tab.
5. On the **Health Check** tab, select **100.64 IP range** as the health check source IP, click **Next**, and click **Submit**.
<img src="" width="70%" />

## Relevant Documentation
- [Configuring Health Check](https://intl.cloud.tencent.com/document/product/214/39251)
- [Health Check Identifiers](https://intl.cloud.tencent.com/document/product/214/6097)
