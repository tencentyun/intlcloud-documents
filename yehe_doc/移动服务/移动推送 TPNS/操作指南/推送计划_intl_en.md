## Overview

A push plan helps operational personnel and developers manage multiple push tasks for different push targets in the form of combinations and allows them to view the overall effect of pushes by plan and evaluate the fulfillment of overall goals.


## Use Cases

#### Managing push tasks for different operational goals

Multiple push tasks may need to be created for big events such as 6/18 and 11/11 shopping festivals or for the same operational goal such as improving the user retention rate. In this case, you can create a push plan to manage relevant push tasks. This allows you to view the number of delivered messages and user clicks by plan to find out the conversion effect and fulfillment of marketing goals.

#### Notifications and pushes triggered by users

For common push types such as like, comment, share, and private message, you can put all single-user push tasks of the same type into the same plan. This allows you to view data such as the number of push messages and user clicks of a type by day to evaluate if messages of this type help improve user engagement.

## Operation Directions

### Creating a push plan in the console

**Method 1:**

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).
2. Go to **Push Management** > **Push Plan** and click **Create Plan**.
3. In the pop-up dialog box, enter the plan name and description and click **Confirm**.
After the plan is created, you can view its name, description, and number of push tasks on the **Push Plan** page. You can also edit or delete the plan at any time. 

**Method 2:**

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).
2. Go to **Push Management** > **Task List** and click **Create Push**.
3. Click **+Create New Plan*.
   ![](https://main.qcloudimg.com/raw/a340cc1783dfc8f00da6ceae396d5812.png)
4. In the pop-up dialog box, enter the plan name and description and click **Confirm**.
After the plan is created, it will be automatically selected for the current push.


### Viewing push tasks in a push plan

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).
2. Go to **Push Management** > **Push Plan**, click **Details** on the right of the target push plan, and click **Task List**.
![](https://main.qcloudimg.com/raw/a30e39d13e055ebdaa59108c7ca088bf.png)

### Creating a push task in a push plan

On the push plan details page, click **Task List** > **Create Push**.
![](https://main.qcloudimg.com/raw/dc7ae3d299e0e65f8b07c69ed5d77b4a.png)

### Viewing the aggregated statistics of a push plan

On the push plan details page, click **Plan Overview** and you can view the aggregated statistics of the push plan.
![](https://main.qcloudimg.com/raw/bdf6651442b40956965ffcc7b5560b41.png)

### Creating a push plan and specify a push plan to push a message via RESTful API calls

#### Creating a push plan

Refer to [Creating Push Plan](https://intl.cloud.tencent.com/document/product/1024/39025) to create a push plan. Then, you can specify it to push a message.

#### Sample creation

```
{
			"planName":"VIP_Level 15",
			"planDescribe":"VIP member benefits"
}
```

#### Specifying a push plan to push a message

When calling the push API, you can set the `plan_id` to specify a push plan to push a message to target recipients. For more information, see the **Optional Parameters** section in [Push API](https://intl.cloud.tencent.com/document/product/1024/33764).

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
