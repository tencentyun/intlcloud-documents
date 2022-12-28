
### Can I define and manage my organization by region?
No. All organization entities are accessible across all regions. There is no need to specify the region when creating and managing an organization. Users under Tencent Cloud accounts can use this service in all regions where Tencent Cloud is available.

### Can I change the Tencent Cloud account used as the root account?
No. You should carefully select the root account.

### How do I add a Tencent Cloud account to my organization?
You can do this by inviting or creating a member as instructed in [Adding Organization Member](https://www.tencentcloud.com/document/product/1031/51865).


### Can a Tencent Cloud account join multiple organizations?
No.

### Can I set multi-factor authentication (MFA) for a Tencent Cloud account created in an organization through programming?
No.


### How many Tencent Cloud accounts can be managed in an organization?
Currently, up to 100 accounts can be managed in an organization. To manage more accounts, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.

### How do I delete a Tencent Cloud member account from an organization?
You can delete a member account in two ways:
**Option 1:** Delete an invited member account by logging in with the root account.
(1) Log in to the [TCO console](https://console.cloud.tencent.com/organization) as the root account admin.
(2) Select **Member list** on the left sidebar.
(3) Select the target account and click **Delete member**.

**Option 2:** Delete an invited member account by logging in with the member account.
(1) Log in to the target member account as the admin.
(2) Go to the TCO console.
(3) Select **Quit organization**.

### How do I create a department?
You can create a department as follows:
1. Log in to the [TCO console](https://console.cloud.tencent.com/organization) as the root account admin.
2. Select **Department management** on the left sidebar.
3. Select the target location in the organizational structure. You can create a department under the root directly or under another unit.
4. Select **Create department** and enter a department name, which must be unique in your organization.

<dx-alert infotype="notice" title="">
You can rename the department later.
</dx-alert>

Then, you can add Tencent Cloud accounts to this unit.

### How do I add a Tencent Cloud account to a department?
You can add a member account to a department as follows:
1. Select **Department management** in the TCO console.
2. Select the target Tencent Cloud account and click **Move member**.
3. In the pop-up window, select the target department.

### Can a Tencent Cloud account join multiple departments?
No.

### How many levels of departments can an organization have?
An organizational structure can have up to five levels of nested department nodes from the admin root to the Tencent Cloud accounts in the lowest department.
