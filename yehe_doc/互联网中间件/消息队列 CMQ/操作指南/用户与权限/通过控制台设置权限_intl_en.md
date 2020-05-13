## Operation Scenarios
This document uses **write permissions for message consumption and batch message consumption** of the CMQ queue model as an example to describe how to grant a user CMQ permissions.

## Permission Description
Before CAM is activated, all the original sub-accounts (sub-users and collaborators) can log in to the CMQ Console and view the resource list of the root account (through the `list` API permission and formerly by using the root account key). After CAM is connected, sub-accounts do not have the root account's resource list permission by default (the sub-account key is used for console login). It can get access only after it is authorized by the root account in CAM.

The console will call CMQ APIs; therefore, if a sub-account needs to view queues, topics, and subscription information in the console, permissions need to be granted to CMQ APIs called in the console; otherwise, the error of no permission will occur when the sub-account tries to view information in the console. Below are the APIs that need to be authorized for different console pages:
- Viewing queue list in console: authorize the `ListQueue` API
- Viewing topic list in console: authorize the `ListTopic` API
- Viewing subscription list in console: authorize the `ListSubscriptionByTopic` API

If the sub-account also wants to access CMQ in the console, it needs to be granted permissions of the corresponding APIs. **If it wants to view monitoring data in the console, it needs to be granted permissions of Cloud Monitor APIs in CAM.**


## Directions
### Creating sub-user
1. Log in to the **[CAM Console](https://console.cloud.tencent.com/cam)**, click **User List**, and click **Create User** in the top-left corner.
2. On the user creating page, select the user type and enter the user information.
If the user needs to log in to the Tencent Cloud Console or call TencentCloud APIs, you need to check **Tencent Cloud Console Access** and enter the user's QQ account as the login credential.
For more information on accounts, please see [User Types](https://intl.cloud.tencent.com/document/product/598/32633).
>You are recommended to use a QQ account that has not signed up for Tencent Cloud as the QQ account of the sub-account. (Sub-accounts do not need to top up as CMQ fees will be deducted from the balance of the root account.)
3. Associate policies with the user (after being associated with a policy, the user can be granted the permissions described in the policy). For detailed directions, please see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
4. In the **User Management** list, you can view the added sub-user.

### Creating custom policy
You can create a custom policy to enable the permission of a specific API, e.g., specifying write permission (message consumption and batch message consumption) of CMQ queues.
For detailed directions, please see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
>The `list` API permissions of CMQ are all enabled by default (i.e., you can view the specific resource lists in the CMQ Console after logging in). You can use the permissions to control what resource content can be displayed.

### Logging in as sub-user
After logging in by using a sub-account, if you cannot find the target resource, please switch to the collaborator developer account in the top-right corner in the console.

