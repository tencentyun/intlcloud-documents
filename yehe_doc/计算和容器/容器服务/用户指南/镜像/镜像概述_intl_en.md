## Overview 

This document describes three types of images supported by TKE and their respective use cases and instructions. For more information, see [Image Types](https://intl.cloud.tencent.com/document/product/213/4941).

- **Public Image**: It is officially provided by Tencent Cloud. Each image contains the basic operating system and the initialized add-ons provided by Tencent Cloud, and is available to all users.
- **Custom Image**: It is created by using the image creation feature or imported by using the image import feature. A custom image is only available to the creator and the people they share it with. It is a non-standard environment that doesn't come with official support and ongoing maintenance from Tencent Cloud.
- **Market Image**: It is provided for specific use cases, such as [qGPU sharing](https://intl.cloud.tencent.com/document/product/457/42973). It is available to all users and integrated with certain applications in addition to the operating system.


## Notes

- There are two levels of operating systems: **cluster level** and **node pool level**.
  - When creating nodes, adding existing nodes, or upgrading nodes within a cluster, you will use the operating system at the cluster level.
  - When adding existing nodes or expanding the node capacity inside the node pool, you will use the operating system at the node pool level.
- Changes to the operating system only apply to new nodes and reinstalled nodes, but **not existing nodes**.

## List of Public Images Supported by TKE

TKE offers the following **public images** that you can choose as needed.

>! Whenever TKE plans to adjust the image logic, we will notify you **at least one week** in advance through the Message Center, SMS, and email.
>Image logic changes will not affect the existing nodes previously created by using an earlier image. For better results, we recommend you use a later basic image.



<table>
	<tr>
	<th>Image ID </th><th>OS Name Displayed in the Console </th><th>OS Type</th><th>Release Status</th><th>Remarks</th>
	</tr>
	<tr>
	<td><a href="https://console.cloud.tencent.com/cvm/image/detail?rid=16&id=img-eb30mz89"> img-eb30mz89 </a></td>
	<td>TencentOS Server 3.1 (TK4)</td>		<td>TencentOS Server</td><td>Official launch</td>	<td> <li><b>We recommend you use</b> the latest release of TencentOS Server. </li> <li>Kernel version: 5.4.119 </li> <li>Automatic installation of the GPU driver is not supported, and you need to install it yourself. </li></td>
</tr>
<tr>
	<td><a href="https://console.cloud.tencent.com/cvm/image/detail?rid=4&id=img-hdt9xxkt">img-hdt9xxkt</a></td>
	<td><b>TencentOS Server 2.4</b>, former name: Tencent Linux release 2.4 (Final)</td>	<td>Tlinux</td><td>Official launch</td>	<td><li>Kernel version: 4.14.105 </li></td>
</tr>
	<tr>
	<td><a href="https://console.cloud.tencent.com/cvm/image/detail/8/PUBLIC_IMAGE/img-22trbn9x"> img-22trbn9x </a></td>
	<td>Ubuntu Server 20.04.1 LTS 64-bit</td>		<td>Ubuntu</td><td>In beta test. <a href="https://console.cloud.tencent.com/workorder/category">Submit a ticket</a> for application.</td>
	<td>Ubuntu 20.04.1 public kernel</td>
</tr>
	<tr>
	<td><a href="https://console.cloud.tencent.com/cvm/image/detail/8/PUBLIC_IMAGE/img-pi0ii46r"> img-pi0ii46r </a></td>
	<td>Ubuntu 18.04 LTS 64-bit</td>		<td>Ubuntu</td><td>Official launch</td>
	<td>Ubuntu 18.04.1 public kernel</td>
</tr>
<tr>
	<td><a href="https://console.cloud.tencent.com/cvm/image/detail/8/PUBLIC_IMAGE/img-25szkc8t">img-25szkc8t</a></td>
	<td> CentOS 8.0 </td>		<td>CentOS</td><td>In beta test. <a href="https://console.cloud.tencent.com/workorder/category">Submit a ticket</a> for application.</td>
	<td>CentOS 8.0 public kernel</td>
</tr>
	<tr>
	<td><a href="https://console.cloud.tencent.com/cvm/image/detail/8/PUBLIC_IMAGE/img-9qabwvbn">img-9qabwvbn</a></td>
	<td> CentOS 7.6 </td>		<td>CentOS</td><td>Official launch</td>
	<td>CentOS 7.6 public kernel</td>
</tr>
</table>
