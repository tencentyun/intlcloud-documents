## Overview 

This document describes three types of images supported by TKE and their respective use cases and instructions. For more information, see [Image Types](https://intl.cloud.tencent.com/document/product/213/4941).

- **Public image**: They are images officially provided by Tencent Cloud. Each image contains an operating system and initialization components provided by Tencent Cloud, and is available to all users.
- **Custom image**: It is created by using the image creation feature or imported by using the image import feature. A custom image is only available to the creator and the people they share it with. It is a non-standard environment that doesn't come with official support and ongoing maintenance from Tencent Cloud.
- **Market image**: It is provided for specific use cases, such as [qGPU sharing](https://intl.cloud.tencent.com/document/product/457/42973). It is available to all users and integrated with certain applications in addition to the operating system.


## Notes

- There are two levels of operating systems, including **cluster level** and **node pool level**.
  - OS configured at the cluster level is used when creating a node, adding an existing node, and upgrading a node in a cluster.
  - When adding existing nodes or expanding the node capacity inside the node pool, you will use the OS at the node pool level.
- Changes to the OS only apply to new nodes and reinstalled nodes, **but not existing nodes**.

## List of Public Images Supported by TKE

TKE offers the following **public images** that you can choose as needed.

>? Whenever TKE plans to adjust the image logic, we will notify you **at least one week** in advance via Message Center, SMS, and email.
>Image logic changes will not affect the existing nodes previously created by using an earlier image. For better results, we recommend you use a later basic image.


<table>
<thead>
  <tr>
    <th>Image ID</th>
    <th>OS Name</th>
    <th>OS Name Displayed in the Console</th>
    <th>OS Type</th>
    <th>Release Status</th>
    <th>Notes</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><a href="https://console.cloud.tencent.com/cvm/image/detail?rid=16&id=img-eb30mz89">img-eb30mz89</a></td>
    <td>tlinux3.1x86_64</td>
    <td>TencentOS Server 3.1 (TK4)</td>
    <td>Tencent OS Server</td>
    <td>Full release</td>
    <td>The latest release version of Tencent OS Server is recommended<br>Kernel version: 5.4.119<br>You need to install the GPU driver manually</td>
  </tr>
  <tr>
    <td><a href="https://console.cloud.tencent.com/cvm/image/detail?rid=4&id=img-hdt9xxkt">img-hdt9xxkt</a></td>
    <td>tlinux2.4x86_64</td>
    <td>TencentOS Server 2.4<br>Formerly known as Tencent linux release 2.4 (Final)</td>
    <td>Tlinux</td>
    <td>Full release</td>
    <td>Kernel version: 4.14.105</td>
  </tr>
  <tr>
    <td><a href="https://console.cloud.tencent.com/cvm/image/detail/8/PUBLIC_IMAGE/img-22trbn9x">img-22trbn9x</a></td>
    <td>ubuntu20.04x86_64</td>
    <td>Ubuntu Server 20.04.1 LTS 64bit</td>
    <td>Ubuntu</td>
    <td>It is in beta. To join it, please <a href="https://console.intl.cloud.tencent.com/workorder/category">submit a ticket</a> to apply.</td>
    <td>Ubuntu 20.04.1 public kernel</td>
  </tr>
  <tr>
    <td><a href="https://console.cloud.tencent.com/cvm/image/detail?rid=1&id=img-pi0ii46r">img-pi0ii46r</a></td>
    <td>Ubuntu18.04.1x86_64</td>
    <td>Ubuntu 18.04 LTS 64bit</td>
    <td>Ubuntu</td>
    <td>Full release</td>
    <td>Ubuntu 18.04.1 public kernel</td>
  </tr>
  <tr>
    <td><a href="https://console.cloud.tencent.com/cvm/image/detail/8/PUBLIC_IMAGE/img-25szkc8t">img-25szkc8t</a></td>
    <td>centos8.0x86_64</td>
    <td>CentOS 8.0</td>
    <td>CentOS</td>
    <td>It is in beta. To join it, please <a href="https://console.intl.cloud.tencent.com/workorder/category">submit a ticket</a> to apply.</td>
    <td>CentOS 8.0 public kernel</td>
  </tr>
  <tr>
    <td><a href="https://console.cloud.tencent.com/cvm/image/detail?rid=1&id=img-9qabwvbn">img-9qabwvbn</a></td>
    <td>CentOS7.6.0_x64</td>
    <td>CentOS 7.6</td>
    <td>CentOS</td>
    <td>Full release</td>
    <td>CentOS 7.6 public kernel</td>
  </tr>
</tbody>
</table>
