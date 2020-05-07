Compared with using quick configuration to create a Tencent Cloud Virtual Machine (CVM), custom configuration provides more image platforms and advanced configurations for storage, bandwidth, and security group. You can select the configuration method as needed. This document uses custom configuration as an example.
To create a CVM with quick configuration, you can refer to [Custom Configuration for Windows CVM](https://intl.cloud.tencent.com/document/product/213/2764).

## Registration and Verification

Before using the CVM, you need to perform the following operations:
1. Sign up for a Tencent Cloud account and complete identity verification.
A new user needs to [sign up](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F) for an account on the official website of Tencent Cloud. For detailed operations, see [Sign Up for a Tencent Cloud Account](https://cloud.tencent.com/doc/product/378/9603).
2. Visit the [Tencent CVM Introduction](https://intl.cloud.tencent.com/product/cvm) page, click **Get Started** and “Create”.

<span id="SelectType"></span>
## Selecting the Model

1. Configure the following information as prompted by the page:
![Select region and model](https://main.qcloudimg.com/raw/07493412dd043911fe8aa3ecb0d0bcd4.png)
<table>
<tr><th style="width: 20%">Category</th><th style="width: 12%">Required/Optional</th><th>Configuration Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/213/2180">Billing Mode</a></td><td>Required</td><td>Please select based on your actual needs:<ul><li><b>Pay-as-you-go</b>: an elastic billing method applicable to scenarios such as e-commerce flash sales, where demand will fluctuate significantly in an instant.</li><li><b>Spot instance</b>: a new instance operation mode applicable to scenarios such as big data computing and online website service using load balancing. Its general price range is 10% - 20% of a pay-as-you-go instance.</li></ul></td></tr>
<tr><td>Region</td><td>Required</td><td>We recommend you select a region closest to your customer to reduce access latency and increase access speed.</td></tr>
<tr><td>Availability Zone</td><td>Required</td><td>Select a value as needed.</br>If you want to purchase multiple CVMs, we recommend you select different availability zones to implement disaster recovery.</td></tr>
<tr><td>Network</td><td>Required</td><td>Logically isolated network space built in Tencent Cloud. A virtual private cloud (VPC) includes at least one subnet. The system provides a default VPC and subnet for each region.</br>
If the existing VPC or subnet does not meet your requirements, you can create a VPC or subnet in the VPC console.</br><b>Note</b>:<ul><li>resources in the same VPC can be shared within the private network.</li><li>When purchasing the CVM, ensure that the CVM and the subnet where the CVM is created have the same availability zones.</li></ul></td></tr>
<tr><td>Instance</td><td>Required</td><td>Tencent Cloud provides different types of instances based on the underlying hardware. To achieve optimal performance, we recommend you use instances of the latest generation.</br>For more information about instances, see <a href="https://intl.cloud.tencent.com/document/product/213/11518">Instance Specifications</a>.</td></tr>
<tr><td>Image</td><td>Required</td><td>Tencent Cloud provides common images, custom images, and shared images. You can select an appropriate type by referring to <a href="https://intl.cloud.tencent.com/document/product/213/4941">Image Types</a>.</br>For users who just started using Tencent Cloud, we recommend public images, which contain the activated official Windows operating system and require no extra payment (except for North America regions).</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">System Disk</a></td><td>Required</td><td>Used to install the operating system. Its capacity is 50 GB by default.</br>Available disk types vary by regions. Select as instructed by the page.</br>For more information about CBS, see <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS Types</a>.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">Data Disk</a></td><td>Optional</td><td>Used to scale up the storage capacity of the CVM to ensure high efficiency and reliability. CBS data disks are not added by default.</br>For more information about CBS, see <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS Types</a>.</td></tr>
<tr><td>Public Network Bandwidth</td><td>Required</td><td>Tencent Cloud provides two network billing modes. Select as needed.<ul><li><b>Bill-by-bandwidth</b>: select a fixed bandwidth. Packet loss occurs when this bandwidth is exceeded. This mode is applicable to scenarios where network connection fluctuates slightly.</li><li><b>Bill-by-traffic</b>: billing is based on actual usage. You can specify a maximum bandwidth to prevent being charged for unexpected traffic. Packet loss occurs when the instantaneous bandwidth exceeds this value. This mode is applicable to scenarios where network connection fluctuates significantly.</li></ul></td></tr>
<tr><td>Quantity</td><td>Required</td><td>The number of CVMs to be purchased.</td></tr>  
</table>
2. Click **Next: Complete Configuration** to open the CVM configuration page.

## Configuring the CVM
1. Configure the following information as prompted by the page:
![Security group and CVM](https://main.qcloudimg.com/raw/a1aff1911b9e82506e93c591dd69ee26.png)
<table>
<tr><th style="width: 20%">Category</th><th style="width: 12%">Required/Optional</th><th>Configuration Description</th></tr>
<tr><td>Project</td><td>Required</td><td>The default project is selected by default. You can select an existing project as needed to manage different CVMs.</td></tr>
<tr><td>Security Group</td><td>Required</td><td>Used to configure the network access policies for one or more CVMs.</br><b>Ensure that login port 3389 is open.</b>For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/12452">Security Group</a>.</td></tr>
<tr><td>Instance Name</td><td>Optional</td><td>The name of the CVM to be created.</br>It is defined by the user. We recommend **CVM-01**.</td></tr>
<tr><td>Login Methods</td><td>Required</td><td>The method for logging into the CVM. Please select base on your actual needs.<ul><li><b>Custom Password</b>: customize the password for logging into the instance.</li><li><b>Random Password</b>: an auto-generated password will be sent via <a href="https://console.cloud.tencent.com/message">Internal Messages</a>.</li></ul></td></tr>
<tr><td>Security Service</td><td>Optional</td><td>Enabled for free by default to help users build a CVM security protection system against data leakage.</td></tr>
<tr><td>Cloud Monitoring</td><td>Optional</td><td>Enabled for free by default. It provides comprehensive CVM data monitoring, intelligent data analysis, real-time fault alarms, and custom data reports to help users precisely monitor Tencent Cloud services and the health conditions of CVMs.</td></tr>
<tr><td>Advanced Settings</td><td>Optional</td><td>You can configure additional settings of the instance as needed.<ul><li><b>Hostname</b>: you can customize the internal computer name for the CVM’s operating system. After a CVM is created, you can log into the CVM to view the hostname.</li><li><b>Placement Group</b>: you can add an instance to a placement group as needed to improve service availability. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/15486">Placement Group</a>.</li><li><b>Tag</b>: a tag can be configured to manage CVM resources by categories. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/19548">Tag</a>.</li><li><b>Custom Data</b>: you can configure an instance by specifying custom data, and the configured scripts will run when an instance is started. If multiple CVMs are purchased at a time, the custom data will run on all CVMs. The Windows operating system supports the PowerShell format and a maximum of 16 KB raw data. For details, see <a href="https://intl.cloud.tencent.com/document/product/213/17525">Custom Data</a>.</br><b>Note</b>: custom data configuration supports only public images on Windows. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/19670#cloudbase-init">cloudbase-init</a>.</li></ul></td></tr>
</table>
2. Click **Next: Confirm Configuration** to open the configuration information confirmation page.

## Confirming the configuration information

1. Check the information of the CVM to be purchased and the cost details of each configuration item.
2. Click **Purchase** and complete the payment. You can then check your CVM by logging into the [CVM Console](https://console.cloud.tencent.com/cvm).
Information such as the instance name, public IP address, private IP address, login username, and initial login password of the CVM will be sent to your account via [Internal Messages](https://console.cloud.tencent.com/message). You can log into and manage instances based on the information. To ensure CVM security, change your login password as soon as possible.

## Logging into and connecting the instance

After completing CVM operations, you can log into your CVM in the Tencent Cloud console, and perform operations such as building a site as needed.
Select the method for logging into the CVM in the Tencent Cloud console as needed:
- [Log in to the Windows instance using the RDP file (recommended)](https://intl.cloud.tencent.com/document/product/213/5435)
- [Logging into Windows Instance via Remote Desktop](https://intl.cloud.tencent.com/document/product/213/32498)

## Formatting and partitioning the data disk

If you added a data disk when [selecting the instance type](#SelectType), you need to format and partition the data disk after logging into the CVM instance. **If you did not add any data disk, skip this step.**
Select the appropriate operations guide according to the disk capacity and the CVM operating system.
- For a disk whose capacity is less than 2 TB:
[Initializing a Cloud Disk (Windows)](https://intl.cloud.tencent.com/document/product/362/6734)
- For a disk whose capacity is greater than or equal to 2 TB:
[Initializing a Cloud Disk (Windows)](https://intl.cloud.tencent.com/document/product/362/6735)

For more operations, see [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596).
