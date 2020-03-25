## Overview

You can set access permissions of folders in the COS Console, so that specified users can perform specified operations on the contents of the folders. You are recommended to follow the [principle of least privilege](https://intl.cloud.tencent.com/document/product/436/32972) when configuring permissions to protect your data assets.

>COS stores objects in a flat structure with no traditional folder concept. In order to make COS customary, we turn an object into a "folder" by suffixing it with `/` in its key. In fact, a "folder" in COS is an object with a storage capacity of 0 KB.

The folder permission is essentially an access permission at the object level, which takes precedence over the bucket access permission. COS supports the following two types of object permissions:
- Public permissions: inherited permission, private read/write, and public read/private write. For more information on public permissions, please see [Access Permission Types](https://intl.cloud.tencent.com/document/product/436/13324).
- User permissions: the root account has all the permissions of the object by default (i.e., full access). In COS, sub-accounts can be added to read/write data, read/write permissions, and have the full access.

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket list page.
2. Find the bucket where a folder is located and click the bucket name to enter the bucket management page.
	 ![Bucket management page screenshot](https://main.qcloudimg.com/raw/b3917dd3aff063f14016d9f1b280276b.png)
3. On the "File List" tab, click **Set Permission** in the "Operation" column to the right of the folder for which to set permission.
	 ![File list page screenshot](https://main.qcloudimg.com/raw/2d5efff0532cec0e1fbec063f983e611.png)
4. You can set folder permissions based on your business needs as detailed below:
<table>
   <tr>
      <th>Permission Type</th>
      <th>Configuration Item</th>
      <th>Description</th>
   </tr>
   <tr>
      <td rowspan="4">Public permissions</td>
      <td>Inherited permissions</td>
      <td>Same as the bucket permission by default.</td>
   </tr>
   <tr>
      <td>Private read/write</td>
      <td>Only the root account can read/write, while non-root accounts (sub-accounts, other users' root accounts, or anonymous users) cannot access this folder.</td>
   </tr>
   <tr>
      <td>Public read/private write</td>
      <td>The root account can read/write, while non-root accounts (sub-accounts, other users' root accounts, or anonymous users) can only read the contents of the folder but not write new data into it.</td>
   </tr>
   <tr>
      <td>Public read/write</td>
      <td>Both the root account and non-root accounts (sub-accounts, other users' root accounts, or anonymous users) can read/write.</td>
   </tr>
   <tr>
      <td rowspan="6">User permissions</td>
      <td>User type</td>
      <td>A root account refers to the root account ID of other user accounts, while a sub-account refers to the sub-account under the currently used root account.<br>If you want sub-accounts under another root account to have access permissions, you must grant access permissions to that root accounts first, so that it can grant access permissions to its own sub-accounts.</td>
   </tr>
   <tr>
      <td>Data read</td>
      <td>Permission to read data.</td>
   </tr>
   <tr>
      <td>Data write</td>
      <td>Permission to write data.</td>
   </tr>
   <tr>
      <td>Permission read</td>
      <td>Permission to read folder permission configuration. If this permission is granted, authorized users can get details of folder permission configuration.</td>
   </tr>
   <tr>
      <td>Permission write</td>
			<td>Permission to modify folder permission configuration. If this permission is granted, authorized users can modify the details of folder permission configuration.<b>This configuration will cause permission change. Please select it with caution.</b></td>
   </tr>
   <tr>
      <td>Full access</td>
      <td>Including four permissions: data read, data write, permission read, and permission write. <b>This configuration grants a wide range of permissions. Please select it with caution.</b></td>
   </tr>
</table>
<img src="https://main.qcloudimg.com/raw/be31a82ce94421adf25ff8e0a69db359.png">
5. After setting the permission, click **Save** on the right.


