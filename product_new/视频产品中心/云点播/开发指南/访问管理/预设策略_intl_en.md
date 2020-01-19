Access control is essentially to bind subaccounts to policies or grants policies to subaccounts. You can use preset policies directly in the console to implement some simple authorization operations. For more complicated authorization operations, please see [Custom Policies](https://cloud.tencent.com/document/product/266/39339).

Currently, VOD provides the following preset policies:

| Policy Name | Description |
| :---------------------: | :------------------: |
|  QcloudVODFullAccess   | Full access to VOD |
| QcloudVODReadonlyAccess | Read-only access to VOD  |

## Usage Examples of Preset Policies


### Creating a subuser with full access to VOD

1. Access the **[User List](https://console.cloud.tencent.com/cam)** page in the CAM Console as a [root account](https://cloud.tencent.com/document/product/598/13665) and click **Create User**.
   ![](https://main.qcloudimg.com/raw/1a069f052f6256ee997f600e0d28ad9d.png)
2. On the "Create User" page, click **Custom** under "Subuser" to enter the "Create Subuser" page.
   ![](https://main.qcloudimg.com/raw/e0482952524b105812409fcd53b8173c.png)
3. Enter the user information.
   - Enter the username, select **Programming Access** and **Tencent Cloud Console Access**, and configure other options as needed.
   - Click **Next** and complete authentication as prompted.
     ![](https://main.qcloudimg.com/raw/da19f2f16ac2c776448d3ca3fe87376e.png)
4. Set user permissions.
   - Search for and select the preset policy `QcloudVODFullAccess`.
   - Click **Next**.
		<img src="https://main.qcloudimg.com/raw/eb4b8d164c63e22c71eee3d4b2162c83.png" width="704">
5. Click **Complete** in the "Review Info and Permission" column. After the user is created successfully, download the login link and security credentials as shown below and keep them safe.
   ![](https://main.qcloudimg.com/raw/9026555928c6ebe755b5c3921e9a7668.png)
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
	     <td>Needed for console login</td>   
	     <td>Yes</td>
     </tr> 
	 <tr>      
         <td>Password</td>   
	     <td>Security credential file in CSV format</td>   
	     <td >Needed for console login</td>   
	     <td >Yes</td>
     </tr> 
		  <tr>      
         <td>SecretId</td>   
	     <td>Security credential file in CSV format</td>   
	     <td >Needed for server API call. For more information, please see<a href="https://cloud.tencent.com/document/product/598/37140">Access Key</a></td>   
	     <td >Yes</td>
     </tr> 
	     <tr>      
         <td>SecretKey</td>   
	     <td>Security credential file in CSV format</td>   
	     <td >Needed for server API call. For more information, please see<a href="https://cloud.tencent.com/document/product/598/37140">Access Key</td>   
	     <td >Yes</td>
     </tr> 
</table>

With the above login link and security credentials, you can use this subuser to perform all operations in VOD (e.g., accessing the VOD Console and calling VOD server APIs).
>For more information on how to create a subuser, please see the [Creating Subusers](/document/product/598/13674) document of CAM.

### <span id="p2"></span>Granting full permissions of VOD to existing subusers

1. Access the **[User List](https://console.cloud.tencent.com/cam)** in the CAM Console as a [root account](/document/product/598/13665) and click the desired subaccount.
   ![](https://main.qcloudimg.com/raw/d4e14d166031830c96c8af62e8ba7580.png)
2. Click **Add Policy** in the "Permission" column on the "User Details" page, as shown below (in practice, the information displayed on this page may vary by existing permissions of the subaccount. If the permission of a subaccount is not empty, please click **Associate Policy**).
   ![](https://main.qcloudimg.com/raw/03601abde3da997fcbcbdb0832f97ae9.png)
3. Click **Select Policy from Policy List to Associate**, search for and check the preset policy `QcloudVODFullAccess`, and complete authorization as prompted.

### Revoking a subuser's full access to VOD

1. Access the **[User List](https://console.cloud.tencent.com/cam)** in the CAM Console as a [root account](/document/product/598/13665) and click the desired subaccount.
   ![](https://main.qcloudimg.com/raw/b1aa046a9683d823bfd2a981af6eaf98.png)
2. Find the preset policy `QcloudVODFullAccess` in the "Permission" column on the "User Details" page, click **Unassociate** on the right, and complete deauthorization as prompted.
   <img src="https://main.qcloudimg.com/raw/d8275e7b4d6ae7ebcd9d0f9c729b7aff.png" width="704">
