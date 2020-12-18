In hybrid cloud deployment scenarios, you can directly bind a CLB instance to IPs in the local IDC off the cloud so as to bind it to real servers across VPCs and IDCs.
This feature is currently in beta test. For cross-region binding in Mainland China, please submit a ticket for application. For cross-region binding outside Mainland China, please [contact your Tencent Cloud rep](https://intl.cloud.tencent.com/contact-sales).

## Scheme Advantages
- A hybrid cloud can be built quickly to seamlessly connect the environments in and off the cloud. CLB can forward requests to CVM instances in the in-cloud VPC and the off-cloud IDC at the same time.
- The high-quality public network access capabilities of Tencent Cloud can be reused.
- The rich features of CLB such as layer-4/7 access, health check, and session persistence can be reused.
- The private networks can be interconnected with each other through [CCN](https://intl.cloud.tencent.com/document/product/1003/30049), fine-grained routing is supported to guarantee the quality, and diversified tiered pricing is supported to reduce the costs.
![](https://main.qcloudimg.com/raw/e09b0e4b6fcaedf44267f6ca1950ee54.png)

## Limits
- Cross-network CVM instance binding is currently not supported for private network CLB and classic CLB.
- This feature is available only to standard accounts. You can determine the account type as instructed in [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246#judge).
- Currently, this feature is supported only in the Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, and Hong Kong (China) regions.
- TCP and TCP SSL listeners need to use TOA on the real server to get the source IP. For more information, please see [Loading TOA Module](https://intl.cloud.tencent.com/document/product/608/18945).
- HTTP and HTTPS listeners need to use X-Forwarded-For (XFF) to get the source IP.
- UDP listeners cannot get the source IP.

## Prerequisites
1. You have submitted the application for beta test eligibility. For cross-region binding in Mainland China, please submit a ticket for application. For cross-region binding outside Mainland China, please [contact your Tencent Cloud rep](https://intl.cloud.tencent.com/contact-sales).
2. You have created a CLB instance. For more information, please see [Creating CLB Instances](https://intl.cloud.tencent.com/document/product/214/6149).
3. You have created a CCN instance. For more information, please see [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062).
4. You have associated the Direct Connect gateway associated with the IDC and the target VPC to be bound with the created CCN instance. For more information, please see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).

## Directions
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. On the "Instance Management" page in the CLB Console, click the ID of the target CLB instance.
3. In the "Real Server" section on the "Basic Info" page, click **Configure** to bind a private IP not in the current VPC.
![](https://main.qcloudimg.com/raw/1214576094baa072eb1d3577a5f5781a.png)
4. In the "Enable IP Not in Current VPC" dialog box that pops up, click **Submit**.
![](https://main.qcloudimg.com/raw/4f7b99a8532afabe54440ca7819dcd72.png)
5. In the "Real Server" section on the "Basic Info" page, click **Add SNAT IP**.
![](https://main.qcloudimg.com/raw/fc41b320241fa4de1d961e1a9c8d428f.png)
6. In the "Add SNAT IP" dialog box that pops up, select "Subnet", click **Add** to assign an IP, and click **Save**.
<img src="https://main.qcloudimg.com/raw/6aad8ac7d4a38a8e74ea7b3b59e36cbb.png" width="50%"/>
7. On the instance details page, click the "Listener Management" tab and bind a real server to the CLB instance in the "Configure Listener" section. For more information, please see [Adding real server to CLB instance](https://intl.cloud.tencent.com/document/product/214/6156).
8. In the "Bind Real Server" dialog box that pops up, select "Other Private IPs", click **Add Private IP**, enter the IDC private IP address to be bound, port, and weight, and click **OK**. For more information, please see [Common Server Ports](https://intl.cloud.tencent.com/document/product/213/12451).
9. Return to the "Bound Real Servers" section and you can view the bound IDC private IP.<br/>


