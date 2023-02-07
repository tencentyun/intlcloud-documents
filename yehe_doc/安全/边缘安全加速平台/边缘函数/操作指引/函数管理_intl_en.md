## Overview
This document describes how to create, edit, and delete an edge function, and how to configure the rules that trigger the function.

## Creating and Deploying a Function
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and choose **Edge function** > **Function Management** on the left sidebar.
2. On the **Edge function** page, click **Create function**.
3. On the **Create edge function** page, configure the parameters and click **Create and deploy**.
![](https://qcloudimg.tencent-cloud.cn/raw/3589c7b8d57c4d5228426fb42f52dd2a.png)
Parameters:
 - Function: (Required) It can contain only 2-30 letters, digits, and hyphens and must start with a letter and end with a digit or letter.
 - Description: (Optional) It can contain up to 60 characters.
4. If you see the following pop-up dialog box, the deployment is successful.
![](https://qcloudimg.tencent-cloud.cn/raw/169e3c72c79b921acfd6b13719e9268d.png)

## Configuring a Triggering Rule
1. After the function is deployed successfully, click **Add triggering rule**.
2. On the **Add triggering rule** page, specify the matching type, operator, and value as needed.  
![](https://qcloudimg.tencent-cloud.cn/raw/42b6752efec560c43f8b220a43670eed.png)
3. Click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/47572b634cbb916520705d7e98c5d46f.png)

## Editing the Function
1. If the deployed function does not meet your expectations, go to the [Edge function](https://console.cloud.tencent.com/edgeone/edgefunctions) page, find the function, and then click **Details**. On the function information page, click **Edit**.
![](https://qcloudimg.tencent-cloud.cn/raw/01e3f361566ba12d3d498f86dae1a800.png)
2. Modify the code and click **Save and deploy**. If you have configured a triggering rule for the function, a note will be displayed as follows: 
<img src="https://qcloudimg.tencent-cloud.cn/raw/3b6087cf41036e1e0908299ce3930531.png" style="zoom:70%;" />

## Deleting the Function
1. If you want to delete the function, go to the [Edge function](https://console.cloud.tencent.com/edgeone/edgefunctions) page, find the function, and then click **Delete** in the **Operation** column.  
![](https://qcloudimg.tencent-cloud.cn/raw/8df886ed3f6ad0032976a2a77439aaf3.png)
2. In the pop-up dialog box, click **OK**.  
Once deleted, the function cannot be restored. The triggering rules of the function will also be deleted.