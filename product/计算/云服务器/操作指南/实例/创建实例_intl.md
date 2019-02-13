## Prerequisites
Before creating a CVM instance, you need to complete the following steps:

- [Sign up for Tencent Cloud](https://intl.cloud.tencent.com/document/product/213/6090), and complete [Identity Verification](https://intl.cloud.tencent.com/document/product/378/3629).
- To create a VPC-based CVM instance, you need to [Create a VPC](https://intl.cloud.tencent.com/document/product/215/8113) in the target region, and [Create a Subnet](https://intl.cloud.tencent.com/document/product/215/8114) in the destination region under the VPC. 
- If you do not wish to use the default security group created by the system, you will need to [Create a Security Group](https://intl.cloud.tencent.com/document/product/213/18197#creating-a-security-group) in the target region, and add security group rules that meet your business needs.
- If you need to bind an SSH key pair when creating a Linux instance, please [Create an SSH key](https://intl.cloud.tencent.com/document/product/213/16691#creating-an-ssh-key) under the target project.
- To create a CVM instance with custom image, please click [Create Custom Image](https://intl.cloud.tencent.com/document/product/213/4942) or [Import Image](https://intl.cloud.tencent.com/document/product/213/4945).



## Procedure
1) Log in to [Tencent Cloud Official Website](https://intl.cloud.tencent.com), select **Product** -> **Compute** -> **Cloud Virtual Machine**, and then click the **Get Started** button to enter the CVM purchase page.

2) Select region and availability zone

- Select the region that is closest to your end-users to minimize network latency and improve access speed.
- In cases where you need multiple CVMs, it is recommended to select different availability zones for disaster recovery.
- For more information on regions and available zones, please see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091).

3) Select the series, model, and configuration.

- Tencent Cloud currently offers three instances series: Series 1, Series 2 and Series 3. It's recommended to use the latest series for the best performance. For more information on instance series, please see [here](https://intl.cloud.tencent.com/document/product/213/11518#S).
- Tencent Cloud offers standard, high IO, MEM optimized, computing, GPU, FPGA, big data, and network enhanced instances. For more information on models, please see [here](https://intl.cloud.tencent.com/document/product/213/11518#M).
- Tencent Cloud provides rich instance configurations for different models. For more information on instance configurations, please see [here](https://intl.cloud.tencent.com/document/product/213/11518).

4) Select an image.

- Depending on the source, Tencent Cloud provides image types such as public images, custom images and shared images. For more information, please see [Image Types](https://intl.cloud.tencent.com/document/product/213/4941).

5) Select a system disk and a data disk.

- System disk: Required. Used for installing the OS. You can select the type and capacity of the cloud disk for the system disk. The available types of cloud disks vary in different regions. The default capacity of the system disk is 50 GB.
- Data disk: Optional. You can add a data disk after creating an instance, or add a data disk when purchasing an instance, and then select the cloud disk type and capacity for the data disk. You can create an empty data disk, or use a data disk snapshot to create a data disk.
- For more information, please see [Cloud Block Storage Types](https://intl.cloud.tencent.com/document/product/213/4952).

6) Specify bandwidth

- To assign a public IP to an instance, the bandwidth must be larger than 0 Mbps.
- Traffic usage is the traffic incurred during usage of the instance. Only outbound traffic is charged. You can choose to set a bandwidth cap to avoid high cost due to sudden traffic. The unit price of the network is not affected by the bandwidth cap. 


7) Public gateway
- Public gateway is a CVM with forwarding feature enabled. CVMs without public IPs can access the Internet through a public gateway in a different subnet. The public gateway CVM will carry out source address translation for public network traffic. The IP of traffic by all CVMs accessing the public network is translated to the IP address of public gateway CVM after passing through the public gateway.


8) Set project and select security group
- You can **Create a Security Group** or select an **Existing Security Group**. You can also preview the security group rules. For more information, please see [Security Group](https://intl.cloud.tencent.com/document/product/213/12452).


9) Set instance name and login methods

- Instance name: You can select **Name It Now** to name the instance (up to 60 chars) when purchasing it, or select **Name It Later** to name it after purchase. In the latter case, the CVM instance is named "Not Named" by default. Please note that this is the display name of the instance on console, not the hostname of CVM.
- Login method: For CVMs with Linux images, you can choose **Set Password**, **SSH Key Pair**, and **Random Password** as the login method. For CVMs with Windows images, you can choose **Set Password** and **Random Password**.



10) Enable security and cloud monitoring components

- Security: Activate anti-DDoS service, WAF and Host Security for FREE. For more information, please see [CVM Security](https://intl.cloud.tencent.com/document/product/296/2221).
- Cloud monitoring: Activate cloud product monitoring for FREE. Install components to obtain CVM monitoring metrics and display them in the form of monitor icons, and support customization of alarm threshold. For more information, please see [Cloud Monitoring Overview](https://intl.cloud.tencent.com/document/product/248/13466).

11) Confirm and launch

- Specify the number of instances you need, and click **Enable** to launch the CVM instances
- After launching, you'll receive an internal message containing information including the instance name, public IP address, private IP address, login name, login password (if you chose **Random Password**). You can log in and manage instances with these information.





