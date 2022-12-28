## Overview

You can set access permissions of folders in the COS console, so that specified users can perform specified operations on the content of the folders. You are recommended to follow the [principle of least privilege](https://intl.cloud.tencent.com/document/product/436/32972) when configuring permissions to protect your data assets.

>! COS stores objects in a flat structure with no traditional folder concept. In order to make COS customary, we turn an object into a "folder" by suffixing it with `/` in its key. In fact, a "folder" in COS is an object with a storage capacity of 0 KB.

Folder permission is essentially access permission at the object level, which takes precedence over the bucket access permission. COS supports two types of object permissions:

- Public permissions: inherited permission, private read/write, and public read/private write. For more information on public permissions, please see [Access Permission Types](https://intl.cloud.tencent.com/document/product/436/13324).
- User permissions: the root account has all the permissions of the object by default (i.e., full access). In COS, sub-accounts can be added to read/write data, read/write permissions, and have the full access.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Bucket List** to go to the bucket list page.
3. Locate the bucket where the folder is located and click the bucket name to go to the bucket management page.
4. In the left sidebar, choose **File List** to go to the file list page.
5. Locate the folder for permission setting, and click **Permission**.

6. In the pop-up window, set folder permissions as required.

Permission settings are described as follows:
<table>
   <tr>
      <th>Permission Type</th>
      <th>Parameter</th>
      <th>Description</th>
   </tr>
   <tr>
      <td rowspan="4">Public permission</td>
      <td>Inherit</td>
      <td>Default value, consistent with the bucket permission.</td>
   </tr>
   <tr>
      <td>Private Read/Write</td>
      <td>Only the root account has the read and write permissions on the folder. Non-root accounts (sub-accounts, the root accounts of other users, or anonymous users) cannot access the folder.</td>
   </tr>
   <tr>
      <td>Public Read/Private Write</td>
      <td>The root account has the read and write permissions on the folder. Non-root accounts (sub-accounts, the root accounts of other users, or anonymous users) can read content in the folder but cannot write new data into the folder.</td>
   </tr>
   <tr>
      <td>Public Read/Write</td>
      <td>Both the root account and non-root accounts (sub-accounts, the root accounts of other users, or anonymous users) have the read and write permissions on the folder.</td>
   </tr>
   <tr>
      <td rowspan="6">User ACL</td>
      <td>User Type</td>
      <td>`Root account` indicates the root account of other users. `Sub-account` indicates the sub-account under the current root account.<br>To grant the access permission to a sub-account of another root account, you need to grant the access permission to that root account first and then grant the access permission to the sub-account from that root account.</td>
   </tr>
   <tr>
      <td>Read</td>
      <td>Permission to read data</td>
   </tr>
   <tr>
      <td>Write</td>
      <td>Permission to write data</td>
   </tr>
   <tr>
      <td>Read ACL</td>
      <td>Permission to read folder permission configuration. With this permission, you can obtain folder permission configuration details.</td>
   </tr>
   <tr>
      <td>Write ACL</td>
			<td>Permission to modify folder permission configuration. With this permission, you can modify folder permission configuration details. <b>Exercise caution with this configuration because it will cause permission changes.</b></td>
   </tr>
   <tr>
      <td>Full control</td>
      <td>Includes the Reads, Write, Read ACL, and Write ACL permissions. <b>Exercise caution with this configuration because it grants a wide range of permissions.</b></td>
   </tr>
</table>




5. Click **Save** in the **Operation** column.
6. Click **Close**.



