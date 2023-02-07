## Overview
This feature allows you to perform the following operations on a function triggering rule at a site:  
- Add, delete, modify, and search for a triggering rule.  
- Adjust the priority of the triggering rule. If the request URL matches multiple triggering rules, you can reorder those triggering rules. Only the triggering rule on the top will be executed.  

## Directions 
### Creating a triggering rule
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and choose **Edge function** > **Function Trigger** on the left sidebar.
2. On the **Function Trigger** page, click the ![](https://qcloudimg.tencent-cloud.cn/raw/03f10b28b4a75b8cc534e433375ed0d2.png) icon to the right of the rule list and configure the parameters.<br><img src="https://qcloudimg.tencent-cloud.cn/raw/db4c3d3cbc06081bc5f983a4a86f29a8.png" width=700px>
Parameters  
 - Site: The name of the current site is displayed by default.  
 - Description: (Optional) It can contain up to 60 characters.  
 - Condition: Specify the matching type, operator, and value as needed. For more information, see [Rule Engine](https://intl.cloud.tencent.com/document/product/1145/46151).
 - Execute function: Select a created function from the drop-down list.  
3. Click **OK**.    


### Editing the triggering rule
1. On the **Function Trigger** page, find the rule and click **Edit**.
![](https://qcloudimg.tencent-cloud.cn/raw/09f759146da6faa18987643891aadd8c.png)
2. In the **Edit triggering rule** dialog box, modify the parameters and click **OK**.<br><img src="https://qcloudimg.tencent-cloud.cn/raw/9532ef02ef91e6472f8b9f52810a47e2.png" width=700px>


### Searching for the triggering rule
On the **Function Trigger** page, click the ![](https://qcloudimg.tencent-cloud.cn/raw/cc51996cbb1a4eb77dfc9b452a88d7c0.png) icon to the right of the rule list and enter a keyword of the rule ID in the search box to search for the triggering rule.
![](https://qcloudimg.tencent-cloud.cn/raw/bb46d805f0ffe30dc00ad6478601ea82.png)


### Deleting the triggering rule
1. On the **Function Trigger** page, click the ![](https://qcloudimg.tencent-cloud.cn/raw/341a70c7c6f3c3770463fa7a3ef7c101.png) icon to the right of the rule list.
2. Find the rule and click the ![](https://qcloudimg.tencent-cloud.cn/raw/00b18e737c0759a826082e59ea95d5ad.png) icon.
![](https://qcloudimg.tencent-cloud.cn/raw/6d86865dea1667ba79dc18085c444e93.png)
3. In the pop-up dialog box, click **Confirm to delete**.
![](https://qcloudimg.tencent-cloud.cn/raw/f8d06b6e97d5485860acf2c901dc0599.png)


### Adjusting the priority of the triggering rule
1. On the **Function Trigger** page, click the ![](https://qcloudimg.tencent-cloud.cn/raw/341a70c7c6f3c3770463fa7a3ef7c101.png) icon to the right of the rule list.
2. Find the rule. Click the ![](https://qcloudimg.tencent-cloud.cn/raw/d07f725689d5f191c101504e40bea070.png) icon to move the rule up by one row or the ![](https://qcloudimg.tencent-cloud.cn/raw/993e3ac84f60d1bec83bbeb2d2161ab1.png) icon to move the rule down by one row. Then, click **Save**.
>? If the request URL matches multiple triggering rules, such as Rules 01 and 02 in the following figure, only the triggering rule on the top will be executed. In this example, only Rule 01 will be executed.

![](https://qcloudimg.tencent-cloud.cn/raw/83b800971fa64e3b8acb21dae46baeee.png)

