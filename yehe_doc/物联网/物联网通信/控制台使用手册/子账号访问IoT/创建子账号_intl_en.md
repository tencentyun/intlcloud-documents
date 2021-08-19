
## Overview
This document describes how to add a sub-account (with a **collaborator** as an example) under the root account.
 
## Directions
1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/) as the **root account** and select **Cloud Products** > **[Cloud Access Management](https://console.cloud.tencent.com/cam/overview)** to enter the CAM console.
2. Select **User** > **User List** on the left sidebar and click **Create User**. 
3. On the user type selection page that pops up, select **Collaborator** or **Sub-user**.
4. Enter relevant information such as **username**, **login account**, **mobile** and **email** as required on the collaborator creation page and click **Next**.
5. Select a user group for the new collaborator. If there is no existing user group, click **Create User Group**.
6. Select **Authorize from Policy List**, search for "IoT" in the list, select the IoT-related policies as shown below, and click **Done**.
![](https://main.qcloudimg.com/raw/54aaea875636d2638adebb94d59cd168.png)

After the collaborator is created, you can view the collaborator information in the user list.


## Subsequent Steps
Click the **collaborator username** to enter the user information management page and create an API key for the collaborator. This key is used by the collaborator to access the root account's IoT resources through RESTful APIs.


