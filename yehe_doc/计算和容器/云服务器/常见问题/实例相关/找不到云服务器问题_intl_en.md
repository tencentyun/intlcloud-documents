## Problem Description
A purchased CVM instance cannot be found in the CVM console.


## Possible Causes
[1. The instance is not located in the current region](#1)
[2. You did not log in to the right console](#2)
[3. No instance is available under the current account](#3)
[4. The instance is released due to overdue payment or expiration](#4)
[5. The spot instance is automatically repossessed](#5)
[6. Refund is caused by insufficient resources](#6)


## Solutions
[](id:1)
### 1. The instance is not located in the current region
If you did not switch to the region where the instance is located, you cannot find the instance. You can check this with the following method.
Log in to the CVM console, and click [Instances](https://console.cloud.tencent.com/cvm/instance) in the left sidebar. Switch to another region to check the instance at the top of the page. 
<img src="https://qcloudimg.tencent-cloud.cn/raw/9f3877ec56c7a19adf8c3e5594d5038f.png" width="500px"/>



[](id:2)

### 2. You did not log in to the right console
You maybe purchased a [Lighthouse instance](https://console.cloud.tencent.com/lighthouse/instance) or another instance instead of a CVM instance, and you did not log in to the right console.
- Method 1: Go to [Overview](https://console.cloud.tencent.com/) > **Order Management**, and check the prepaid and postpaid orders for the last three months. If the instance was purchased long ago, please click **[All time](https://console.cloud.tencent.com/expense/deal)**. 
	<img src="https://qcloudimg.tencent-cloud.cn/raw/435aaa01910882ffd0edf1a1dd94a1e0.png" width="500px"/>
                                         
	
- Method 2: View all the resources under your current account by clicking [Overview](https://console.cloud.tencent.com/) > **My Resources** in the console.  
<img src="https://qcloudimg.tencent-cloud.cn/raw/0b159468504385294580b4485235f976.png" width="500px"/>              



[](id:3)

### 3. No instance is available under the current account
- You can find your account ID in an SMS you received related to CVMs.
- The instance may not be purchased with an account under your name. 

[](id:4)

### 4. The instance is released due to overdue payment or expiration
If an instance is expired or with overdue payment, it will be released, and so you cannot find it in the console.

- Terminated instances cannot be recovered. You can check the Prepaid Service Expiration and Suspension Notification via [Message Center](https://console.cloud.tencent.com/message/index). If you did not receive a relevant message in Message Center, maybe you have unsubscribed the notification.
- If your account has overdue payment, please see [Payment Overdue](https://intl.cloud.tencent.com/document/product/213/2181) for status of the CVM instances and public network bandwidth.

[](id:5)

### 5. The spot instance is automatically repossessed
An allocated [Spot Instance](https://intl.cloud.tencent.com/document/product/213/17816) may be repossessed based on the prices or the relationship between supply and demand.

You will be notified via Message Center or metadata before the spot instance is terminated. You can check Notification on Spot Instance Repossessing via [Message Center](https://console.cloud.tencent.com/message/index). If you did not receive a relevant message in Message Center, maybe you have unsubscribed the notification. 

[](id:6)

### 6. Refund is caused by insufficient resources
If you cannot find the newly purchased instance in the console, maybe it is because a refund is caused by insufficient resources.

You can check the refund in [Order Management](https://console.cloud.tencent.com/expense/deal), and then purchase again in another region or availability zone.
