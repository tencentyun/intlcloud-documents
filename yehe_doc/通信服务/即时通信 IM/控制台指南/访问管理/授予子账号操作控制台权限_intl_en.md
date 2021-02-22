## Overview
This document describes two authorization methods to resolves the following issues. Details steps are as below. To configure more complex permission policies, see [Custom Policy](https://intl.cloud.tencent.com/document/product/1047/38088).
- When you are using the IM service with a sub-account, the root account needs to authorize the sub-account to access the [IM console](https://console.cloud.tencent.com/im) and to configure settings. Otherwise, the console will not display the application list, as shown below:
![](https://main.qcloudimg.com/raw/0a28018859d63fc6822457021fc1e023.png)
- When a sub-account has access to tags, but it does not match the access to the console application tags, the sub-account cannot view or create applications in the console.

## Solution 1. Global Authorization
### Step 1. Go to CAM to authorize
Log in to the [CAM console](https://console.cloud.tencent.com/cam) using the root account, click **User List**, click **Authorize** on the left of the sub-user, and the **Associate Policy** dialog box will pop up.
![](https://main.qcloudimg.com/raw/9a87638c3298b3e50307e82186eb17ea.png) 

### Step 2. Select policies
Search by “instant messaging”, select the desired policies, and click **Confirm** to complete the authorization.
![](https://main.qcloudimg.com/raw/9a4b20af40d5800db94c058f6a492175.png)

>?
>- **Read/write access**: allows users to access the console and modify configurations.
>- **Read-only access**: allows users to access the console only, not to perform other operations.
### Step 3. Complete authorization
If **Policy associated** is prompted in the upper right corner, the authorization is completed.
![](https://main.qcloudimg.com/raw/7c2812137b4afc10dcf3de7072a90761.png)


## Solution 2. Authorization by Tag
This solution is designed for customers who need to authorize and manage sub-accounts by tag. Sub-accounts can only access and operate applications under the authorized tags.
>!After a tag policy is assigned to a sub-account, the sub-account cannot access and operate applications with no tags. For a sub-account, there are no tags in a newly created application in the [IM console](https://console.cloud.tencent.com/im). Therefore, the root account needs to change the application tags to authorized tags before the sub-account can use the application.


### Step 1. Go to CAM to authorize
Log in to the [CAM console](https://console.cloud.tencent.com/cam) using the root account, click **Policies**, click **Create Custom Policy**, and the **Select Policy Creation Method** dialog box will pop up.
![](https://main.qcloudimg.com/raw/289a2def35370b7511625b37f3e798b3.png)

### Step 2. Select a tag
Select **Authorize by Tag** to go to **Tag Policy Generator**.
![](https://main.qcloudimg.com/raw/02098a1da180deae9c810b97cb0c453c.png)

### Step 3. Generate a policy
Enter the sub-account to be authorized, tag, and other information in **Tag Policy Generator** and click **Next** to go to the next step.
![](https://main.qcloudimg.com/raw/e590a9843e852bf9eca22bfc95ffbc13.png)

>?If there are no tags to select from, you need to log in to the [Tag console](https://console.cloud.tencent.com/tag/taglist) to create a tag.
>![](https://main.qcloudimg.com/raw/e6d0aeb3a04b9281627805f0cde3d052.png)

### Step 4. Complete authorization
After confirming the information is correct, click **Done** to complete the authorization.
![](https://main.qcloudimg.com/raw/3c9e2624f334f9c9820402f579381ae6.png)