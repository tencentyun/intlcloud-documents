## Operation Scenario
This article describes how to create a Trial Edition app and obtain the SDKAppID in the Instant Messaging (IM) console. It also shows you how to upgrade an app from Trial Edition to Pro Edition.

## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](http://intl.cloud.tencent.com/document/product/378/3629).

## Creating a Trial App
1. Log in to the [IM Console](https://console.cloud.tencent.com/im).
2. Click **Add Application**.
3. In the **Create Application** dialog box, enter an app name and click **OK**.
    After the app is created, you can view the status, version, SDKAppID, creation time, and expiry time of the new app on the overview page of the console.
  >By default, a new app is a trial app and enabled.
  >A Tencent Cloud account supports a maximum of 100 IM apps. If you have reached that limit, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app before creating a new one. **Once an app is deleted, all the data and services associated with the SDKAppID are removed and cannot be recovered, so proceed with caution.**

  ![](https://main.qcloudimg.com/raw/8997bb04e972bfe2a1ef7a149b7350b1.jpg)

## Upgrading an App

1. Locate the desired app and click **Upgrade**. The IM standard billing plan purchase page appears.
2. Configure the parameters described in the following table:
  <table>
     <tr>
         <th>Parameter</th>  
         <th>Description</th>  
     </tr>
	 <tr>      
         <td>SDKAppID</td>   
				<td>Make sure the SDKAppID is correct. It cannot be modified after purchase.</td>   
     </tr> 
	 <tr>      
         <td>Standard billing plan</td>   
				 <td><ul><li>If the current SDKAppID is under the Trial Edition, you can select **Pro Edition** or **Flagship Edition**. The **Purchase value-added service plan separately** option is unavailable.</li><li>If the current SDKAppID is under the Pro Edition or Flagship Edition, only the **Purchase value-added service plan separately** option is available.</li></ul></td>   
     </tr> 
	 <tr>      
         <td nowrap="nowrap">Available value-added features</td>   
				 <td>Value-added plans include value-added features such as **Maximum groups a user can join**, **Maximum members per group**, **Enable content filtering**, and **Extend the retention period of historical messages**.</ul></td>   
     </tr> 
	 <tr> 
	     <td>Purchase Period</td>   
	     <td>Standard billing plans are paid monthly. You can select a length from 1 to 24 months.</td>   
     </tr> 
</table>


4. Check **I have read and accept the “Tencent Cloud Instant Messaging (IM) Service Level Agreement”** and click **Buy Now**.
5. Make sure all information is correct and select whether to use a voucher. Click **Confirm** to complete the process.
