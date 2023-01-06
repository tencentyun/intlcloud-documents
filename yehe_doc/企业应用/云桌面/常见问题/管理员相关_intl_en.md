[](id:q1)
### What is a CVD instance?
CVD is an efficient, flexible, and secure cloud virtual desktop service. It allows you to quickly set up a virtual office system with no need to invest money and time in deployment.

[](id:q2)
### Does CVD offer a free trial?
Currently, CVD offers a free trial only to [enterprise users](https://console.cloud.tencent.com/cvd). To try it out, complete the enterprise identity verification for your Tencent Cloud account first.

[](id:q3)
### What are the specifications of CVD?
CVD comes with rich compute resources (vCPU and memory) and storage resources (system and data disks). It is available in a wide variety of specifications. You can flexibly select the computing power and storage space most appropriate for your use case.

[](id:q4)
### How is CVD billed?
Monthly subscription and pay-as-you-go billing are supported.
Monthly subscription is a prepaid billing mode, where you pay fees in advance to use resources for one or multiple months or even multiple years as needed.
Pay-as-you-go is a postpaid mode, which supports the "shut down to save cost" feature; that is, if your instance is shut down and retained, the system will automatically repossess compute resources (vCPU, memory, and GPU) and charge fees only for storage resources (system and data disks) but not compute resources.

[](id:q5)
### In which regions is CVD available?
CVD is currently available in Beijing (Beijing Zone 5), Shanghai (Shanghai Zone 5), and Guangzhou (Guangzhou Zone 6), with more regions to come. If you need to use it in other regions, please contact your sales representative for assistance. For more information, see [Use Limits](https://www.tencentcloud.com/document/product/1167/51911).

[](id:q6)
### Does CVD support on-premises deployment?
No. For more information on the product, see [Cloud Virtual Desktop](https://www.tencentcloud.com/document/product/1167).

[](id:q7)
### Can I terminate CVD instances?
You can terminate or return CVD instances. Once the status of an instance changes to **Terminating** or **Terminated**, no more fees will be incurred for it. After a pay-as-you-go instance is terminated, all the data will be cleared and cannot be recovered, so you should ask users to back up their data first. For more information, see [Terminating/Returning Instance](https://www.tencentcloud.com/document/product/1167/51935).

[](id:q8)
### How do I create a user?
You can manage users in the IDaaS console. After you are redirected to Tencent Cloud IDaaS, select **Create user** and enter information such as the name (display name), user ID (login account), primary email (for account activation), and department. The user will receive an email for account activation and can log in to the CVD portal with the account and password after activating the account.

[](id:q9)
### How do I assign a CVD instance?
On the **Desktop List** page, select the target CVD instance and click **Bind user**. Note that the instance should be in **To be assigned** and **Started** status.

[](id:q10)
### Can I bind multiple users to the same CVD instance?
No, only one user can be bound to a desktop.

[](id:q11)
### How do I create a custom policy for my CVD instance?
You can create a custom policy in the following steps:
1. Go to the [CVD console](https://console.cloud.tencent.com/cvd) and click **Create policy** on the **Policy Management** page.
2. Configure the following information as prompted:
<table>
   <tr>
      <th width="0%" >Configuration Item</td>
      <th width="0%" >Description</td>
   </tr>
   <tr>
      <td>Policy</td>
      <td>Enter the policy name to differentiate between different policies.</td>
   </tr>
   <tr>
      <td>Description</td>
      <td>Enter the optional policy description to further differentiate between different policies.</td>
   </tr>
   <tr>
      <td>File redirection</td>
      <td>Set the operation permission of the CVD instance on local files.</td>
   </tr>
   <tr>
      <td>Clipboard redirection</td>
      <td>Set the two-way or one-way copy permission between the CVD instance and local device.</td>
   </tr>
   <tr>
      <td>Device redirection</td>
      <td>Set whether to enable the device redirection feature. After it is enabled, the CVD instance can use the USB storage and COM port devices connected to the local device.</td>
   </tr>
   <tr>
      <td>Watermark</td>
      <td>Specify the watermark content and display for the policy.</td>
   </tr>
   <tr>
      <td>Users</td>
      <td>Specify the users for whom the custom policy takes effect. Then, the policy will take effect for all the CVD instances of specified users.</td>
   </tr>
</table>
3. After confirming that everything is correct, click **Save**. The policy will take effect at the next login.


[](id:q12)
### What is the limit on the number of CVD policies?
Each account can have up to ten policies (including the default one). If you need more policies, please contact your sales representative for assistance.


[](id:q14)
### What devices does CVD support?
When using a device, make sure that the device redirection policy is enabled. CVD is compatible with most devices. However, given the great variety of device interfaces, drivers, and protocols, if you encounter any problems, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
- If you want to connect a peripheral device through USB, make sure that the local device has a USB port and the USB redirection feature is enabled for the CVD instance.
- If you want to connect a peripheral device through Bluetooth, make sure that the local device supports Bluetooth.

[](id:q15)
### How do I access data in another VPC or a local IDC from a CVD instance?
Before creating a CVD instance, you need to select a VPC, which serves as a dedicated cloud network space to sustain CVD resources to improve the resource security in different scenarios. By configuring a peer connection or VPN connection based on the VPC of the instance resources, you can access another VPC or a local IDC from the instance.

[](id:q16)
### Can I access the internet from a CVD instance?
You can access the internet from a CVD instance through NAT Gateway. You can bind an EIP to provide secure and high-performance internet access for your CVD instance in the VPC. When creating a NAT gateway, select the correct VPC and configure the routing rules to route subnet traffic to the NAT gateway. For more information, see [Configuring CVD Access to the Internet](https://www.tencentcloud.com/document/product/1167/51942).

[](id:q17)
### Can I access a CVD instance from a thin client?
You can access the CVD portal URL from any supported devices (including Windows and macOS devices) and HTML5 (such as Chrome and Firefox). You can also access CVD from a thin client. For more information, please contact your sales representative.

[](id:q18)
### Does CVD support API call?
CVD has not opened up APIs. If you have such needs, contact the channel manager for assistance.

