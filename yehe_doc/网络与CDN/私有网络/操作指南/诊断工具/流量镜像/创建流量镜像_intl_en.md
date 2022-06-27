A traffic mirror provides a traffic collection service that enables you to filter the traffic from the specified ENI by using quintuple and other rules. Then you can copy the filtered traffic to CVM instances in the same VPC. This feature is applicable to use cases including security audit, risk monitoring, troubleshooting, and business analysis. This document describes how to create a traffic mirror.
>? The traffic mirror feature is currently in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application. Save the link to the Traffic Mirror console for later logins; otherwise, you may need to apply again.

## Prerequisites
Make sure that the source IP and target ENI are in the same VPC and that the source IP has a route table pointing to the target ENI.

## Directions

### Step 1. Create a traffic mirror source
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Diagnostic Tools** > **Traffic Mirror** on the left sidebar and select the target region.
2. Click **+New**.
>?Up to five traffic mirrors can be created in a VPC.
>
3. In the pop-up window, configure as follows:
   - Enter the traffic mirror name (up to 60 characters).
   - Choose **Network**.
   - Select **ENI** for **Collection Scope**. That is, all traffic in the VPC will be collected, excluding the traffic of the ENI that is bound to the receiving IPs. If you select this option, you need to select the specific ENI.
![](https://qcloudimg.tencent-cloud.cn/raw/902cad1c6ecd774e67ffe72d3ce4ab64.png)
   - Select **Collection type**: Select the traffic direction as needed. There are three options: **All traffic**, **Traffic out**, and **Traffic in**.
   - Select **Traffic filtering**: Select a method to filter out unnecessary traffic and keep the mirror small and lightweight.
      -**N/A**: All traffic configured will be collected.
      - **Quintuple**: The traffic that meets quintuple conditions will be collected. After selecting this option, specify **Protocol**, **Source IP range**, **Destination IP range**, **Source port**, and **Destination port**. You can click **Add** to create another filter. Only the traffic that meets all of the filters will be collected.
    ![](https://qcloudimg.tencent-cloud.cn/raw/ab47286ffbc185a6287552ac44de0c6f.png)
    - **The next hop is the NAT gateway**: Collect traffic whose next hop address is the NAT gateway. After selecting this option, select the specific NAT gateway next to **Condition**.
4. After completing the configuration, click **Next**.

### Step 2. Create a traffic mirror target
1. On the **Create Traffic Mirror Target** page, configure the following items:
   + **Target type**: Select the target ENI to receive the forwarded traffic.
> ?
> + At least one target ENI needs to be selected.
> + Traffic to the target ENI from inside the VPC will not be collected.
>
   + **Balance method**:
        + **Evenly distribute traffic**: All traffic is distributed among all target ENIs evenly.
        + **HASH by ENI**: Traffic from an ENI is always forwarded to a fixed target ENI.
![](https://qcloudimg.tencent-cloud.cn/raw/4b3e1c1c5bde43ed33d1724b072bb5e6.png)
2. Click **OK**.

## Result Validation
>!This document takes creating a traffic mirror that collects the outbound traffic of the 10.0.0.14 ENI accessing the www.qq.com website as an example.
>
1. Return to the **Traffic Mirror** page. If the created traffic mirror is displayed in the list with **Collect Traffic** enabled, it has been created successfully.
![](https://main.qcloudimg.com/raw/fd6191f3c858d0f2dd799a467c0d1c40.png)
2. Perform the following steps to verify whether the collected traffic is mirrored to the receiving IP.
	1. Generate the ENI traffic. For example, you can log in to the source CVM and run the "ping **public IP**" command.
    **Source data:**
	 ![](https://main.qcloudimg.com/raw/74ad4cbd7a6f2179b441cafee5976bba.png)
	2. [](id:buzhou2)Log in to the destination CVM and run the following command to capture data and save it as a `.cap` or `.pcap` file. This document uses the `.pcap` file as an example.
```plaintext
tcpdump -i eth0 -w capture-2020-10-27.pcap # Enter the actual filename.
```
	**Destination packets:** 
 ![](https://main.qcloudimg.com/raw/404f6d2c612ae76b78aa63a624e98910.png)
	3. Use a terminal simulator (such as SecureCRT) to log in to the destination CVM and export the file saved in [Step ii](#buzhou2).
 ```plaintext
sz -bye capture-2020-10-27.pcap
 ```
	4. Use a packet parser (such as Wireshark) to get the data from the downloaded `capture-2020-10-27.pcap` file. In this sample, 12 mirrored packets of the source CVM instance are obtained from the destination CVM instance.

 **Packet verification:**
	 ![](https://main.qcloudimg.com/raw/8011aef82006411e35edd41bf5eae5c4.png)

3. If an abnormal packet is obtained or packets cannot be obtained, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## Subsequent Operations
- [Enabling and Disabling a Traffic Mirror](https://intl.cloud.tencent.com/document/product/215/36393)
- [Modifying a Traffic Mirror](https://intl.cloud.tencent.com/document/product/215/36393)
- [Adding Tags](https://intl.cloud.tencent.com/document/product/215/36393)
- [Deleting a Traffic Mirror](https://intl.cloud.tencent.com/document/product/215/36393)
