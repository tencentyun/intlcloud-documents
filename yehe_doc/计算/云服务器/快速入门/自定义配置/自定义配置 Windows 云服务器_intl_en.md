Custom configuration provides more image platforms and advanced configurations for storage, bandwidth, and security group. You can select the configuration mode as needed. This document uses a custom configuration as an example.

## Registration and Verification

Before using a CVM, you need to perform the following operations:
1. Sign up for a Tencent Cloud account and complete identity verification. The identity verification is required if you want to purchase CVM instances in the Chinese mainland.
A new user needs to [sign up](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F) for an account on the Tencent Cloud website. For details, see [Signing up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).
2. Visit the [Tencent CVM Introduction](https://intl.cloud.tencent.com/product/cvm) page, and click **Get Started**.

<span id="SelectType"></span>
## Selecting a Device Model

1. Configure the following information as prompted by the page:
![Select region and model](https://main.qcloudimg.com/raw/40c2812ff1294f901238cc3e39ba25f9.png)
<table>
<tr><th style="width: 20%">Category</th><th style="width: 12%">Required/Optional</th><th>Configuration Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/213/2180">Billing Mode</a></td><td>Required</td><td><ul><li><b>Pay as you go</b>: an elastic billing mode for the CVM.</li></ul></td></tr>
<tr><td>Region</td><td>Required</td><td>We recommend you select a region closest to your customer to reduce access latency and increase access speed.</td></tr>
<tr><td>Availability Zone</td><td>Required</td><td>Select an availability zone as needed.</br>If you want to purchase multiple CVMs, we recommend you select different availability zones to implement disaster recovery.</td></tr>
<tr><td>Network</td><td>Required</td><td>Logically isolated network space built in Tencent Cloud. A virtual private cloud (VPC) includes at least one subnet. The system provides a default VPC and subnet for each region.</br>
If the existing VPC or subnet does not meet your requirements, you can create a VPC or subnet in the VPC console.</br><b>Note</b>:<ul><li>Resources in the same VPC can be shared within the private network.</li><li>When purchasing the CVM, ensure that the CVM and the subnet where the CVM is created have the same availability zones.</li></ul></td></tr>
<tr><td>Instance</td><td>Required</td><td>Tencent Cloud provides different instance types based on the underlying hardware. For optimal performance, we recommend you use the instance types of the latest generation.</br>For more information on instances, see <a href="https://intl.cloud.tencent.com/document/product/213/11518">Instance Types</a>.</td></tr>
<tr><td>Image</td><td>Required</td><td>Tencent Cloud provides public images, custom images, and shared images. For more information on images, see<a href="https://intl.cloud.tencent.com/document/product/213/4941">Image Types Overview</a>.</br>If you have just started using Tencent Cloud, we recommend you choose public images, which contain the activated official Windows operating system and do not require extra payments (except for North America regions).</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">System Disk</a></td><td>Required</td><td>Used to install the operating system. Its default capacity is 50 GB.</br>Available Cloud Block Storage (CBS) types vary with regions. Please select a value as instructed by the page.</br>For more information on CBS, see <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS Types</a>.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">Data Disk</a></td><td>Optional</td><td>Used to scale up the storage capacity of the CVM to to ensure high efficiency and reliability. CBS data disks are not added by default.</br>For more information on CBS, see <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS Types</a>.</td></tr>
<tr><td>Public Network Bandwidth</td><td>Required</td><td>Tencent Cloud provides two network billing modes. Set a value as required.<ul><li><b>Bill-by-bandwidth</b>: select a fixed bandwidth. Packet loss will occur when the bandwidth exceeds this value. This is applicable to scenarios where the network connection fluctuates slightly.</li><li><b>Bill-by-traffic</b>: billing is based on traffic that is actually used. You can specify a peak bandwidth to prevent charges incurred by unexpected traffic. Packet loss will occur when the instantaneous bandwidth exceeds this value. This is applicable to scenarios where the network connection fluctuates significantly.</li></ul></td></tr>
<tr><td>Quantity</td><td>Required</td><td>Number of CVMs to be purchased.</td></tr>
</table>
2. Click **Next: Complete Configuration** to access the CVM configuration page.

## Configuring the CVM
1. Configure the following information as prompted by the page:
![Security group and CVM](https://main.qcloudimg.com/raw/be9b22616da76afd527f855368707899.png)
<table>
<tr><th style="width: 20%">Category</th><th style="width: 12%">Required/Optional</th><th>Configuration Description</th></tr>
<tr><td>Security Group</td><td>Required</td><td>Used to configure the network access policies for one or more CVMs.</br><b>Ensure that login port 3389 is open.</b>For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/12452">Security Groups</a>.</td></tr>
<tr><td>Project</td><td>Required</td><td>The default project is selected. You can select an existing project as needed to manage different CVMs.</td></tr>
<tr><td>Tag</td><td>Optional</td><td>Used to categorize and manage CVM instances. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/19548">Managing Instances via Tags</a>.</td></tr>
<tr><td>Instance Name</td><td>Optional</td><td>The name of the CVM to be created.</br>It is user-defined. We recommend **CVM-01**.</td></tr>
<tr><td>Login Method</td><td>Required</td><td>Configure the method to log in to the CVM as needed.<ul><li><b>Custom Password</b>: customize the password for logging in to the instance.</li><li><b>SSH Key Pair</b>: select a key pair as the instance login credential (only available to the Linux operating system)</li><li><b>Random Password</b>: an automatically generated password will be sent through the <a href="https://console.cloud.tencent.com/message">Message Center</a>.</li></ul></td></tr>
<tr><td>Security Service</td><td>Optional</td><td>By default, security service is enabled for free to help you build a CVM security system to prevent data leakage.</td></tr>
<tr><td>Cloud Monitoring</td><td>Optional</td><td>By default, cloud monitoring is enabled for free. It provides comprehensive CVM data monitoring, intelligent data analysis, real-time fault alarms, and custom data reports to precisely monitor Tencent Cloud services and the health conditions of CVMs.</td></tr>
<tr><td>Advanced Settings</td><td>Optional</td><td>Configure additional settings for the instance as needed.<ul><li><b>Hostname</b>: you can customize the name of the computer in the CVM operating system. After a CVM is created, you can log in to it to view the hostname.</li><li><b>CAM Role</b>: you can set a role and use it to grant the role entity the permissions to access CVM services and resources and perform operations in Tencent Cloud. For more information about the settings, see<a href="https://intl.cloud.tencent.com/document/product/213/38290">Managing Roles</a>.</li><li><b>Placement Group</b>: you can add an instance to a placement group as needed to improve service availability. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/15486">Placement Group</a>.</li><li><b>Custom Data</b>: you can configure an instance by specifying custom data, and the configured scripts will run when an instance is launched. If multiple CVMs are purchased together, the custom data will run on all CVMs. The Windows operating system supports the PowerShell format and a maximum of 16 KB of raw data. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/17526">Configuring Custom Data (Windows CVM)</a>.</br><b>Note</b>: custom data configuration only supports public images on Windows. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/19670">Cloud-Init & Cloudbase-Init</a>.</li></ul></td></tr>
</table>
2. Click **Next: Confirm Configuration** to access the configuration information confirmation page.

## Confirming the Configuration Information

1. Check the information of the CVM to be purchased and the cost details of each configuration item.
2. Click **Purchase** and complete the payment. Then, you can log in to the [CVM console](https://console.cloud.tencent.com/cvm) to see your CVM.
Information such as the instance name, public IP address, private IP address, login username, and initial login password of the CVM will be sent to your account through [Message Center](https://console.cloud.tencent.com/message). You can use this information to log in to and manage your instances. To ensure security, change your CVM login password as soon as possible.

## Logging in to and Connecting the Instance

After completing CVM operations, you can log in to your CVM on the Tencent Cloud console and perform operations such as building a site as needed.
Select a method for logging in to the CVM on the Tencent Cloud console as needed:
- [Log in to a Windows CVM Instance Using the RDP File (Recommended)](https://intl.cloud.tencent.com/document/product/213/5435)
- [Log in to a Windows CVM Instance Using Remote Desktop](https://intl.cloud.tencent.com/document/product/213/32498)

## Formatting and Partitioning the Data Disk

If you added a data disk when [selecting the instance type](#SelectType), you need to format and partition the data disk after logging in to the CVM instance. **If you have not added any data disks, skip this step.**
Select the appropriate operations guide according to the disk capacity and the CVM operating system.
- For a disk smaller than 2 TB:
[Initializing a Cloud Disk (Windows)](https://intl.cloud.tencent.com/document/product/362/31597)
- For a disk equal to or larger than 2 TB:
[Initializing a Cloud Disk (Windows)](https://intl.cloud.tencent.com/document/product/362/31598)

For more operations, see [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596).
