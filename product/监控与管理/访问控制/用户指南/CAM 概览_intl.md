In the [CAM console](https://intl.cloud.tencent.com/login), the overview page have five sections: **Access Management Resources, Login URL, Sensitive Operation, Last Login Info, and Security Guide**.
- If you are logged in to the console as an authorized user, you will see the complete information as shown below:
![](https://main.qcloudimg.com/raw/01db21bb84efbe32cbf7991d77c6c2ac.jpg) 
<a id="authority"></a>
- If you are logged in to the console as an unauthorized user, you will only see **Login URL** and **Last Login Info** as shown below:
A primary account can grant permission to sub-users (or collaborators) by **QcloudCamSummaryAccess policy** to view the information on the overview page.
![](https://main.qcloudimg.com/raw/b5f5df2051187ead797afa6b52a1d858.jpg)

## Access Management Resources
Here you can see the number of users, user groups, and custom policies created in a primary account. You can click the button under the number to enter the corresponding management page.
![](https://main.qcloudimg.com/raw/4c1498665023d1af8f5943a19d633139.jpg)

## Login URL
Here you can see login URLs for sub-users and WeChat Work sub-users. Both primary accounts and sub-users can copy the URL by clicking the Copy button on the right.
![](https://main.qcloudimg.com/raw/df6adbde1788221c0646455af92e7e57.jpg)
- Sub-users: applicable to general sub-users.
- Sub-users from WeChat Work: applicable to sub-users that are created or associated through WeChat Work.

## Sensitive Operations
In this section you will see the most recent 3-day records (up to 50 records) of sensitive operations performed by all accounts under the name of your primary account. The recorded information includes account ID, operator ID, detailed sensitive operations and operation time.

![](https://main.qcloudimg.com/raw/e9249aaf9989ef5d1fbe5f95bd69dc5f.jpg)

You can also click **View All Records** to enter the CloudAudit console to view sensitive operation records in detail.

## Last Login Info
This section shows the time, IP and current account location of your last login.

![](https://main.qcloudimg.com/raw/ab524446787f2f64ca4ee54db1563ade.jpg)
<a id="more"></a>

## Security Guide
The Security Guide provides instructions for you to learn how to protect your account security through enabling MFA, enabling account protection, creating CAM users and user groups, etc.
The **Enable MFA for primary account** and **Enable protection for primary account** options are available only for the primary account;  The others are available for all authorized users.
**For the safety of your account and cloud assets, we strongly recommend that you follow this security guide to complete all the configurations step by step.**
We will see the status of your security configuratons as **Not completed** or **Completed**. You will only be able to see the status of each configuration when you are logged in with the primary account. An authorized user can click the triangle symbol on the left side of each configuration to view the corresponding feature description and entry. Below is an example of the Security Guide user interface after log-in.

![](https://main.qcloudimg.com/raw/f605c11d1e46f3171cbb663471164114.jpg)

### Enable MFA for Primary Account
Multi-factor Authentication (MFA) is a simple and efficient security authentication method. An MFA device (dynamic password card or token card) can provide an extra layer of protection for your account, on top of the username and password. Tencent Cloud offers two types of MFA devices: hardware MFA device and virtual MFA device. 
The primary account user can click **Enable MFA for primary account** under the description to enter the specific settings page. 
<!--For more information, please see:
- [Hardware MFA Device](https://intl.cloud.tencent.com/document/product/378/14520)
- [Virtual MFA Device](https://intl.cloud.tencent.com/document/product/378/14498)-->

### Enable Protection for Primary Account
A primary account user can enable login protection and operation protection.
- With the login protection enabled, a primary account user must first be authenticated by **MFA** in order to log in to Tencent Cloud. It helps prevent illegal log-ins, thus maximizing the security of the account and account assets.
- With the operation protection enabled, a primary account user must first be authenticated by **MFA** or **Mobile Verification** before performing any sensitive operations, thus preventing malicious operations.

The primary account user can click **Enable protection for primary account** under the description to enter the detail setting page.
<!--For more information, please see:
- [Login Protection](https://intl.cloud.tencent.com/document/product/378/8392)
- [Operation Protection](https://intl.cloud.tencent.com/document/product/378/10740)-->

### Create CAM Users
As a Tencent Cloud primary account user, you can create CAM users and grant them the required permissions. You can also manage different types of users, including collaborators, message recipients and sub-users. 
An authorized user can click **Create User** under the description to enter the detail setting page. For more information, please see:
- [Sub-user](https://intl.cloud.tencent.com/document/product/598/13674)
- [Collaborator](https://intl.cloud.tencent.com/document/product/598/13666)
- [Message Recipient](https://intl.cloud.tencent.com/document/product/598/13667)

### Create Groups and Add Users
As a Tencent Cloud primary account user, you can create user groups and add CAM users to the group. You can also assign permisisons to the user groups by associating them with policies. This helps you manage and allocate your account resources for greater efficiency.
An authorized user can click **Create Group** under the description to enter the detail setting page. For more information, please see:
- [User Group Management](https://intl.cloud.tencent.com/document/product/598/10599)

### Manage Authorization Policies
CAM supports two types of policies: preset policy and custom policy.
- A preset policy is a collection of common permissions created and managed by Tencent Cloud, including super admin permissions, resource management permissions. You cannot edit or make changes on preset policies.
- A custom policy is a type of policy that allows you to create, assign and manage permissions at a granular level. You can edit or make changes on custom policies.

Assigning permissions to user groups or users can simplify permission management and permission audit of the CAM users in your account.
An authorized user can click **Manage Custom Policy** under the  description to enter the detail settings page. For more information, please see:
- [Policy Management](https://intl.cloud.tencent.com/document/product/598/10601)

### Enable MFA for Sub-users
Enabling MFA for sub-users can help enhance your cloud security. With MFA enabled,  CAM users must perform secondary authentication to log in to Tencent Cloud or perform sensitive operations in Tencent Cloud. Because MFA related settings are very important to your cloud security, only primary users or users with CAM management permissions are allowed to set up MFA. 
An authorized user can click **Enable MFA for sub-users** under the description to enter the detail setting page. For more information, please see:
- **Enable MFA for Sub-users** in [Security Setting of Sub-accounts/Collaborators](https://intl.cloud.tencent.com/document/product/598/14985)

### Enable Protection for Sub-users
An authorized user can enable login protection and operation protection for sub-users.
- With the login protection enabled, a sub-user must first be authenticated by **MFA** in order to log in to Tencent Cloud. This helps prevent the illegal log-ins, thus maximizing the account security.
- With the operation protection enabled, a sub-user must first be authenticated by **MFA** or **Mobile Verification** to perform sensitive operations, so as to guarantee cloud asset security.

Enabling login protection and operation protection for sub-users (CAM users) can help keep your cloud asset safe.
An authorized user can click **Enable protection for sub-users**  under the description to enter the detail setting page:
1. Click the name of the sub-user for whom you want to enable protection to enter the user details page.
2. Click **Security Settings** in the user detail page.
3. Click **Manage MFA** on the right side of **MFA Device** to enable login protection and operation protection for the selected sub-user.

