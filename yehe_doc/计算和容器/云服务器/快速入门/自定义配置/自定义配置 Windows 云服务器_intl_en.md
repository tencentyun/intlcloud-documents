Besides the quick configuration template, you can also create CVMs with custom configurations as needed. 


## Registration

Before using a CVM instance, you need to perform the following operations:
1. A new user needs to [sign up](https://www.tencentcloud.com/account/register) for an account on the Tencent Cloud website. For detailed directions, see [Signing Up](https://www.tencentcloud.com/document/product/378/17985).
2. Visit the [Tencent Cloud CVM introduction page](https://www.tencentcloud.com/products/cvm) and click **Buy Now**.


## Basic Configuration[](id:SelectType)

<dx-alert infotype="notice" title="">
For accounts that are making purchases for the first time, the **Quick Configuration** page appears by default. For accounts that have made purchases before, the **Custom Configuration** page appears by default. If you have never purchased a CVM instance, select **Custom Configuration**.
</dx-alert>

1. Configure the following information.
<table>
  <tr>
	<th style="width: 20%">Item</th>
	<th style="width: 12%">Required</th>
	<th>Description</th>
  </tr>
  <tr>
	<td>
	  <a href="https://intl.cloud.tencent.com/document/product/213/2180">Billing Mode</a>
	</td>
	<td>Yes</td>
	<td>Select one as needed:
	<ul>
	  <li>
	  <b>Pay-as-you-go</b>: It is an elastic billing method of CVM applicable to scenarios such as e-commerce flash sales, where demand will fluctuate significantly in an instant.</li>
	  <li>
	  <b>Spot instance</b>: It is a new instance operation mode applicable to scenarios such as big data computing and online website service using load balancing. Its general price range is 10%–20% of a pay-as-you-go instance.</li>
	</ul></td>
  </tr>
  <tr>
	<td>Region</td>
	<td>Yes</td>
	<td>Select the region closest to your users to minimize the access latency and improve the access speed</td>
  </tr>
  <tr>
	<td>AZ</td>
	<td>Yes</td>
	<td>Select one as needed.
	<br />If you want to purchase multiple CVM instances, we recommend you select different AZs to implement disaster recovery. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/6091">Regions and AZs</a>.</td>
  </tr>
	<tr>
	<td>Instance</td>
	<td>Yes</td>
	<td>
	Tencent Cloud provides different instance types based on the underlying hardware. For optimal performance, we recommend you use instance types of the latest generation.
	<br />For more information on instances, see <a href="https://intl.cloud.tencent.com/document/product/213/11518">Instance Types</a>.</td> 
  </tr>
	<tr>
	<td>Image</td>
	<td>Yes</td>
	<td>Tencent Cloud provides public images, custom images, and shared images. For more information on images, see <a href="https://intl.cloud.tencent.com/document/product/213/4941">Image Types</a>. 
	<br />We recommend new Tencent Cloud users select a public image.</td>
  </tr>
	 <tr>
	<td>
	  <a href="https://intl.cloud.tencent.com/document/product/362/31636">System disk</a>
	</td>
	<td>Yes</td>
	<td>It is used for OS installation and defaults to 50 GB.
	<br />Available cloud disk types vary by region. Select one as instructed on the page.
	<br />For more information on cloud disks, see <a href="https://intl.cloud.tencent.com/document/product/362/31636">Cloud Disk Types</a>.</td> 
  </tr>
  <tr>
	<td>
	  <a href="https://intl.cloud.tencent.com/document/product/362/31636">Data disk</a>
	</td>
	<td>No</td>
	<td>It is used to scale up the storage capacity of the CVM instance to ensure high efficiency and reliability. It is not added by default.
	<br />For more information on cloud disks, see <a href="https://intl.cloud.tencent.com/document/product/362/31636">Cloud Disk Types</a>.</td> 
  </tr>
  <tr>
	<td>Scheduled Snapshot</td>
	<td>No</td>
	<td>A scheduled snapshot policy can be set for the system disk or data disk. For more information, see <a href="https://intl.cloud.tencent.com/document/product/362/35238">Scheduled Snapshots</a>.</td> 
  </tr>
	<tr>
	<td>Quantity</td>
	<td>Yes</td>
	<td>It indicates the quantity of CVM instances to be purchased.</td>
  </tr>
</table>


2. Click **Next: Set Network and CVM** to enter the instance settings page.




## Network and CVM
1. Configure the following information as prompted by the page:
<table>
  <tr>
	<th style="width: 20%">Item</th>
	<th style="width: 12%">Required</th>
	<th>Description</th>
  </tr>
	 <tr>
	<td>Network</td>
	<td>Yes</td>
	<td>
	It is a logically isolated network space built in Tencent Cloud. A VPC includes at least one subnet. The system provides a default VPC and subnet for each region.
	<br />If the existing VPC or subnet does not meet your requirements, you can create a VPC or subnet in the VPC console.
	<br />
	<b>Note</b>:
	<ul>
	  <li>By default, resources in the same VPC are interconnected over the private network.</li>
	  <li>When purchasing a CVM instance, make sure that the CVM instance and its subnet are in the same AZ.</li>
	</ul></td>
  </tr>
  <tr>
	<td>Public IP</td>
	<td>No</td>
	<td>	If your CVM instance needs to access the public network, you need to assign a public IP for it. You can assign the public IP when creating the CVM instance or configure an <a href="https://intl.cloud.tencent.com/document/product/213/5733">EIP</a> after the creation.</td>
	</tr>
	<tr>
	<td>Bill-by-bandwidth mode</td>
	<td>No</td>
	<td>	Tencent Cloud provides two network billing modes. You can select one as needed.
	<ul>
	  <li>
	  <b>Bill-by-traffic</b>: Billing is based on traffic that is actually used. You can specify a peak bandwidth to prevent charges incurred by unexpected traffic. Packet loss will occur when the instantaneous bandwidth exceeds this value. This is applicable to scenarios where the network connection fluctuates significantly.</li>
	  <li>
	  <b>Bill-by-bandwidth package</b>: Select this aggregated billing mode when your public network instances have traffic peaks at different times. It is applicable to large-scale businesses where traffic can be staggered between different instances using the public network.
	  <br />BWP is currently in beta test. To try it out, <a href="https://console.intl.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</li> 
	</ul>For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/10578">Public Network Billing</a>.
	</td>
  </tr>
	<tr>
	<td>Bandwidth value</td>
	<td>No</td>
	<td>You can set the maximum public network bandwidth of the CVM instance as needed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/12523">Public Network Bandwidth Cap</a>.</td>
	</tr>
  <tr>
	<td>Security group</td>
	<td>Yes</td>
	<td>Used to configure the network access policies for one or more CVM instances.
	<br/>
	<b>Make sure that login port 3389 is open. </b>For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/12452">Security Group</a>.</td> 
  </tr>
	<tr>
	<td>Tag</td>
	<td>No</td>
	<td>You can add tags for the CVM instance as needed, which can be used to categorize, search for, and aggregate cloud resources. For more information, see <a href="https://intl.cloud.tencent.com/document/product/651/13334">Overview</a>.</td>
  </tr>
	<tr>
	<td>Instance name</td>
	<td>No</td>
	<td>The name of the CVM to be created.
	<br/>It is user-defined. We recommend <b>CVM-01</b>.</td>
  </tr>
  <tr>
	<td>Login Methods</td>
	<td>Yes</td>
	<td>Configure the method to log in to the CVM as needed.
	<ul>
	  <li>
	  <b>Set Password</b>: Customize the password for logging in to the instance.</li>
	  <li>
	  <b>Random Password</b>: A password will be automatically generated and sent to you in <a href="https://console.cloud.tencent.com/message">Message Center</a>.</li>
	</ul></td>
  </tr>
	<tr>
	<td>Instance Termination Protection</td>
	<td>No</td>
	<td>It is not enabled by default. You can enable it as needed. Then, you cannot terminate an instance in the console or via the API. For more information, see <a href="https://www.tencentcloud.com/document/product/213/47383">Enabling Instance Termination Protection</a>.</td>
  </tr>
  <tr>
	<td>Security enhancement</td>
	<td>No</td>
	<td>By default, security service is enabled for free to help you build a CVM security system to prevent data leakage.</td>
  </tr>
  <tr>
	<td>Cloud Monitoring</td>
	<td>No</td>
	<td>
	CM is activated by default. It provides comprehensive CVM data monitoring, smart data analysis, real-time fault alarms, and custom data reports to precisely monitor Tencent Cloud services and the health conditions of CVM instances.</td>
  </tr>
	<tr>
	<td>Automation Assistant</td>
	<td>No</td>
	<td>It is enabled free of charge by default. As the native Ops and deployment tool of CVM, it can automatically run shell commands in batches and complete various tasks such as running automated Ops scripts, polling processes, installing/uninstalling software, updating applications, and installing patches, without the need to connect to the instance remotely.</td>
  </tr>
  <tr>
	<td>Advanced settings</td>
	<td>No</td>
	<td>Configure additional settings for the instance as needed.
	<ul>
	  <li>
	  <b>Hostname</b>: You can customize the name of the computer in the CVM operating system. After a CVM instance is created, you can log in to it to view the hostname.</li>
		<li>
	  <b>Project</b>: The default project is selected. You can select an existing project as needed to manage different CVM instances.</li>
	  <li>
	  <b>CAM Role</b>: You can set a role and use it to grant role entity the permissions to access CVM services and resources and perform operations in Tencent Cloud. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/213/45917">Managing Roles</a>.</li>
	  <li>
	  <b>Placement Group</b>: You can add the instances to placement groups to improve your business availability. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/213/15486">Placement Group</a>.</li>
	  <li> <b>Custom Data</b>: You can configure an instance by specifying custom data, and the configured scripts will run when an instance is started. If multiple CVM instances are purchased at a time, the custom data will run on all of them. The Windows operating system supports the PowerShell format and a maximum of 16 KB of raw data. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/17526">Configuring Custom Data (Windows CVM)</a>.
	  <br />
	  <b>Note</b>: Custom data configuration applies only to certain Windows public images. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/17526#.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9">Configuring Custom Data (Windows CVM)</a>.</li>
	</ul></td>
  </tr>
</table>


2. Click **Next: Confirm Configuration** to enter the configuration information confirmation page.





## Confirming the Configuration
1. Check the configuration items and billing details of the CVM instance to be purchased.
2. Read and indicate your consent to the **Tencent Cloud Terms of Service**.
3. You can perform the following operations as needed:
    - Select **Save as Launch Template** to save the configuration of this instance as a launch template, based on which you can quickly create instances. For more information, see [Managing Instance Startup Template](https://intl.cloud.tencent.com/document/product/213/45221).
    - Select **Generate API Explorer Reusable Script** to generate the OpenAPI reusable script code for instance creation corresponding to the selected configuration. You can save the code for purchasing CVM instances with the same configuration. For more information, see [Generating API Explorer Reusable Scripts to Create Instances](https://intl.cloud.tencent.com/document/product/213/39811).
4. Click **Buy Now** or **Activate** and make the payment.
After making the payment, you can log in to the [CVM console](https://console.cloud.tencent.com/cvm) to check your CVM instance.
Information such as the instance name, public IP address, private IP address, login username, and initial login password of the CVM will be sent to your account through the [Message Center](https://console.cloud.tencent.com/message). You can use this information to log in to and manage your instances. To ensure the security of your CVM, please change your CVM login password as soon as possible.

## Logging in to the Instance

After completing CVM operations, you can log in to your CVM on the Tencent Cloud console and perform operations such as building a site as needed.
Select a method for logging in to the CVM on the Tencent Cloud console as needed:
- [Log in to a Windows instance using the standard method (recommended)](https://intl.cloud.tencent.com/document/product/213/41018)
- [Log in to a Linux instance using the RDP file](https://intl.cloud.tencent.com/document/product/213/5435)
- [Log in to a Windows instance using remote desktop](https://intl.cloud.tencent.com/document/product/213/32498)

## Disk Formatting and Partitioning

If you added a data disk when [selecting the instance type](#SelectType), you need to format and partition the data disk after logging in to the CVM instance. **If you have not added any data disks, skip this step.**
Select the appropriate operations guide according to the disk capacity and the CVM operating system.
- For a disk smaller than 2 TB:
[Initializing a Cloud Disk (Windows)](https://intl.cloud.tencent.com/document/product/362/31597)
- For a disk equal to or larger than 2 TB:
[Initializing a Cloud Disk (Windows)](https://intl.cloud.tencent.com/document/product/362/31598)

For more operations, see [Initialization Scenarios](https://intl.cloud.tencent.com/document/product/362/31596).
