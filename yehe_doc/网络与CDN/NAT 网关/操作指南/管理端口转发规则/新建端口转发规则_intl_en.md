A port forwarding table configures the DNAT feature on the NAT gateway. It maps the combination of **[private IP, protocol and port]** of a CVM in the VPC to a combination of **[public IP, protocol and port]** in the public network, so that resources on the CVM can be accessed from the public network.
You can create port forwarding rules by completing the steps below.

>? In a NAT gateway, an EIP can be set in the SNAT rule and port forwarding rule at the same time. See [Managing SNAT Rules](https://intl.cloud.tencent.com/document/product/1015/30237).
>
1. Log in to the [**NAT Gateway console**](https://console.cloud.tencent.com/vpc/nat?fromNav).
2. In the list, click the ID of the target NAT gateway to go to its details page. Click **Port Forwarding** tab.
<img src="https://qcloudimg.tencent-cloud.cn/raw/899b2499c178d8ba1a8b6086bd399978.png" width="70%">
3. Click **Create**, specify the **Protocol**, **Public port and IP** and **Internal port and IP**, and click **OK**.
>!The internal IP address only supports the private IP address of a CVM within the VPC.
>
![](https://qcloudimg.tencent-cloud.cn/raw/7e89db9a6122f50d4fc0ac55ad016684.png)

