## Introduction
This article describes how to create Trial Edition apps and obtain SDKAppIDs. It also covers how to upgrade Trial Edition apps to Pro Edition apps using the IM console.

## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](http://intl.cloud.tencent.com/document/product/378/3629).

## Creating a Trial App
1. Log in to the [IM console](https://console.cloud.tencent.com/im).
2. Click **Add Application**.
3. In the **Create Application** dialog box, enter an app name and click **OK**.
    After the app is created, you can view the status, service version, SDKAppID, creation time, and expiration time of the new app on the overview page of the console.
  > By default, a new app is a trial app and enabled.
  > A Tencent Cloud account can create a maximum of 100 IM apps. If you want to create more apps, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app. **Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost**. **Proceed with caution**.
  >
  ![](https://main.qcloudimg.com/raw/2753962b67754a9ebb2a2a5b8042f2ef.png)

## Upgrading an App

1. Locate the desired app and click **Upgrade**. The IM standard billing plan purchase page appears.
2. Configure the parameters described in the following table:
  <table>
     <tr>
         <th>Parameter</th>  
         <th>Description</th>  
     </tr>
	 <tr>      
         <td>SDKAppID of your app</td>   
				<td>Make sure that the SDKAppID is correct. You will not be able to modify it after purchasing the standard billing plan.</td>   
     </tr> 
	 <tr>      
         <td>Standard billing plan</td>   
				 <td><ul><li>If your app is a trial app, you can only select **Pro** or **Flagship**. You cannot purchase value-added service plans.</li><li>If your app is a pro or flagship app, you can only purchase **value-added service plans**.</li></ul></td>   
     </tr> 
	 <tr>      
         <td nowrap="nowrap">Value-added plans</td>   
				 <td>Value-added plans include **Maximum groups a user can join**, **Maximum members per group**, **Enable content filtering**, and **Extend the retention period of historical messages**.</ul></td>   
     </tr> 
	 <tr> 
	     <td>Duration</td>   
	     <td>Standard billing plans are purchased by the month. You can select a length from 1 to 24 months.</td>   
     </tr> 
</table>
<img src="https://main.qcloudimg.com/raw/cf5c80a6fb2fed4b7a545b6f92b643ca.png">
4. Select **I have read and agree to the Tencent Cloud IM service agreement** and click **Purchase**.
5. Check all information and select whether to use a voucher. Click **Confirm** to complete the process.
