In the [CAM console](https://console.cloud.tencent.com/cam), the overview page have five modules: **Access Management Resources, Login URL, Sensitive Operation, Last Login Info, and Security Guide**, as shown below.
- If you are log in to the console as an authorized user, you will see the below information；
![](https://main.qcloudimg.com/raw/d435c8e7cf7ed16659b33d73da41fa01.png) 
<a id="authority"></a>
- If you are log in to the console as an unauthorized user, we will only see the **Login URL** and **Last Login Info** as shown below:
A primary account can grant authorization to sub-users (or collaborators) by the **QcloudCamSummaryAccess policy**, allowing them to view the information in the console overview page.
![](https://main.qcloudimg.com/raw/43041356d65e8f0076f5846d224847b7.png)

## Access Management Resources
Here you can see the number of users, user groups, and custom policies created under the primary account. Also, you can click the button below a specific number to enter the main management page.
![](https://main.qcloudimg.com/raw/eb4a27aef033d26e1b5ac2314f6ddf25.png)

## Login URL
Here you can see login URLs for sub-users and WeChat Work sub-users. Both the primary account and sub-users are allowed to copy the URL through the Copy button on the right side of the URL.
![](https://main.qcloudimg.com/raw/d68b8ed3cfe89966bc1e556a2240edae.png)
- Sub-users: applicable to general sub-users.
- Sub-users from WeChat Work: applicable to sub-users created or associated through WeChat Work.

## Sensitive Operation
The Sensitive Operation module displays the sensitive operation records (up to 50 records) of all accounts under the primary account in last 3 days, including account ID, operator ID, detailed sensitive operation and operation time.
![](https://main.qcloudimg.com/raw/82fdaeb9cb8135c6eef97e64d37db04f.png)
You can also click **View All Records** to enter the CloudAudit console to view sensitive operation records in detail.

## Last Login Info
The Last Login Info module shows the last login time, IP, and location of the current account.
![](https://main.qcloudimg.com/raw/e48475cba7fea457c552c30abba5af92.png)
<a id="more"></a>
## Security Guide
The Security Guide module provides instructions on how to use basic CAM features and necessary security operation guides, including enabling MFA, enabling account protection, and creating CAM users and user groups.
The **Enable MFA for primary account** and **Enable protection for primary account** options are available only for the primary account. The other five options are available for all authorized users.
**To protect your account and cloud assets, we strongly recommend that you complete all the configurations in Security Guide.**
Each option can be in the **Not completed** or **Completed** status. If a primary account user log in to the console, the status of each option will be displayed. But authorized non-primary account users cannot view these statuses.
An authorized user can click the triangle symbol on the left side of each option to view the corresponding feature description and configuration entry. The figure below shows an example of the Security Guide module after the primary account user logs in to the console.
![](https://main.qcloudimg.com/raw/8b1276706131c07170af03fcefe54ad0.png)

### Enable MFA for Primary Account
Multi-factor Authentication (MFA) is a simple and efficient security authentication method. An MFA device (dynamic password card or token card) can provides an extra layer of protection for your account, besides your username and password. Tencent Cloud offers two types of MFA devices: hardware MFA device and virtual MFA device. 
The primary account user can click **Enable MFA for primary account** below the detailed description to enter the specific settings page. For more information, please see:
- [Hardware MFA Device](https://cloud.tencent.com/document/product/378/14520)
- [Virtual MFA Device](https://cloud.tencent.com/document/product/378/14498)

### Enable Protection for Primary Account
A primary account user can enable login protection and operation protection.
- With the login protection enabled, a primary account user must first verify the identity by **MFA** to log in to Tencent Cloud. It helps to prevent the account from being illegally logged in by others who know its password, thus maximizing the security of the account and assets under the account.
- With the operation protection enabled, a primary account user must first verify the identity by **MFA** or **Mobile Verification** before performing sensitive operations, thus avoiding malicious use by others. 

The primary account user can click **Enable protection for primary account** below the detailed description to enter the specific settings page. For more information, please see:
- [Login Protection](https://cloud.tencent.com/document/product/378/8392)
- [Operation Protection](https://cloud.tencent.com/document/product/378/10740)

### Create CAM Users
Create CAM users and grant them the required permissions. A primary account user of Tencent Cloud can manage different types of users with different roles using the user management feature. User types include collaborator, message recipient and sub-user. 
An authorized user can click **Create User** below the detailed description to enter the specific settings page. For more information, please see:
- [Sub-user](https://cloud.tencent.com/document/product/598/13674)
- [Collaborator](https://cloud.tencent.com/document/product/598/13666)
- [Message Recipient](https://cloud.tencent.com/document/product/598/13667)

### Create Groups and Add Users
Create a user group and add CAM users. Associate appropriate policies with this user group to assign different permissions. This can help you manage and allocate account resources for greater productivity.
An authorized user can click **Create Group** below the detailed description to enter the specific settings page. For more information, please see:
- [User Group Management](https://cloud.tencent.com/document/product/598/10599)

### Manage Authorization Policies
CAM supports two types of policies: preset policy and custom policy.
- A preset policy is a collection of some common permissions created and managed by Tencent Cloud, such as super admin permissions, resource management permissions, which has a rough granular. These policies cannot be edited.
- A custom policy created by users allows you to assign permissions with a fine granular. These policies can be edited. 

Assigning permissions to user groups or users can simplify your permission management and audit of CAM users in your account.
An authorized user can click **Manage Custom Policy** below the detailed description to enter the specific settings page. For more information, please see:
- [Policy Management](https://cloud.tencent.com/document/product/598/10601)

### Enable MFA for Sub-users
Enabling MFA for sub-users can help enhance the security of your cloud assets. With MFA enabled for CAM users, CAM users must perform secondary authentication to log in to Tencent Cloud or perform sensitive operations in Tencent Cloud, so as to guarantee asset security. The related MFA settings are important for the cloud asset security. Sub-users or collaborators can only accept the security attributes set by the primary account or users with CAM management permissions.
An authorized user can click **Enable MFA for sub-users** below the detailed description to enter the specific settings page. For more information, please see:
- **Enable MFA for Sub-users** in [MFA Configuration Guide](https://cloud.tencent.com/document/product/598/14985)

### Enable Protection for Sub-users
An authorized user can enable login protection and operation protection for sub-users.
- With the login protection enabled, a sub-user must first verify the identity by **MFA** to log in to Tencent Cloud. It helps to prevent the account from being illegally logged in by others who know its password, thus maximizing the security of the account and assets under the account.
- With the operation protection enabled, a sub-user must first verify the identity by **MFA** or **Mobile Verification** to perform sensitive operations, so as to guarantee the asset security.

Enabling login protection and operation protection for sub-users (CAM users) can help enhance the security of your cloud assets.
An authorized user can click **Enable protection for sub-users** below the detailed description to enter the specific settings page:
1. Click the name of the sub-user for whom you want to enable protection to enter the user details page.
2. Click **Security Settings** in the user details page.
3. Click **Manage MFA** on the right side of **MFA Device** to enable login protection and operation protection for the selected sub-user.

