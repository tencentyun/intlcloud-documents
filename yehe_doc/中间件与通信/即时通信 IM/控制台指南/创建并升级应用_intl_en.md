## Use Cases
This article describes how to create Trial Edition apps and obtain SDKAppIDs. It also covers how to upgrade Trial Edition apps to Pro Edition apps using the IM console.

## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](http://intl.cloud.tencent.com/document/product/378/3629).

## Creating a Trial App
1. Log in to the [IM console](https://console.cloud.tencent.com/im).
2. Click **Create Application**.
3. In the **Create Application** dialog box, enter your app name, and click **Confirm**.
    After the app is created, you can view the status, service version, SDKAppID, creation time, and expiration time of the new app on the overview page of the console.

<dx-alert infotype="explain" title="">
By default, a new app is a trial app and enabled.
A Tencent Cloud account can create a maximum of 300 IM apps. If you want to create more apps, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app first and then create a new one. **Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost. Proceed with caution**.
</dx-alert>

![](https://main.qcloudimg.com/raw/8997bb04e972bfe2a1ef7a149b7350b1.jpg)


## Upgrading an App
>?You can use a plan to upgrade an app from the Trial Edition to the Pro Edition or Flagship Edition but cannot roll it back to the Trial Edition after the upgrade. After the services of an app are suspended due to overdue payments or refunds, if you need to continue to use the services, you can renew the Pro Edition or Flagship Edition plan. If you want to go back to the Trial Edition, [create a new app](https://intl.cloud.tencent.com/document/product/1047/34577).


1. Click **View Upgradeable Items** in the target app card to view the comparison of upgradeable items.
![](https://main.qcloudimg.com/raw/57df90241441a67073bfd4b52de3bc5d.png)
2. Click **Upgrade Plan** at the bottom of the **Compare Upgradeable Items** dialog box.
3. Configure the following parameters as required:
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
         <td nowrap="nowrap">Value-added Features</td>   
				 <td>Value-added features include **max groups per user**, **max number of members in a group (non-audio-video group)**, **content filtering (advanced)**, and **extending storage period of historical messages**.</ul></td>   
     </tr> 
	 <tr> 
	     <td>Subscription length</td>   
	     <td>The plans are purchased on a monthly basis. You can select a length from 1 to 24 months.<br>You can also select to **Auto renew subscription when there are sufficient funds**.</td>   
     </tr> 
</table>
![](https://main.qcloudimg.com/raw/30985b047064c2c520d5c8b867ed42f5.png)

![](https://main.qcloudimg.com/raw/ee60c52d0d2b738e2afb1f0209a27a79.png)

4. Select **I have read and agree to the [Tencent Cloud IM service level agreement](https://intl.cloud.tencent.com/document/product/1047/34545)** and click **Purchase Now**.
5. Check all information and select whether to use a voucher. Click **Confirm** to complete the process.
