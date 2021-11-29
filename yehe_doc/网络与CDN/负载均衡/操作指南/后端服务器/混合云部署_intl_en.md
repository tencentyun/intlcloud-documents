In hybrid cloud deployment scenarios, you can directly bind CLB instances to IPs in the local IDC off the cloud so as to bind them to real servers across VPCs and IDCs.
This feature is currently in beta. If you want to use it, please [submit a ticket](https://intl.cloud.tencent.com/apply/p/mzjxboiv2yq). 

## Solution Advantages
- A hybrid cloud can be built quickly to seamlessly connect the environments in and off the cloud. CLB can forward requests to CVM instances in the in-cloud VPC and the off-cloud IDC at the same time.
- The high-quality public network access capabilities of Tencent Cloud can be reused.
- The rich features of CLB such as layer-4/7 access, health check, and session persistence can be reused.
- The private networks can be interconnected with each other through [CCN](https://intl.cloud.tencent.com/document/product/1003/30049), fine-grained routing is supported to guarantee the quality, and diversified tiered pricing is supported to reduce the costs.
![](https://main.qcloudimg.com/raw/e09b0e4b6fcaedf44267f6ca1950ee54.png)	

## Limits
- Cross-network CVM instance binding is currently not supported for classic CLB instances.
- This feature is available only to bill-by-IP accounts. To check your account type, please see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
- Cross-region binding 2.0 and hybrid cloud deployment do not support [Allow Traffic by Default in security groups](https://intl.cloud.tencent.com/document/product/214/14733), for which you need to allow the client IP and service port on the real server.
- This feature is currently supported only in Guangzhou, Shenzhen, Shanghai, Jinan, Hangzhou, Beijing, Tianjin, Chengdu, Chongqing, Hong Kong (China), Singapore, and Silicon Vally.
- TCP and TCP SSL listeners need to use TOA on the real server to get the source IP. For more information, please see [TOA Module Loading Method](https://intl.cloud.tencent.com/document/product/608/18945).
- HTTP and HTTPS listeners need to use `X-Forwarded-For` (XFF) to get the source IP.
- UDP listeners cannot get the source IP.

## Prerequisites
1. Submit an application for beta test eligibility. For cross-region binding in the Chinese mainland, please submit a ticket for application. For cross-region binding outside the Chinese mainland, please [contact your Tencent Cloud rep](https://intl.cloud.tencent.com/contact-sales).
2. Create a CLB instance. For more information, please see [Creating CLB Instances](https://intl.cloud.tencent.com/document/product/214/6149).
3. Create a CCN instance. For more information, please see [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062).
4. Associate the Direct Connect gateway associated with the IDC and the target VPC with the created CCN instance. For more information, please see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).

## Operation Directions
1. Log in to the [CLB console](https://console.cloud.tencent.com/loadbalance).
2. On the **Instance Management** page, click the ID of the target CLB instance.
3. In the **Real Server** section on the **Basic Info** tab, click **Configure** to bind a private IP of another VPC.
![](https://main.qcloudimg.com/raw/1214576094baa072eb1d3577a5f5781a.png)
4. Click **Submit** in the pop-up box.
![](https://main.qcloudimg.com/raw/4f7b99a8532afabe54440ca7819dcd72.png)
5. In the **Real Server** section on the **Basic Info** tab, click **Add SNAT IP**.
![](https://main.qcloudimg.com/raw/fc41b320241fa4de1d961e1a9c8d428f.png)
6. In the pop-up box, select **Subnet**, click **Add** to assign an IP, and click **Save**.
<img src="https://main.qcloudimg.com/raw/6aad8ac7d4a38a8e74ea7b3b59e36cbb.png" width="50%"/>
7. On the instance details page, open the **Listener Management** tab, and bind a real server to the CLB instance in the listener configuration section. For more information, please see [Managing Real Servers](https://intl.cloud.tencent.com/document/product/214/6156).
8. In the pop-up box, select **Other Private IP**, click **Add a private IP**, enter the target IDC private IP, port, and weight, and click **Confirm**. For more information on ports, please see [Server Common Port](https://intl.cloud.tencent.com/document/product/213/12451).

9. Now you can view the bound IDC private IP in the **Bound Real Servers** section.<br/>



