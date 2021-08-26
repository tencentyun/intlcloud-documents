
## Overview
This document describes how to add a sub-account (with a **collaborator** as an example) under the root account.

## Directions
1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/) as the **root account** and select **Cloud Products** > **[Cloud Access Management](https://console.cloud.tencent.com/cam/overview)** to enter the CAM console.
2. Select **Users** > **User List** on the left sidebar and click **Create User**. 
3. On the user type selection page that pops up, select **Collaborator** or **Sub-user**.
4. Enter relevant information such as **username**, **login account**, **mobile** and **email** as required on the collaborator creation page and click **Next**.
5. Select a user group for the new collaborator. If there is no existing user group, click **Create User Group**.
6. Select **Select policies from the policy list**, search for "IoT" in the list, select the IoT-related policies as shown below, and click **Done**.
![](https://main.qcloudimg.com/raw/2bb88bb4cb1fc322d1f9e49712eb8c3c.png)

After the collaborator is created, you can view the collaborator information in the user list.


## Subsequent Steps
Click the **collaborator username** to enter the user information management page and create an API key for the collaborator. This key is used by the collaborator to access the root account's IoT resources through RESTful APIs.


