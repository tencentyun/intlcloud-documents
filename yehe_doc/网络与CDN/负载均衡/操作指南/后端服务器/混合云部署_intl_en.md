In hybrid cloud deployment scenarios, you can directly bind CLB instances to IPs in the local IDC off the cloud so as to bind them to real servers across VPCs and IDCs.
This feature is in beta test. To try it out, for cross-region binding in the Chinese mainland, [submit a ticket](https://intl.cloud.tencent.com/apply/p/mzjxboiv2yq); for cross-region binding outside the Chinese mainland, [contact us](https://intl.cloud.tencent.com/contact-sales).

## Solution Strengths
- A hybrid cloud can be built quickly to seamlessly connect the environments in and off the cloud. CLB can forward requests to CVM instances in the in-cloud VPC and the off-cloud IDC at the same time.
- The high-quality public network access capabilities of Tencent Cloud can be reused.
- The rich features of CLB such as layer-4/7 access, health check, and session persistence can be reused.
- The private networks can be interconnected with each other through [CCN](https://intl.cloud.tencent.com/document/product/1003/30049), fine-grained routing is supported to guarantee the quality, and diversified tiered pricing is supported to reduce the costs.
![](https://main.qcloudimg.com/raw/e09b0e4b6fcaedf44267f6ca1950ee54.png)

## Limits
- Cross-network CVM instance binding is currently not supported for classic CLB instances.
- This feature is available only to bill-by-IP accounts. To check your account type, please see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
- This feature is only supported by VPC, not by classic networks.
- This feature is supported on IPv4 and IPv6 NAT64 CLB instances. The layer-7 IPv6 CLB instance needs to enable the dual-stack binding to bind the IPv4 and IPv6 CVM instances simultaneously for supporting cross-region binding 2.0 and hybrid cloud deployment.
- Cross-region binding 2.0 and hybrid cloud deployment do not support [Allow Traffic by Default in security groups](https://intl.cloud.tencent.com/document/product/214/14733), for which you need to allow the client IP and service port on the real server.
- CLB instances cannot be bound with each other in cross-region binding 2.0 and hybrid cloud deployment scenarios.
- This feature is only available in Guangzhou, Shenzhen, Shanghai, Jinan, Hangzhou, Hefei, Beijing, Tianjin, Chengdu, Chongqing, Hong Kong (China), Singapore and Silicon Valley.
- TCP and TCP SSL listeners need to use TOA on the real server to get the source IP. For more information, please see [Obtaining Real Client IPs via TOA in Hybrid Cloud Deployment](https://intl.cloud.tencent.com/document/product/214/45530).
- HTTP and HTTPS listeners need to use `X-Forwarded-For` (XFF) to get the source IP.
- UDP listeners cannot get the source IP.

## Prerequisites
1. You have submitted the application for beta test eligibility. For cross-region binding in the Chinese mainland, [submit a ticket](https://intl.cloud.tencent.com/apply/p/mzjxboiv2yq) for application. For cross-region binding outside the Chinese mainland, [contact your Tencent Cloud rep](https://intl.cloud.tencent.com/contact-sales).
2. You have created a CLB instance. For more information, please see [Creating CLB Instances](https://intl.cloud.tencent.com/document/product/214/6149).
3. You have created a CCN instance. For more information, please see [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062).
4. You have bound the direct connect gateway associated with the IDC and the target VPC to the created CCN instance. For more information, please see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).

## Directions
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. On the **Instance Management** page, click the ID of the target CLB instance.
3. On the **Basic Info** tab of the **Real Server** section, click **Configure** to bind a private IP of another VPC.
![](https://main.qcloudimg.com/raw/1214576094baa072eb1d3577a5f5781a.png)
4. Click **Submit** in the pop-up dialog box.
![](https://main.qcloudimg.com/raw/4f7b99a8532afabe54440ca7819dcd72.png)
5. On the **Basic Info** tab of the **Real Server** section, click **Add SNAT IP**.
![](https://main.qcloudimg.com/raw/fc41b320241fa4de1d961e1a9c8d428f.png)
6. In the pop-up dialog box, select **Subnet**, click **Add** to assign an IP, and click **Save**.
>?
>- A SNAT IP is mainly used in hybrid cloud deployment where requests are forwarded to IDC servers. It must be assigned when you bind a CLB instance to an IP in the IDC that is interconnected with CNN, and serves as the private IP of your VPC.
>- A maximum of 10 SNAT IPs can be configured for each CLB instance.
>- Each CLB instance configures one SNAT IP in one forwarding rule, and supports 55,000 max connections after being bound to one real server. If you configure more SNAT IPs or real servers, the number of connections increases proportionally. Assume that you configure 2 SNAT IPs for the CLB instance and bind 10 ports to the real server, resulting in a maximum of 1.1 million connections (2 x 10 x 55,000). You can calculate how many SNAT IPs to assign based on the number of connections.
>- **Be aware that deleting a SNAT IP will disconnect all connections on the IP.**
>
<img src="https://main.qcloudimg.com/raw/6aad8ac7d4a38a8e74ea7b3b59e36cbb.png" width="50%"/>
7. On the instance details page, open the **Listener Management** tab, and bind a real server to the CLB instance in the listener configuration section. For more information, please see [Managing Real Servers](https://intl.cloud.tencent.com/document/product/214/6156).
8. In the pop-up dialog box, select **Other Private IP**, click **Add a private IP**, and enter the target IDC private IP, port, and weight. Then click **Confirm**. For more information on ports, please see [Server Common Port](https://intl.cloud.tencent.com/document/product/213/12451).
![]()
9. Now you can view the bound IDC private IP in the **Bound Real Servers** section.<br/>
<img src="" width="60%"/>


## References
[Cross-Region Binding 2.0 (New)](https://intl.cloud.tencent.com/document/product/214/38441)
