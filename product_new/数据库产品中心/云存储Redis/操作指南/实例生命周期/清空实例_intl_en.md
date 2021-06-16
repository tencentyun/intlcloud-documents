## Scenario
This document describes how to clear the data of an instance in the TencentDB for Redis Console.
>!
>- Once cleared, the data cannot be recovered. Please make sure you have backed up all data before submitting the clearing request.
>- Data clearing will affect the service provided by the instance, and the instance cannot be accessed during the clearing process. Please do so with caution.


## Directions

1. Log in to the [Redis Console](https://console.cloud.tencent.com/redis) and click an instance ID in the instance list to enter the instance details page.
2. On the instance details page, click **Clear Instance** in the upper-right corner.
![](https://main.qcloudimg.com/raw/9b5c4b5f4a344e1d62dbc2498f5aa53b.png)
3. In the pop-up dialog box, enter the instance password and click **OK**.
 >?The password to be entered here is the instance password you set previously but not the "instance ID:instance password" connection password used for accessing the instance.
4. You will be returned to the instance list. The instance is in the "Clearing" status. After the status changes to "Running", the instance can be used normally.
