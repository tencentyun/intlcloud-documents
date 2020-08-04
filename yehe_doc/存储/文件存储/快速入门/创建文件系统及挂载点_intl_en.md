## Overview

You can create a file system and mount target on the file system page in the CFS Console. This document describes in detail how to do so.

## Directions

#### 1. Enter the file system page

Log in to the [CFS Console](https://console.cloud.tencent.com/cfs) and click **File System** on the left sidebar to enter the file system list page.

#### 2. Create a file system and mount target

Click **Create** and configure the following information in the pop-up window. After confirming that everything is correct, click **OK**.

<table>
  <tr>
    <th nowrap="nowrap">Field</th>
    <th>Meaning</th>
  </tr>
  <tr>
    <td>Region</td>
    <td>Select the region where the CFS file system is to be created.</td>
  </tr>
  <tr>
    <td nowrap="nowrap">AZ</td>
    <td>Select the AZ where the CFS file system is to be created.</td>
  </tr>
  <tr>
  <tr>
    <td nowrap="nowrap">Storage class</td>
    <td>Select the needed storage class (standard or high-performance).</td>
  </tr>
  <tr>
    <td nowrap="nowrap">File service protocol</td>
    <td>Select the protocol type for the file system, which can be NFS or CIFS/SMB. Among them, NFS is more suitable for Linux/Unix clients, while CIFS/SMB is more suitable for Windows clients. The beta test for CIFS/SMB file systems has ended, and the schedule for future tests will be announced later. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/582/9553">Notes on CIFS/SMB Beta Test</a>.</td>
  </tr>
  <tr>
    <td nowrap="nowrap">Client type</td>
    <td>Select the type of the client that needs to access the CFS file system, which can be a CVM instance (including TKE and BatchCompute) or a CPM instance. As the two types of instances are in different networks, the system will assign the file system to the specified network according to your client type.</td>
  </tr>
  <tr>
    <td nowrap="nowrap">Network type</td>
    <td>
    <p>VPC or basic network. Please create and mount the file system according to the network type in which your CVM instance resides; otherwise, access may fail as network interconnection is unavailable.</p>
    <li>To allow a file system to be shared by CVM instances in the same VPC, you need to select VPC when creating the file system. If a file system resides in a VPC, only CVM instances in the same VPC can be mounted if no specific network settings are made.</li>
    <li>To allow a file system to be shared by CVM instances in the basic network, you need to select basic network when creating the file system. If a file system resides in the basic network, only CVM instances in the basic network can be mounted if no specific network settings are made.</li>
    <li>If a file system needs to be shared across multiple networks, please see <a href="https://intl.cloud.tencent.com/document/product/582/9764">Cross-network Access to File System</a>.</li>
    </td>
  </tr> 
  <tr>
    <td>Permission group</td>
    <td>Each file system must be bound to a permission group, which specifies the access allowlist and read/write permissions.
    </td>
  </tr>
<tr>
    <td>Tag</td>
    <td>
      <li>If you already have a tag, you can add it to the new file system here;</li>
<li>If you don't have a tag yet, please go to the <a href="https://console.cloud.tencent.com/tag/taglist">Tag Console</a> to create a desired tag and add it to the file system. You can also add tags to the file system after it is created.</li>
    </td>
  </tr>
</table>



#### 3. Get the mount target information

(1) After the file system is created, return to the file system list.
(2) Click the name of the file system to enter its basic information page.
(3) Click **Mount Target Info** to get the mount commands on Linux and Windows. You are recommended to copy the commands provided in the console to perform mount operations.
