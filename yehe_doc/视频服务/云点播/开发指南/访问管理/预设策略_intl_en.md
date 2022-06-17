>!This document describes the access management feature of **VOD**. For more information on access management for other Tencent Cloud services, please see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

Access management is essentially to bind sub-accounts to policies or grant policies to sub-accounts. You can use preset policies directly in the console to implement some simple authorization operations. For more complicated authorization operations, please see [Custom Policy](https://intl.cloud.tencent.com/document/product/266/33972).

Currently, VOD provides the following preset policies:

| Policy Name | Description |
| :---------------------: | :------------------: |
|  QcloudVODFullAccess   | Full access to VOD |
| QcloudVODReadonlyAccess | Read-only access to VOD  |

## Preset Policy Use Cases


### Creating subuser with full access to VOD

1. Access the [User List](https://console.cloud.tencent.com/cam) page in the CAM console as a [root account](https://intl.cloud.tencent.com/document/product/598/32633) and click **Create User**.
   ![](https://main.qcloudimg.com/raw/e700947b468ef25d4bf70ad1fecc6348.png)
2. On the **Create User** page, click **Custom Creation**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/24a4e0e0b9461bdcbc0b4ea50e3e1267.png)
3. Click **Next** and enter the user information.
   - Enter the username, select **Programming Access** and **Tencent Cloud Console Access**, and configure other options as needed.
   - Click **Next** and complete authentication as prompted.
     ![](https://qcloudimg.tencent-cloud.cn/raw/389813710fb711d28bb80f2f9979cd10.png)
4. Set user permissions.
   - Search for and select the preset policy `QcloudVODFullAccess`.
   - Click **Next**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/597de21489df26315d604469d6906ec2.png" width="704">
5. Click **Complete** in the "Review Info and Permission" column. After the user is created successfully, download the login link and security credentials as shown below and keep them safe.
   ![](https://main.qcloudimg.com/raw/cc223f380730f8dbfe81caa799be2dfc.png)
<table>
     <tr>
         <th nowrap="nowrap">Information</th>  
         <th nowrap="nowrap">Source</th>  
         <th nowrap="nowrap">Function</th>  
         <th nowrap="nowrap">Storage Required</th>  
     </tr>
	 <tr>      
         <td>Login link</td>   
	     <td>Copy on the page</td>   
	     <td nowrap="nowrap">Makes it easier to log in to the console without having to enter the root account</td>   
	     <td>No</td>
     </tr> 
	 <tr>      
         <td nowrap="nowrap">Username</td>   
	     <td>Security credential file in CSV format</td>   
	     <td>Required for console login</td>   
	     <td>Yes</td>
     </tr> 
	 <tr>      
         <td>Password</td>   
	     <td>Security credential file in CSV format</td>   
	     <td >Required for console login</td>   
	     <td >Yes</td>
     </tr> 
		  <tr>      
         <td>SecretId</td>   
	     <td>Security credential file in CSV format</td>   
	     <td >Required for server API call. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</a></td>   
	     <td >Yes</td>
     </tr> 
	     <tr>      
         <td>SecretKey</td>   
	     <td>Security credential file in CSV format</td>   
	     <td >Required for server API call. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/598/32675">Access Key</td>   
	     <td >Yes</td>
     </tr> 
</table>

With the above login link and security credentials, you can use this subuser to perform all operations in VOD (e.g., accessing the VOD console and calling VOD server APIs).
>?For more information on how to create a subuser, please see the [Creating Subusers](https://intl.cloud.tencent.com/document/product/598/13674) document of CAM.

### <span id="p2"></span>Granting full permissions of VOD to existing subusers

1. Access the **[User List](https://console.cloud.tencent.com/cam)** in the CAM console as a [root account](https://intl.cloud.tencent.com/document/product/598/32633) and click the target sub-account.
   ![](https://main.qcloudimg.com/raw/86a75ce62dde0ba4c061975181186974.png)
2. Click **Add Policy** in the **Permission** column on the **User Details** page, as shown below (in practice, the information displayed on this page may vary by existing permissions of the sub-account. If the permission of a sub-account is not empty, please click **Associate Policy**).
   ![](https://main.qcloudimg.com/raw/e775e39eec0292f31a78d5a2332d6d09.png)
3. Click **Select Policy from Policy List to Associate**, search for and check the preset policy `QcloudVODFullAccess`, and complete authorization as prompted.

### Revoking subuser's full access to VOD

1. Access the **[User List](https://console.cloud.tencent.com/cam)** in the CAM console as a [root account](https://intl.cloud.tencent.com/document/product/598/32633) and click the target sub-account.
   ![](https://main.qcloudimg.com/raw/86a75ce62dde0ba4c061975181186974.png)
2. Find the preset policy `QcloudVODFullAccess` in the **Permission** column on the **User Details** page, click **Unassociate** on the right, and complete deauthorization as prompted.
   <img src="https://main.qcloudimg.com/raw/4d221c52efe40913031355c877f28a47.png" width="704">

