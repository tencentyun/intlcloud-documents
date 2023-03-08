[](id:q1)
### What is CVD?
CVD is an efficient, flexible, and secure cloud virtual desktop service. It allows you to quickly set up a virtual office system with no need to invest money and time in deployment.

[](id:q2)

### What desktop specifications does CVD offer?
CVD offers desktops with compute (vCPU and memory) and storage resources (system and data disks) in a wide variety of specifications that you can choose based on your use case.

[](id:q3)

### How is CVD billed?
Monthly subscription and pay-as-you-go billing are supported.
Monthly subscription is a prepaid billing mode, where you pay fees in advance to use resources for one or multiple months or even multiple years as needed.
Pay-as-you-go is a postpaid billing mode. It supports "shut down to save cost". After you shut down a desktop, the system will reclaim the compute resources (vCPUs, memory, and GPUs) without terminating the desktop. Therefore, for shut down desktops, only storage fees (system disks and data disks) will be incurred. Compute resources will not be charged. This helps you reduce costs.

[](id:q4)

### In which regions is CVD available?
CVD is currently available in Hong Kong only, with more regions to come. If you need to use it in other regions, please contact your sales representative. For more information, see [Use Limits](https://www.tencentcloud.com/document/product/1167/51911).

[](id:q5)

### Does CVD support on-premises deployment?
No, CVD **does not support on-premises deployment currently**. To learn more about the product, see [Cloud Virtual Desktop](https://www.tencentcloud.com/document/product/1167).

[](id:q6)

### Can I terminate CVD instances?
You can terminate or return CVD instances. Once the status of an instance changes to **Terminating** or **Terminated**, no more fees will be incurred for it. After a pay-as-you-go instance is terminated, all the data will be cleared and cannot be recovered, so you should ask users to back up their data first. For more information, see [Terminating/Returning Instance](https://www.tencentcloud.com/document/product/1167/51935).

[](id:q7)

### How do I create sub-users?
You can manage sub-users in the Tencent Cloud CAM console. For details, see [User Management](https://www.tencentcloud.com/document/product/1167/51940).

[](id:q8)

### What devices does CVD support?
When using a device, make sure that the device redirection policy is enabled. CVD is compatible with most devices. However, given the great variety of device interfaces, drivers, and protocols, if you encounter any problems, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
- If you want to connect a peripheral device through USB, make sure that the local device has a USB port and the USB redirection feature is enabled for the CVD instance.
- If you want to connect a peripheral device through Bluetooth, make sure that the local device supports Bluetooth.

[](id:q9)

### How do I access data in another VPC or a local IDC from a CVD instance?
The VPC you select when creating a CVD instance serves as a dedicated cloud network space for the desktop’s resources. This improves resource security and allows you to configure different desktops for different scenarios. You can access another VPC or a local IDC from your current instance by configuring a peer connection or VPN connection in your current VPC.

[](id:q10)

### Can I access the internet from a CVD instance?
A cloud virtual desktop accesses the internet through a NAT gateway. Just bind an EIP and you can provide secure and high-performance internet access for your CVD instance from its VPC. When creating a NAT gateway, select your instance’s VPC and configure a routing rule to route the subnet traffic to the NAT gateway. For more information, see [Configuring CVD Access to the Internet](https://www.tencentcloud.com/document/product/1167/51942).

[](id:q11)

### Can I access a CVD instance from a thin client?
You can access the CVD portal URL from any supported devices (including Windows and macOS devices) and HTML5 (such as Chrome and Firefox). You can also access CVD from a thin client. For more information, please contact your sales representative.

[](id:q12)
### Does CVD support API call?
CVD has not opened up APIs. If you have such needs, contact the channel manager for assistance.

