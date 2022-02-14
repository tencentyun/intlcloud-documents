Traffic mirror provides a traffic collection service that enables you to filter the traffic from the specified ENI using 5-tuple and other rules. Then you can copy the filtered traffic to CVM instances in the same VPC. This feature is applicable to use cases including security audit, risk monitoring, troubleshooting and business analysis. This document describes how to create a traffic mirror.
>? The traffic mirror feature is currently in beta. If you want to try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). Please save the link to the Traffic Mirror console for later logins, otherwise you may need to apply again.

## Prerequisites
Make sure that both the source IP and target ENI are in the same VPC and the source IP has a route table pointing to the target ENI.
## Directions
### Step 1: create a traffic mirror source
1. Open the link you obtained after [submitting a ticket](https://console.cloud.tencent.com/workorder/category) and log in to the Traffic Mirror console. In the top **Region** selector, choose the region where the traffic mirror will be created.
2. Click **+New**.
>? Up to 5 traffic mirrors can be created in one VPC.
>
3. In the pop-up window, configure as follows:
   - Enter a name for the traffic mirror (up to 60 characters).
   - Choose **Network**.
   - Choose **ENI** for **Collection Range**. That is, all traffic in the VPC will be collected, but the traffic of the ENI that is bound to receiving IPs will be excluded. This option requires selecting specific ENIs.
![](https://qcloudimg.tencent-cloud.cn/raw/902cad1c6ecd774e67ffe72d3ce4ab64.png)
   - Choose **Collection type**: select the traffic direction as needed. There are three options: All traffic, Traffic out and Traffic in.
   - Choose **Traffic filtering**: select a method to filter out unnecessary traffic and keep the mirror small and lightweight.
      - **N/A**: all traffic configured will be collected.
      - **Quintuple**: the traffic that meets 5-tuple conditions will be collected. After this option is selected, please specify **Protocol**, **Source IP range**, **Destination IP range**, **Source port**, and **Destination port**. You can click **Add** to create another filter condition. Only the traffic that meets all of filter conditions will be collected.
    ![](https://qcloudimg.tencent-cloud.cn/raw/ab47286ffbc185a6287552ac44de0c6f.png)
   - **The next hop is the NAT gateway**: collect traffic whose next hop address is the NAT gateway. After this option is selected, select the corresponding NAT gateway next to **Condition**.
4. After completing the configuration, click **Next**.

### Step 2: create a traffic mirror target
1. Set the receiving traffic as follows:
   + **Target type**: select the target ENI to receive the traffic.
> ?
> + At least one target ENI needs to be selected.
> + Traffic to the target ENI from inside the VPC is not collected.
>
   + **Balance method**: 
        + **Evenly distribution**: all traffic is distributed among all target ENIs evenly.
        + **HASH by ENI**: traffic from an ENI is always forwarded to a fixed target ENI.
![](https://qcloudimg.tencent-cloud.cn/raw/4b3e1c1c5bde43ed33d1724b072bb5e6.png)
2. Click **OK**.

## Result Validation
>! This document takes creating a traffic mirror that collects the outbound traffic of the 10.0.0.14 ENI accessing the www.qq.com website as an example.
>
1. Return to the **Traffic mirroring** page. If the traffic mirror that you just created is displayed with **Collect Traffic** enabled, the traffic mirror has been created successfully.
![](https://main.qcloudimg.com/raw/fd6191f3c858d0f2dd799a467c0d1c40.png)
2. Perform the following steps to verify whether the collected traffic is mirrored to the receiving IP.
	1. Generate the ENI traffic. For example, you can log in to the source CVM and run the `ping **public IP**` command.
    **Source data:**
	 ![](https://main.qcloudimg.com/raw/74ad4cbd7a6f2179b441cafee5976bba.png)
	2. [](id:buzhou2)Log in to the destination CVM and run the following commands to capture data and save it as a “.cap” or “.pcap” file. This document uses the “.pcap” file as an example.
```plaintext
tcpdump -i eth0 -w capture-2020-10-27.pcap    #Enter the actual file name.
```
	**Destination packets:** 
 ![](https://main.qcloudimg.com/raw/404f6d2c612ae76b78aa63a624e98910.png)
	3. Use a terminal simulator (such as SecureCRT) to log in to the destination CVM and export the file saved in [Step ii](#buzhou2).
 ```plaintext
sz -bye capture-2020-10-27.pcap
 ```
	4. Use a packet parser (such as Wireshark) to obtain data from the “capture-2020-10-27.pcap” file that has been downloaded. In this example, 12 mirrored packets of the source CVM are obtained from the destination CVM.
	 **Packet verification:**
![](https://main.qcloudimg.com/raw/8011aef82006411e35edd41bf5eae5c4.png)
3. If an exceptional packet is obtained, or it’s unable to obtain packets, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Subsequent operations
- [Enabling or disabling the traffic mirror](https://intl.cloud.tencent.com/document/product/215/36393)
- [Modifying the traffic mirror](https://intl.cloud.tencent.com/document/product/215/36393)
- [Adding a tag](https://intl.cloud.tencent.com/document/product/215/36393)
- [Deleting the traffic mirror](https://intl.cloud.tencent.com/document/product/215/36393)
