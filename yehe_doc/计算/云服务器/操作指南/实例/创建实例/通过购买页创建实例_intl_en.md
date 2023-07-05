## Overview

This document guides you through how to create a Tencent Cloud Virtual Machine (CVM) instance using the custom configuration mode as an example.

## Preparations

Before creating a CVM instance, you need to complete the following steps:
- [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).
- To create a CVM instance whose network type is virtual private cloud (VPC), you need to [create a VPC](https://intl.cloud.tencent.com/document/product/215/31805) in the target region and [create a subnet](https://intl.cloud.tencent.com/document/product/215/31806) in the target availability zone under the VPC.
- If you do not use the default project, you need to [create a project](https://intl.cloud.tencent.com/document/product/378/34726).
- If you do not use the default security group, you need to [create a security group](https://intl.cloud.tencent.com/document/product/213/34271) in the target region and add a security group rule that meets your business requirements.
- To bind an SSH key pair when creating a Linux instance, you need to [create an SSH key](https://intl.cloud.tencent.com/document/product/213/16691) for the target project.
- To create a CVM instance with a custom image, you need to [create a custom image](https://intl.cloud.tencent.com/document/product/213/4942) or [import an image](https://intl.cloud.tencent.com/document/product/213/4945).

## Directions

1. Log in to [Tencent Cloud](https://intl.cloud.tencent.com). Select **Products** > **Compute and Container**> **Compute** > **[Cloud Virtual Machine](https://intl.cloud.tencent.com/products/cvm)**. Click **Buy Now** to enter the CVM purchase page.
 - **[Custom Configuration](https://buy.intl.cloud.tencent.com/cvm?regionId=1&projectId=-1&templateCreateMode=createLt)**: It is suitable for specific scenarios and makes it easier for you to purchase CVM instances as needed.
2. Configure the following information as prompted by the page:
<table>
  <tr>
	<th style="width: 20%">Type</th>
	<th style="width: 12%">Required</th>
	<th>Configuration Description</th>
  </tr>
  <tr>
	<td>Billing mode</td>
	<td>Yes</td>
	<td>Select one as needed:
	<ul>
	  <li>
	  <b>Pay-as-you-go</b>: It is an elastic billing method of CVM applicable to scenarios such as e-commerce flash sales, where demand will fluctuate significantly in an instant.</li>
	  <li>
	  <b>Spot instance</b>: It is a new instance operation mode applicable to scenarios such as big data computing and online website service using load balancing. Its general price range is 10%–20% of a pay-as-you-go instance.</li>
	  - 20%。</li>
	</ul>For billing details, see <a href="https://intl.cloud.tencent.com/document/product/213/2180">Billing Plans</a>.</td> 
  </tr>
  <tr>
	<td>Region/Availability Zone</td>
	<td>Yes</td>
	<td>
	<ul>
	  <li>
	  <b>Region</b>: We recommend you select the region closest to your end users to minimize the access latency and improve the access speed.</li>
	  <li>
	  <b>Availability zone</b>: Select one as needed.
	  <br />If you want to purchase multiple CVM instances, we recommend you select different AZs to implement disaster recovery.</li>
	</ul>For more information on regions and AZs, see <a href="https://intl.cloud.tencent.com/document/product/213/6091">Regions and AZs</a>.</td> 
  </tr>
	<tr>
	<td>Instance</td>
	<td>Yes</td>
	<td>Tencent Cloud provides different instance types based on the underlying hardware.
	<br />For more information on instances, see <a href="https://intl.cloud.tencent.com/document/product/213/11518">Instance Types</a>.</td> 
  </tr>
	<tr>
	<td>Image</td>
	<td>Yes</td>
	<td>Tencent Cloud provides public images, custom images, and shared images. For more information on images, see <a href="https://intl.cloud.tencent.com/document/product/213/4941">Image Types</a>.</td> 
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

3. Click **Next: Set Network and CVM** to enter the instance settings page.
4. Configure the following information as prompted by the page:
<table>
  <tr>
	<th style="width: 20%">Type</th>
	<th style="width: 12%">Required</th>
	<th>Configuration Description</th>
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
	<td>If your CVM instance needs to access the public network, you need to assign a public IP for it. You can assign the public IP when creating the CVM instance or configure an <a href="https://intl.cloud.tencent.com/document/product/213/5733">EIP</a> after the creation.	<br><b>Note</b>: 
	<ul>
	  <li>The dedicated public IP that is assigned free of charge cannot be unbound from the instance. To unbind this IP address, convert it to an EIP first. For more information on EIPs, see <a href="https://intl.cloud.tencent.com/document/product/213/5733">Elastic IP (EIP)</a>.</li>
	  <li>No dedicated public IP can be assigned in the following two cases, subject to the information on the purchase page:
	  <ul>
		<li>The IP resources have been sold out.</li>
		<li>Resources are only available in certain regions.</li>
	  </ul>
	</td>
	</tr>
	<tr>
	<td>Bill-by-bandwidth mode</td>
	<td>Yes</td>
	<td>
	<br />Tencent Cloud provides two network billing modes. Configure a value greater than 0 Mbps as needed.
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
	<td>
	<ul>
	  <li>If there is no available security group, you can choose <b>New security group</b>.</li><li>If there are available security groups, you can choose <b>Existing Security Groups</b>.</li></ul>For more information on security groups, see <a href="https://intl.cloud.tencent.com/document/product/213/12452">Security Group</a>.</td>
  </tr>
  <tr>
	<td>Tag</td>
	<td>No</td>
	<td>You can add tags for the instance as needed, which can be used to categorize, search for, and aggregate cloud resources. For more information, see <a href="https://intl.cloud.tencent.com/document/product/651/13334">Overview</a>.</td>
  </tr>
  <tr>
	<td>Instance name</td>
	<td>No</td>
	<td>You can customize the name of the CVM instance to be created.
	<br />
	<ul>
	  <li>If no instance name is specified, <b>Unnamed</b> will be used by default.</li><li>An instance name can contain up to 128 characters. <a href="https://intl.cloud.tencent.com/document/product/213/32020">Batch sequential naming or pattern string-based naming</a> is also supported.</li>
	</ul>
	<b>Note</b>: This name is displayed only in the console. It is not the hostname of the CVM instance.</td>
  </tr>
  <tr>
	<td>Login Methods</td>
	<td>Yes</td>
	<td>Configure the method to log in to the CVM as needed.
	<ul>
	  <li>
	  <b>Set Password</b>: Customize the password for logging in to the instance.</li>
	  <li>
	  <b>SSH Key Pair (only for Linux instances)</b>: Associate the instance with an SSH key to ensure secure login to the CVM instance.<br />If no key is available or existing keys are inappropriate, click <b>Create Now</b> to create a key. For more information on SSH keys, see <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSH Keys</a>.</li>
	  <li>
	  <b>Random Password</b>: A password will be automatically generated and sent to you in <a href="https://console.cloud.tencent.com/message">Message Center</a>.</li> 
	</ul></td>
  </tr>
  <tr>
	<td>Instance Termination Protection</td>
	<td>No</td>
	<td>It is not enabled by default. You can enable it as needed. Then, you cannot terminate an instance in the console or via the API. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/47383">Enabling Instance Termination Protection</a>.</td>
  </tr>
  <tr>
	<td>Security Enhancement</td>
	<td>No</td>
	<td>By default, Anti-DDoS and Cloud Workload Protection are enabled free of charge to help you build a CVM security system to prevent data leakage.</td>
  </tr>
  <tr>
	<td>Tencent Cloud Observability Platform</td>
	<td>No</td>
	<td>
	CM is activated by default. You can install add-ons to get CVM monitoring metrics and display them in visual charts. You can also specify custom alarm thresholds. In addition, you can configure three-dimensional CVM data monitoring, smart data analysis, real-time fault alarms, and custom data reports to precisely monitor Tencent Cloud services and the health conditions of CVM instances.</td>
  </tr>
  <tr>
	<td>Advanced Settings</td>
	<td>No</td>
	<td>Configure additional settings for the instance as needed.
	<ul>
	  <li>
	  <b>Hostname</b>: You can customize the name of the computer in the CVM operating system. After a CVM instance is created, you can log in to it to view the hostname.</li>
		<li>
	  <b>Project</b>: The default project is selected. You can select an existing project as needed to manage different CVM instances.</li>
	  <li>
	  <b>CAM Role</b>: You can set a role and use it to grant a role entity the permissions to access CVM services and resources and perform operations in Tencent Cloud. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/213/45917">Managing Roles</a>.</li>	  
	  <li>
	  <b>Placement Group</b>: You can add the instances to placement groups to improve your business availability. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/213/15486">Placement Group</a>.</li> 
	  <li>
	  <b>Custom Data</b>: You can configure an instance by specifying custom data, and the configured scripts will run when an instance is started. If multiple CVM instances are purchased at a time, the custom data will run on all of them. The Linux operating system supports the Shell format, while the Windows operating system supports the PowerShell format and a maximum of 16 KB of raw data. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/17525">Configuring Custom Data (Linux CVM)</a>.
	  <br/>
	  <b>Note</b>: Custom data configuration applies only to certain public images with the cloud-init service. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/19670">Cloud-Init & Cloudbase-Init</a>.</li> 
	  <a href="https://intl.cloud.tencent.com/document/product/213/19670">Cloud-Init</a>。</li>
	</ul></td>
  </tr>
</table>

5. Click **Next: Confirm Configuration** to enter the configuration information confirmation page.
6. Validate the information of the CVM to be purchased and the cost details of each configuration item.
7. Read and indicate your consent to the **Tencent Cloud Terms of Service**.
8. You can perform the following operations as needed:
 - Select **Save as Launch Template** to save the configuration of this instance as a launch template, based on which you can quickly create instances. For more information, see [Managing Instance Startup Template](https://intl.cloud.tencent.com/document/product/213/45221).
 - Select **Generate API Explorer Reusable Script** to generate the OpenAPI reusable script code for instance creation corresponding to the selected configuration. You can save the code for purchasing CVM instances with the same configuration. For more information, see [Generating API Explorer Reusable Scripts to Create Instances](https://intl.cloud.tencent.com/document/product/213/39811).
9. Click **Buy Now** or **Activate** and make the payment.
After making the payment, you can log in to the [CVM console](https://console.cloud.tencent.com/cvm) to check your CVM instance.
Information such as the instance name, public IP address, private IP address, login username, and initial login password of the CVM will be sent to your account through the [Message Center](https://console.cloud.tencent.com/message). You can use this information to log in to and manage your instances. To ensure the security of your CVM, please change your CVM login password as soon as possible.
