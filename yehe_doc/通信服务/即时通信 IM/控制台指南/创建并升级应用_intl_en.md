## Overview
This article describes how to create Trial Edition apps and obtain SDKAppIDs. It also covers how to upgrade Trial Edition apps to Pro Edition apps using the IM console.

## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](http://intl.cloud.tencent.com/document/product/378/3629).

## Creating a Trial App
1. Log in to the [Instant Messaging Console](https://console.cloud.tencent.com/im).
2. Click **Add Application**.
3. In the **Create Application** dialog box, enter an app name and click **OK**.
    After the app is created, you can view the status, service version, SDKAppID, creation time, and expiration time of the new app on the overview page of the console.
  >? By default, a new app is a trial app and enabled.
  > A Tencent Cloud account can create a maximum of 100 IM apps. If you want to create more apps, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app first. **Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost**.

![](https://main.qcloudimg.com/raw/8997bb04e972bfe2a1ef7a149b7350b1.jpg)

## Upgrading an App
>? You can use a package to upgrade an app from the Trial Edition to the Pro Edition or Flagship Edition but cannot roll it back to the Trial Edition after the upgrade. After the services of an app are suspended due to arrears or refunds, if you need to continue to use the services, you can [renew] the Pro Edition or Flagship Edition package. If you want to go back to the Trial Edition, [create a new app](https://intl.cloud.tencent.com/document/product/1047/34577).


1. Click **Upgrade** in the card for the target app to open the IM package purchase page.
2. Configure the parameters described in the following table:
  <table>
     <tr>
         <th>Parameter Item</th>  
         <th>Note</th>  
     </tr>
	 <tr>      
         <td>Select the SDKAppID of your app</td>   
				<td>Make sure the SDKAppID is correct. It cannot be modified after purchase.</td>   
     </tr> 
	 <tr>      
         <td>Select a plan</td>   
				 <td><ul><li>If your app is a trial app, you can only select **Pro** or **Flagship**. You cannot purchase value-added service plans.</li><li>If your app is a pro or flagship app, you can only purchase **value-added service plans**.</li></ul></td>   
     </tr> 
	 <tr>      
         <td nowrap="nowrap">Value-added Plans</td>   
				 <td>Value-added plans include **Maximum groups a user can join**, **Maximum members per group (non-AVChatRoom)**, **Enable content filtering**, and **Extend the retention period of historical messages**.</ul></td>   
     </tr> 
	 <tr> 
	     <td>Subscription length</td>   
	     <td>The plans are purchased on a monthly basis. You can select a length from 1 to 24 months.<br>You can also select to **Auto renew subscription when there are sufficient funds**.</td>   
     </tr> 
</table>

4. Select **I have read and agree to the [Tencent Cloud IM service level agreement](https://intl.cloud.tencent.com/document/product/1047/34545)** and click **Purchase**.
5. Check all information and select whether to use a voucher. Click **Confirm** to complete the process.
