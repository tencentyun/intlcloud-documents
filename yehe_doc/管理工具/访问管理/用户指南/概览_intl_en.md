
The Dashboard in the [CAM Console](https://console.cloud.tencent.com/cam/overview) contains five modules: **CAM Resources**, **Login URL**, **Sensitive Operations**, **Last Login Info**, and the **Security Guide**. This documents describes each module in detail.
- Users associated with the `QcloudCamSummaryAccess` policy can view the information of all modules when they log in to the console as shown below:
![](https://main.qcloudimg.com/raw/01db21bb84efbe32cbf7991d77c6c2ac.jpg)
- Users not associated with the `QcloudCamSummaryAccess` policy will only see the **Login URL** and **Last Login Info** modules as shown below:
The root account can authorize sub-accounts through the `QcloudCamSummaryAccess` policy as needed to allow them to view the Dashboard information in the console.
![](https://main.qcloudimg.com/raw/b5f5df2051187ead797afa6b52a1d858.jpg)

## CAM Resources
The CAM resources module displays the numbers of users, user groups, custom policies, roles, and identity providers created under the current root account. You can create more resources by clicking the button below each resource quantity.
![](https://main.qcloudimg.com/raw/4c1498665023d1af8f5943a19d633139.jpg)
## Login URL
The login URL module displays the login URL for the sub-user. Both the root account and the sub-account can copy the URL by clicking **Copy** icon to the right of the URL.
![](https://main.qcloudimg.com/raw/df6adbde1788221c0646455af92e7e57.jpg)
- Sub-user login link: applies to sub-users.

## Sensitive Operations
The sensitive operations module displays the overview information of all sensitive operations under the current root account in the last 3 days (up to 50 entries). The displayed information includes account ID, operator ID, sensitive operation details, and operation time. You can also click **View All Records** to enter the Cloud Audit Console to view more detailed sensitive operation records.
![](https://main.qcloudimg.com/raw/e9249aaf9989ef5d1fbe5f95bd69dc5f.jpg)


## Last Login Info
The last login info module displays the last login time and IP of the current account.
![](https://main.qcloudimg.com/raw/a0270ed9f12a9c4851e9f744bd8c7ec0.png)
<a id="more"></a>
## Security Guide
>For the security of your accounts and assets in Tencent Cloud, you are strongly recommended to complete all the configurations in the security guide.
>
The security guide module provides basic CAM feature descriptions and necessary security operation guidance, such as binding MFA devices to root accounts, enabling account protection for root accounts, creating sub-accounts, and creating groups and adding sub-accounts.
>- Operation permission: the **Bind MFA Device to Root Account** and **Enable Account Protection for Root Account** features can only be done by the root account, while the other five features can be completed by all authorized users.
>- Feature status: each feature has two states: **Not Completed** and **Completed**. The root account user can view the status of each feature. Sub-accounts cannot view feature statuses.
>- Feature links: sub-accounts with permissions can view feature descriptions and links by clicking the triangle icon to the left of each guide item. The following figure shows the security guide module the root account sees.
![](https://main.qcloudimg.com/raw/f605c11d1e46f3171cbb663471164114.jpg)

### Binding MFA device to root account
Multi-factor authentication (MFA) is an additional layer of security protection provided by Tencent Cloud besides authentication with username and password. Currently, two types of MFA devices are supported: hardware MFA devices and virtual MFA devices.
The root account user can click **Bind MFA Device** below the detailed description to enter **Security Settings**. For detailed directions, please see:
- [Hardware MFA Device](https://intl.cloud.tencent.com/document/product/378/32528)
- [Virtual MFA Device](https://intl.cloud.tencent.com/document/product/378/32528)

### Enabling account protection for root account
Account protection includes login protection and operation protection. After login protection is enabled, you need to verify your identity through MFA when logging in to the Tencent Cloud Console. After operation protection is enabled, you need to verify your identity through MFA when performing sensitive operations.
The root account user can click **Enable Account Protection** below the detailed description to enter **Security Settings**. For detailed directions, please see:
- [Login Protection](https://intl.cloud.tencent.com/document/product/378/8392)
- [Operation Protection](https://intl.cloud.tencent.com/document/product/378/10740)

### Creating a sub-account
Types of sub-account include sub-users, collaborators, and message recipients. You can create sub-accounts with different responsibilities to assist you according to your business needs.
An authorized user can click **Create User** below the detailed description to create a user. For detailed directions, please see:
- [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674)
- [Creating a Collaborator](https://intl.cloud.tencent.com/document/product/598/32639)
- [Creating a Message Recipient](https://intl.cloud.tencent.com/document/product/598/13667)

### Creating a group and adding sub-accounts
Creating, assigning permissions to, and adding users to user groups can help simplify permission management and review for sub-accounts.
An authorized user can click **Create Group** below the detailed description to create a user group. For detailed directions, please see:
- [User Group Management](https://intl.cloud.tencent.com/document/product/598/10599)

### Managing authorization policy
CAM supports two types of policies: preset policies and custom policies.
- A preset policy is a set of common permissions created and managed by Tencent Cloud at a coarse granularity. It is non-editable.
- A custom policy is created by yourself and allows you to assign permissions at a finer granularity. It is editable. 

Assigning permissions to user groups or users simplifies the process of managing and reviewing the permissions of CAM users in your account.
An authorized user can click **Create Custom Policy** below the detailed description to the **Policies** page. For detailed directions, please see:
- [Policy](https://intl.cloud.tencent.com/document/product/598/10601)

### Enabling account protection for sub-account
An authorized user can select a sub-account in the user list and enable login protection and operation protection on the **Security** tab in the user’s details page. MFA will then be required when the user logs in or performs sensitive operations. Currently, MFA modes supported for sub-accounts include virtual MFA device verification, hardware MFA device verification, and mobile verification code.
An authorized user can click **Enable Account Protection for Sub-Account** below the detailed description to enter the **User List** page. For detailed directions, please see:
- [Setting Security Protection for Sub-Users](https://intl.cloud.tencent.com/document/product/598/32657)
- [Setting Security Protection for Collaborators](https://intl.cloud.tencent.com/document/product/598/32660)

### Binding MFA device to sub-account
An authorized user can select a sub-user or collaborator in the user list and enable MFA device protection on the **Security** tab in the user’s details page. The user will need to bind the MFA device upon next login.
An authorized user can click **Bind MFA Device to Sub-Account** below the detailed description to enter the **User List** page. For detailed directions, please see:
- [Setting Security Protection for Sub-Users](https://intl.cloud.tencent.com/document/product/598/32657)
- [Setting Security Protection for Collaborators](https://intl.cloud.tencent.com/document/product/598/32660)

## Use Limits
For more information on the limits of the number of sub-accounts, user groups, and policies allowed, please see [Limits](https://intl.cloud.tencent.com/document/product/598/10609).

