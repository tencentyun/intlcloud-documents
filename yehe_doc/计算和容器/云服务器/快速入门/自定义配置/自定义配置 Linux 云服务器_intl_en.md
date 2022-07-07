Compared with using quick configuration to create a Tencent Cloud Virtual Machine (CVM), custom configuration provides more image platforms and advanced configurations for storage, bandwidth, and security group. You can select the configuration method as needed. This document uses custom configuration as an example.

## Registration and Verification

Before using a CVM instance, you need to perform the following operations:
1. Sign up for a Tencent Cloud account and complete identity verification.
A new user needs to [sign up](https://intl.cloud.tencent.com/register) for an account on the Tencent Cloud website. For details, see [Signing up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).
2. Go to the [Tencent Cloud CVM introduction page](https://intl.cloud.tencent.com/zh/products/cvm) page and click **Buy Now**.


## Selecting Model[](id:SelectType)

<dx-alert infotype="notice" title="">
For accounts that are making purchases for the first time, the **Quick Configuration** page appears by default. For accounts that have made purchases before, the **Custom Configuration** page appears by default. If you have never purchased a CVM instance, choose **Custom Configuration**.
</dx-alert>

1. Configure the following information as prompted by the page:
![](https://main.qcloudimg.com/raw/07493412dd043911fe8aa3ecb0d0bcd4.png)
<table>
<tr><th style="width: 20%">Category</th><th style="width: 12%">Required/Optional</th><th>Configuration Description</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/213/2180">Billing Plans</a></td><td>Required</td><td>Select based on your actual needs:<ul><li><b>Pay-as-you-go</b>: An elastic billing method applicable to scenarios such as e-commerce flash sales, where demand will fluctuate significantly in an instant.</li><li><b>Spot instance</b>: A new instance operation mode applicable to scenarios such as big data computing and online website service using load balancing. Its general price range is 10%-20% of a pay-as-you-go instance.</li></ul></td></tr>
<tr><td>Region</td><td>Required</td><td>We recommend you select a region closest to your customer to reduce access latency and increase access speed.</td></tr>
<tr><td>Availability Zone</td><td>Required</td><td>Select an availability zone as needed.</br>If you want to purchase multiple CVM instances, we recommend you select different availability zones to implement disaster recovery.</td></tr>
<tr><td>Network</td><td>Required</td><td>A logically isolated network space built in Tencent Cloud. A virtual private cloud (VPC) includes at least one subnet. The system provides a default VPC and subnet for each region.</br>
If the existing VPC or subnet does not meet your requirements, you can create a VPC or subnet on the VPC console.</br><b>Note</b>:<ul><li>Resources in the same VPC can be shared within the private network.</li><li>When purchasing the CVM instance, ensure that the CVM instance and the subnet where the CVM instance is created have the same availability zones.</li></ul></td></tr>
<tr><td>Instance</td><td>Required</td><td>Tencent Cloud provides different instance types based on the underlying hardware. For optimal performance, we recommend you use the instance types of the latest generation.</br>For more information on instances, see <a href="https://intl.cloud.tencent.com/document/product/213/11518">Instance Types</a>.</td></tr>
<tr><td>Image</td><td>Required</td><td>Tencent Cloud provides public images, custom images, and shared images. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/4941">Image Types Overview</a>.</br>If you have just started using Tencent Cloud, we recommend you choose public images.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">System Disk</a></td><td>Required</td><td>Used to install the operating system. Its default capacity is 50 GB.</br>Available Cloud Block Storage (CBS) types vary with regions. Select a value as instructed by the page.</br>For more information on CBS, see <a href="https://intl.cloud.tencent.com/document/product/362/31636">Cloud Disk Types</a>.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">Data Disk</a></td><td>Optional</td><td>Used to scale up the storage capacity of the CVM instance to ensure high efficiency and reliability. CBS data disks are not added by default.</br>For more information on CBS, see <a href="https://intl.cloud.tencent.com/document/product/362/31636">CBS Types</a>.</td></tr>
<tr><td>Scheduled Snapshot</td><td>Optional</td><td>A scheduled snapshot policy can be set for the system disk or data disk. For more information, see <a href="https://intl.cloud.tencent.com/document/product/362/35238">Scheduled Snapshots</a>.</td></tr>
<tr><td>Public Network Bandwidth</td><td>Required</td><td>Tencent Cloud provides two network billing modes. Set a value as required.<ul><li><b>Bill-by-bandwidth</b>: Select a fixed bandwidth. Packet loss will occur when the bandwidth exceeds this value. This is applicable to scenarios where the network connection fluctuates slightly.</li><li><b>Bill-by-traffic</b>: Billing is based on traffic that is actually used. You can specify a peak bandwidth to prevent charges incurred by unexpected traffic. Packet loss will occur when the instantaneous bandwidth exceeds this value. This is applicable to scenarios where the network connection fluctuates significantly.</li></ul></td></tr>
<tr><td>Quantity</td><td>Required</td><td>Number of CVM instances to be purchased.</td></tr> 
</table>



2. Click **Next: Complete Configuration** to enter the CVM configuration page.

## Configuring CVM
1. Configure the following information as prompted by the page:
![](https://main.qcloudimg.com/raw/44493e285aee4d9523e009b7690fc616.png)
<table>
  <tr>
	<th style="width: 20%">Type</th>
	<th style="width: 12%">Required</th>
	<th>Configuration Description</th>
  </tr>
  <tr>
	<td>Security Group</td>
	<td>Yes</td>
	<td>Used to configure the network access policies for one or more CVM instances.
	<br />
	<b>Make sure that login port 22 is open. </b>For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/12452">Security Group</a>.</td> 
	<a href="https://intl.cloud.tencent.com/document/product/213/12452">Security Group</a>。</td>
  </tr>
  <tr>
	<td>Projects</td>
	<td>Yes</td>
	<td>The default project is selected. You can select an existing project as needed to manage different CVM instances.</td>
  </tr>
  <tr>
	<td>Tag</td>
	<td>No</td>
	<td>You can add tags for the instance as needed, which are used to categorize, search for, and aggregate cloud resources. For more information, see <a href="https://intl.cloud.tencent.com/document/product/651/13334">Overview</a>.</td>
  </tr>
  <tr>
	<td>Instance Name</td>
	<td>No</td>
	<td>The name of the CVM instance to be created.
	<br />It is user-defined. We recommend **CVM-01**.</td>
  </tr>
  <tr>
	<td>Login Methods</td>
	<td>Yes</td>
	<td>Configure the method to log in to the CVM instance as needed.
	<ul>
	  <li>
	  <b>Set Password</b>: Customize the password for logging in to the instance.</li>
	  <li>
	  <b>SSH Key Pair</b>: Associate the instance with an SSH key to ensure secure login to the CVM instance.
		<br />If no key is available or existing keys are inappropriate, click <b>Create Now</b> to create a key. For more information on SSH keys,
	  see <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSH Keys</a>.</li>
	 <tr>
	<td>Instance Termination Protection</td>
	<td>No</td>
	<td>It is disabled by default. You can enable it as needed. Then, you cannot terminate an instance in the console or via the API. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/47383">Enabling Instance Termination Protection</a>.</td>
     <li>
	  <b>Random Password</b>: A password will be automatically generated and sent to you in <a href="https://console.cloud.tencent.com/message">Message Center</a>.</li>
	</ul></td>
  </tr>
  <tr>
	<td>Security Service</td>
	<td>No</td>
	<td>By default, security service is enabled for free to help you build a CVM security system to prevent data leakage.</td>
  </tr>
  <tr>
	<td>Cloud Monitor</td>
	<td>No</td>
	<td>
	By default, cloud monitoring is enabled for free. It provides comprehensive CVM data monitoring, intelligent data analysis, real-time fault alarms, and custom data reports to precisely monitor Tencent Cloud services and the health conditions of CVM instances.</td>
  </tr>
	<tr>
	<td>Automation Assistant</td>
	<td>No</td>
	<td>It is enabled for free by default. As the native Ops and deployment tool of CVM, it can automatically run shell commands in batches and complete various tasks such as running automated Ops scripts, polling processes, installing/uninstalling software, updating applications, and installing patches, without the need to connect to the instance remotely.</td>
  </tr>
	<tr>
	<td>Advanced Settings</td>
	<td>No</td>
	<td>Configure additional settings for the instance as needed.
	<ul>
	  <li>
	  <b>Hostname</b>: You can customize the name of the computer in the CVM operating system. After a CVM instance is created, you can log in to it to view the hostname.</li>
	  <li>
	  <b>CAM Role</b>: You can set a role and use it to grant role entity the permissions to access CVM services and resources and perform operations in Tencent Cloud. For more information about the settings, see <a href="https://intl.cloud.tencent.com/document/product/213/38290">Managing Roles</a>.</li>
	  <li>
	  <b>Placement Group</b>: You can add the instances to placement groups to improve your business availability. Configure as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/15486">Placement Group</a>.</li>
	  <li>
	  <b>Custom Data</b>: You can configure an instance by specifying custom data, and the configured scripts will run when an instance is launched. If multiple CVM instances are purchased together, the custom data will run on all of them. Linux supports the Shell format and a maximum of 16 KB of raw data. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/17525">Configuring Custom Data (Linux CVM)</a>.
	  <br />
	  <b>Note</b>: Custom data configuration only supports certain public images with the Cloud-Init service. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/19670">Cloud-Init</a>.</li>
	</ul></td>
  </tr>
</table>


2. Click **Next: Confirm Configuration** to enter the configuration information confirmation page.


## Confirming Configuration Information

1. Validate the information of the CVM instance to be purchased and the cost details of each configuration item.
2. Read and select **Agree "Tencent Cloud Service Terms"**.
3. You can perform the following operations as needed:
   - Select **Save as Launch Template** to save the configuration of this instance as a launch template, based on which you can quickly create instances. For more information, see [Managing Instance Startup Template](https://intl.cloud.tencent.com/document/product/213/45221).
   - Select **Generate API Explorer Reusable Script** to generate the OpenAPI reusable script code for instance creation corresponding to the selected configuration. You can save the code for purchasing CVM instances with the same configuration. For more information, see [Generating API Explorer Reusable Scripts to Create Instances](https://intl.cloud.tencent.com/document/product/213/39811).
4. Click **Buy Now** or **Activate** and complete the payment. You can then check your CVM instances in the [CVM console](https://console.cloud.tencent.com/cvm).
Information such as the instance name, public IP address, private IP address, login username, and initial login password of the CVM instance will be sent to your account through the [Message Center](https://console.cloud.tencent.com/message). You can use this information to log in to and manage your instances. To ensure the security of your CVM instance, change your CVM instance login password as soon as possible.

## Logging in and Connecting to Instance

After completing CVM operations, you can log in to your CVM instance in the Tencent Cloud console and perform operations such as building a site as needed.
Select a method for logging in to the CVM instance in the Tencent Cloud console as needed:
- [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436)
- [Logging in to Linux Instances (Remote Login)](https://intl.cloud.tencent.com/document/product/213/32502)
- [Logging in to Linux Instance (SSH Key)](https://intl.cloud.tencent.com/document/product/213/32501)

## Partitioning and formatting the data disk

If you added a data disk when [selecting the instance type](#SelectType), you need to format and partition the data disk after logging in to the CVM instance. **If you have not added any data disks, skip this step.**
Select the appropriate operations guide according to the disk capacity and the CVM operating system.
- For a disk smaller than 2 TB:
 [Initializing a Cloud Disk (Linux)](https://intl.cloud.tencent.com/document/product/362/31597)
- For a disk equal to or larger than 2 TB:
 [Initializing a Cloud Disk (Linux)](https://intl.cloud.tencent.com/document/product/362/31598)

For more operations, see [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596).
