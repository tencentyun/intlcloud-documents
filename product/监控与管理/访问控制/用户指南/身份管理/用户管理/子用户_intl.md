## Overview
Sub-users are entities created by the root account. A sub-user is assigned an ID and credentials, and is able to log in to and configure console independently and has access to APIs.

## User Guide

### Create a sub-user
1. Log in to the Tencent Cloud console, go to [User](https://intl.cloud.tencent.com/login), click **New User** -> **Sub-User**, as shown below:
![](https://main.qcloudimg.com/raw/7b921ed8373241c3a0a95ffc07e31d85.png)

2. Enter user information. Here you can create sub-users in batches, set access type and console password or perform other operations, as shown below:
![](https://main.qcloudimg.com/raw/4962841547ebba72831a070dd677948a.png)

3. Set permissions. When it has been associated with a policy, the sub-user will be automatically granted the permissions described in that policy. You can give sub-user permission in 3 different ways:
 - Add sub-users to a user group: This is the best way to manage permissions for users with different roles and functions. You can grant permissions to a sub-user by adding the sub-user to an existing user group or creating a new user group. After that, the sub-user will be associated with the policies of the user group.
![](https://main.qcloudimg.com/raw/e79f64bd22c0360a81be6ede50625697.png)
 - Copy the permissions of an existing user: click **Copy Existing User's Permissions** and select the user whose permissions you want to copy, then you can associate the sub-user with the policies of that user.
![](https://main.qcloudimg.com/raw/3389a46e252f83b2a24ddd792f9acd57.png)
 - Use the policy list: Click **Grant Permissions from Policy List**, and then select the policies you want to associate with the sub-user.
 ![](https://main.qcloudimg.com/raw/0aa27768d3eeb74b2ff47a3e97f13339.png)
4. You can email the complete information, or save some of the information to a local Excel file, as shown below:
![](https://main.qcloudimg.com/raw/48b723b38d8913f04dc8e23a6e59b82b.png)

5. Click **Done**.

### Associate a sub-user with policies

#### Direct association
1. Log in to the Tencent Cloud console, go to [User](https://intl.cloud.tencent.com/login) and select the sub-user you want to associate the polices with, then click **Authorize** in the **Operation** column, as shown below:
![](https://main.qcloudimg.com/raw/d431d6825c51120e9e462237c315f1ea.png)
2. Select the policies to be associated, and then click **OK**.
![](https://main.qcloudimg.com/raw/fb9779cbd6cef71554fa44aa7695b9ba.png)

#### Association with policies by joining groups
1. Log in to the Tencent Cloud console, go to [User](https://intl.cloud.tencent.com/login), select the sub-user you want to authorize, and then click **More** -> **Add to Group** in the **Operation** column.
![](https://main.qcloudimg.com/raw/35fec2c0af30fbc085e1dbb2c6f2a4e1.png)
2. Select the user group to which you want to add the sub-user, and then click **OK**.


### Disassociate a sub-user from policies

#### Direct disassociation
1. Log in to the Tencent Cloud console, go to [User](https://intl.cloud.tencent.com/login), select the sub-user you want to disassociate from the policies, and then click the sub-user name to enter the details page.
![](https://main.qcloudimg.com/raw/c0a52eb5fa8cdffa50a3ac5cb60760e2.png)
2. Click **Associated Policies**, choose the policies to be disassociated in the list, and then click **Disassociate** on the right.
![](https://main.qcloudimg.com/raw/5f47772dd8a3979f943404602a0137c3.png)
3. Click **Disassociate**.

#### Remove a sub-user from a user group
1. Log in to the Tencent Cloud console, go to [User](https://intl.cloud.tencent.com/login), select the sub-user you want to disassociate from the policies, and then click the sub-user name to enter the detail page.
![](https://main.qcloudimg.com/raw/6c61bef73a33142298a11937f7204626.png)
2. Click **Associated Policies**, in the list choose the policies you want to disassociate, and then click **Disassociate** on the right.
![](https://main.qcloudimg.com/raw/cb8fa7fea27df5b61aab292b4e576292.png)
3. Click **Disassociate** to remove the sub-user from the user group. The sub-user is now disassociated from the policies of that user group.

### Subscribe a sub-user to messages
1. Log in to the Tencent Cloud console, go to [User](https://intl.cloud.tencent.com/login), select the sub-user for whom you want to subscribe to messages service, and then click **More** -> **Subscribe to Messages** in the **Operation** column, as shown below:
![](https://main.qcloudimg.com/raw/0eccae84ffb092837cb37ca9e4de7569.png)
2. Select the desired message type and click **OK**.
![](https://main.qcloudimg.com/raw/0f77e3303cd8b19d5e99ef7af00721d6.png)

### View sub-user information in **User List** -> **Details**

1. Log in to the Tencent Cloud console, go to [User](https://intl.cloud.tencent.com/login), select the sub-user you want to view, and then click **details** on the left, as shown below:
 ![](https://main.qcloudimg.com/raw/155fd1de3e96e998fcce98c07ad975a5.png)


### Search for sub-users using search box
1. Log in to the Tencent Cloud console, go to [User](https://intl.cloud.tencent.com/login), enter the keyword in the search box at the upper right corner, and then click **search**. 
![](https://main.qcloudimg.com/raw/4e02a8f8ca32ab753c18bc0e7d033330.png)
>The search box supports multi-keyword search (separated by a space). You can search for sub-users by using keywords such as username, ID, mobile number, email and remarks.



### Delete a sub-user

#### Delete a single sub-user
1. Log in to the Tencent Cloud console, go to [User](https://intl.cloud.tencent.com/login), select the sub-user you want to delete, and then click **More** -> **Delete** in the **Operation** column, as shown below:
![](https://main.qcloudimg.com/raw/83a26b84ac282d64354796115b996cab.png)

2. Click **Delete**.


#### Delete multiple sub-users
1. Log in to the Tencent Cloud console, go to [User](https://intl.cloud.tencent.com/login), in the user list select multiple sub-users you want to delete, and then click **Delete** at the upper left corner, as shown below:
![](https://main.qcloudimg.com/raw/476873d2cf57da621a41967c7c725904.png)

2. Click **Delete**.

