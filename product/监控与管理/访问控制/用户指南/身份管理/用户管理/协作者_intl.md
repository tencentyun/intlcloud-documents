## Overview
Collaborator is a type of sub-account and is used to assist its primary account to manage cloud resources and sub-accounts. Collaborators can log in to the console to access the resources as well as receive message notifications.

## User Guide

### Create a collaborator

1. Log in to the Tencent Cloud console, go to [User](https://console.cloud.tencent.com/cam), click **Create User**, and then select **Collaborator**.
![](https://main.qcloudimg.com/raw/ac5cf81c6d781e7dca12b7efe234d092.png)

2. Enter the user information. We recommend that you turn on login protection and sensitive operations protection.

3. Set permissions. You can set permissions for the created collaborator in the following three ways. When associated with a policy, the collaborator can be granted the permissions described in the policy.
 - User groups: This is the best way to manage user permissions according to their functions. You can grant permissions to a collaborator by adding the collaborator to an existing user group or creating a new user group. The collaborator then will be associated with the policy of that user group. 
 ![](https://main.qcloudimg.com/raw/4a6b738e3748aeecc50ed0623ecfd9eb.png)
 - Copy the permissions of an existing user: By clicking **Copy Existing User's Permissions** and selecting the user whose permissions you want to copy, you can associate the collaborator with the policies of the user.
 ![](https://main.qcloudimg.com/raw/908a5e4531f0b35b61f7d1db79638068.png)
 - Use the policy list: Click **Grant Permissions from Policy List**, and then select the policies you want to associate with the collaborator.
 ![](https://main.qcloudimg.com/raw/82fc1abeb724a84eba9855022fc69bfe.png)
 
4. Click **Done**.

### Associate a collaborator with policies

#### Direct association
1. Log in to the Tencent Cloud console, go to [User](https://console.cloud.tencent.com/cam), select the collaborator you want to authorize, and click **Authorize** in the **Operation** column.
![](https://main.qcloudimg.com/raw/aa5e5efa2674742134ad0a100f43fc80.png)
2. Select the policies to be associated, and then click **OK**.
![](https://main.qcloudimg.com/raw/651a1c0e8181f64a34d597e2bcd48cdc.png)

#### Association with policies by joining groups
1. Log in to the Tencent Cloud console, go to [User](https://console.cloud.tencent.com/cam), locate the collaborator you want to authorize, and click **More** -> **Add to Group** in the **Operation** column.
![](https://main.qcloudimg.com/raw/34ba527220e06d8344cd9dc4dbdd0441.png)
2. Select the user group to which you want to add the collaborator, and then click **OK**.

### Disassociate a collaborator from policies 
#### Direct disassociation
1. Log in to the Tencent Cloud console, go to [User](https://console.cloud.tencent.com/cam), locate the collaborator you want to disassociate from policies, and then click the collaborator name to enter the details page.
![](https://main.qcloudimg.com/raw/2648266a7986476740ab2bef1006c091.png)
2. Click **Associated Policies**, locate the policies to be disassociated in the list, and then click **Disassociate** on the right.
![](https://main.qcloudimg.com/raw/70941b2c1281d828e7c5ca608ee462a3.png)
3. Click **Disassociate**.

#### Remove a collaborator from a user group
1. Log in to the Tencent Cloud console, go to [User](https://console.cloud.tencent.com/cam), locate the collaborator you want to disassociate from policies, and then click the collaborator name to enter the details page.
![](https://main.qcloudimg.com/raw/2648266a7986476740ab2bef1006c091.png)
2. Click **Associated Policies**, locate the policies to be disassociated in the list, and then click **Disassociate** on the right.
![](https://main.qcloudimg.com/raw/c1566f7e4b28fd1eef8e401afb2996dc.png)
3. Click **Disassociate** to remove the collaborator from the user group, and then the collaborator is disassociated from the policies of the user group.

### Subscribe a collaborator to messages
1. Log in to the Tencent Cloud console, go to [User](https://console.cloud.tencent.com/cam), select the collaborator for whom you want to subscribe to messages, and then click **More** -> **Subscribe to Messages** in the **Operation** column, as shown below:
![](https://main.qcloudimg.com/raw/79139119ca274cea6f32148bad2c31df.png)

2. Select the message type you want to subscribe to and click **OK**.
![](https://main.qcloudimg.com/raw/c527d42e456bbf72034f038fc1bad31c.png)

### View collaborator information in **User List** -> **Details**

1. Log in to the Tencent Cloud console, go to [User](https://console.cloud.tencent.com/cam), select the collaborator you want to view, and then click **detail** on the left, as shown below: ![](https://main.qcloudimg.com/raw/24cd11e8ea5094e390938b68736ec9f6.png)
>The message subscription, notes, last login time, last login method, MFA status and other information of the sub-user can be found here.

### Search for collaborators using search box
1. Log in to the Tencent Cloud console, go to [User](https://console.cloud.tencent.com/cam), enter the keyword in the search box at the upper right corner, and then click **search**  to find the collaborator. 
![](https://main.qcloudimg.com/raw/336d924fa1ed9fc07ecf4294a54729b8.png)
>The search box supports multi-keyword search (separated by a space). You can search collaborators using keywords such as username, ID, mobile number, email and remarks.


### Delete collaborators
#### Delete a single collaborator
1. Log in to the Tencent Cloud console, go to [User](https://console.cloud.tencent.com/cam), select the collaborator you want to deleted, and then click **More** -> **Delete** in the **Operation** column, as shown below:
![](https://main.qcloudimg.com/raw/dc58ed07235b00038f049d22b2bec191.png)

2. Click **Delete** to delete the collaborator.

#### Delete multiple collaborators
1. Log in to the Tencent Cloud console, go to [User](https://console.cloud.tencent.com/cam), select multiple collaborators to be deleted, and then click **Delete** at the upper left corner, as shown below:
![](https://main.qcloudimg.com/raw/a274a4888c8e7c00cda091538445ec54.png)
2. Click **Delete** to delete the collaborator.


