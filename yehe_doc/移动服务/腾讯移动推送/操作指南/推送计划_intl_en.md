## Overview

A push plan helps operational personnel and developers manage multiple push tasks for different push targets in the form of combinations and allows them to view the overall effect of pushes by plan and evaluate the achievement of overall goals.


## Use Cases

#### Managing push tasks for different operational goals

Multiple push tasks may need to be created for phased events such as 6/18 and 11/11 shopping festivals or for the same operational goal such as improving the retention rate of new users. In this case, you can create a push plan to manage them and view the number of messages reached and user clicks at the plan level, so as to understand the conversion effect and achievement of marketing goals.

#### Notifications and pushes triggered by user

For common push types such as like, comment, share, and private message, you can group all single-user push tasks of the same type into the same plan and view data such as the number of push messages and user clicks in the type by day, so as to evaluate the promotional effect of the message type on user activity.

## Directions

### Creating push plan in console

**Method 1:**

1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns)
2. Go to **Push Management** > **Push Plan** and click **Create Plan**.
3. In the **Create Plan** dialog box, enter the plan name and description and click **OK**. After the plan is created, you can view its name, description, and number of push tasks and edit or delete it at any time on the push plan page.

**Method 2:**

1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns)
2. Go to **Push Management** > **Push Task** and click **Create Push**.
3. Click **Create Push Plan**.
   ![](https://main.qcloudimg.com/raw/a340cc1783dfc8f00da6ceae396d5812.png)
4. In the **Create Push Plan** dialog box, enter the plan name and description and click **OK**. After the plan is created, it will be automatically selected for the current push.



### Viewing push task under push plan

1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns)
2. Go to **Push Management** > **Push Plan**, select the target push plan, and click **Details** to enter the push task list page.
   ![](https://main.qcloudimg.com/raw/a30e39d13e055ebdaa59108c7ca088bf.png)

### Creating push task in push plan

On the push task list page, click **Create Task**. On the push task creation page, select **Message Content** > **Preview** > **Push** and configure the task.
![](https://main.qcloudimg.com/raw/dc7ae3d299e0e65f8b07c69ed5d77b4a.png)

### Viewing the aggregated statistics of push plan

In the push plan details, select the overview page, and you can view the aggregated statistics of the push plan on the "Plan Overview" tab.
![](https://main.qcloudimg.com/raw/bdf6651442b40956965ffcc7b5560b41.png)
	

### Using RESTful API (to create push plan or specify push plan for push)

When calling the push API, you can set the `plan_id` to specify the ID of the push plan for the target recipients. For more information, please see [Optional Parameter Description](https://intl.cloud.tencent.com/document/product/1024/33764) in the RESTful API document.

Below is a sample push:

```json
{
    "audience_type": "token",
    "environment":"dev",
    "token_list": [ "05da87c0ae********fa9e08d884aada5bb2"],
    "message_type":"notify",
    "plan_id":"20200704",
    "message":{
     "title": "Push title",
    "content": "Push content",
    "ios":{
        "aps": {
            "alert": {
                "subtitle": "Push subtitle"
            },
            "badge_type": -2,
            "sound":"Tassel.wav",
            "category": "INVITE_CATEGORY"
        },
       "custom_content":"{\"key\":\"value\"}",
    }
 }
}
```

​	
