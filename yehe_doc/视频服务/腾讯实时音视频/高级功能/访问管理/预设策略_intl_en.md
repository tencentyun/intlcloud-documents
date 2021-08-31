>!This document describes the management of access to **TRTC**. For access management of other Tencent Cloud services, see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

TRTC access management works by associating permission policies with sub-accounts or granting policies to sub-accounts. The preset policies in the console allow you to perform some simple authorization. For more sophisticated authorization, see [Custom Policies](https://intl.cloud.tencent.com/document/product/647/39551).

TRTC offers the following preset policies currently.

| Policy | Description |
| --------------------- | ------------------ |
|   QcloudTRTCFullAccess   | Read-and-write permission |
| QcloudTRTCReadonlyAccess |  Read-only permission  |

## Examples of Using Preset Policies


### Creating a sub-account with the read-and-write permission

1. Go to the [User List](https://console.cloud.tencent.com/cam) page of the CAM console using a Tencent Cloud [root account](https://intl.cloud.tencent.com/document/product/598/32633) and click **Create User**.
2. On the "Create User" page, click **Custom Create** to go to the "Create Sub-user" page.
	
	>?Finish the steps before **User Permissions** as instructed in [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
3. On the **User Permissions** page:
   1. Search for and check the preset policy `QcloudTRTCFullAccess`.
   2. Click **Next**.
3. In the **Review** step, click **Complete**. After the sub-user is created successfully, download the login link and security credential file and store them properly. They contain the following information.
<table>
     <tr>
         <th nowrap="nowrap">Information</th>  
         <th nowrap="nowrap">Source</th>  
         <th nowrap="nowrap">Use</th>  
         <th nowrap="nowrap">Storage Required</th>  
     </tr>
	 <tr>      
         <td>Login link</td>   
	     <td>Copied from the console page</td>   
	     <td nowrap="nowrap">Facilitates console login. Root account information is not required for login via the link.</td>   
	     <td>No</td>
     </tr> 
	 <tr>      
         <td nowrap="nowrap">User ID </td>   
	     <td>Security credential file in CSV format</td>   
	     <td>Required for console login</td>   
	     <td>Yes</td>
     </tr> 
	 <tr>      
         <td>Password</td>   
	     <td>Security credential file in CSV format</td>   
	     <td >Required for console login</td>   
	     <td>Yes</td>
     </tr> 
		  <tr>      
         <td>SecretId</td>   
	     <td>Security credential file in CSV format</td>   
	     <td >Required for server API calling. For more information, see<a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a></td>   
	     <td>Yes</td>
     </tr> 
	     <tr>      
         <td>SecretKey</td>   
	     <td>Security credential file in CSV format</td>   
	     <td >Required for server API calling. For more information, see<a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</td>   
	     <td>Yes</td>
     </tr> 
</table>
4. Provide the login link and security credentials to the party you want to authorize access, who will be able to use the sub-account to perform all kinds of TRTC operations, including visiting the TRTC console, calling TRTC server APIs, etc.

### Granting read-and-write permission to existing sub-account

1. Go to the **[User List](https://console.cloud.tencent.com/cam)** of the CAM console using a Tencent Cloud [root account](https://intl.cloud.tencent.com/document/product/598/32633) and click the target sub-account.
2. On the **User Details** page, click **Add Policy** under the **Permissions** tab. If the sub-account already has permissions, click **Associate Policy**.
3. Click **Select policies from the policy list**, search for and check the preset policy `QcloudTRTCFullAccess`, and complete the authorization as prompted.

### Revoke the read-and-write permission of a sub-account


1. Go to the **[User List](https://console.cloud.tencent.com/cam)** of the CAM console using a Tencent Cloud [root account](https://intl.cloud.tencent.com/document/product/598/32633) and click the target sub-account.
2. On the **User Details** page, find the preset policy `QcloudTRTCFullAccess` under the **Permission** tab, click **Unassociate** on the right, and complete the deauthorization as prompted.
