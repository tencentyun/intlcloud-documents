### Can I define and manage my organization by region?
No. All organization entities can access all regions. There is no need to specify the region when creating and managing an organization. Users of Tencent Cloud accounts can use this service in all regions where Tencent service is provided.
### Can I change the master account?
No. The master account cannot be changed, so please select your master account with care.
### How do I add a Tencent Cloud account to my organization?
You can add a Tencent Cloud account to your organization in two ways:
Invite an existing account to join your organization
1. Log in as the master account administrator and navigate to the [Tencent Cloud Organization](https://console.cloud.tencent.com/organization).
2. Select the Member Management tab.
3. Select **Member List** and then select **Invite Member**.
4. Provide the email address of the account you want to invite or the Tencent Cloud account ID of the account.

The specified Tencent Cloud accounts will receive an email inviting them to join your organization. The administrator of the invited Tencent Cloud account must use the Tencent Cloud Organization console to accept or decline the invitation. If the corresponding administrator accepts your invitation, the account will appear in the member account list for your organization.

### Can one Tencent Cloud account be a member of more than one organization?
No. Each Tencent Cloud account can only be the member of one organization at a time.
### Can a Tencent Cloud account created in an organization set up multi-factor authentication (MFA) using a program?
No. This operation is currently not supported.
### Can Tencent Cloud accounts created by Tencent Cloud Organization move to other organizations?
Yes. However, this account must first be removed from your organization so that it is an independent account (see below). When the account is an independent account, it can be invited to join another organization. 
### How many Tencent Cloud accounts can be managed in an organization?
Currently, one organization can manage 100 accounts. If you need to manage more accounts, please contact customer service or submit a ticket.

### How do you delete a Tencent Cloud member account from the organization?
You can delete a member account in two ways:
**Method 1: **Delete invited member account by logging in with master account
1. Log in as the master account administrator and then navigate to the [Tencent Cloud Organization](https://console.cloud.tencent.com/organization).
2. Select the **Member List** in the left sidebar.
3. Select the account to be deleted and then select **Delete Member**.

**Method 2: **Delete invited member account by logging in with member account
1. Log in as the administrator to the member account to be deleted from the organization.
2. Navigate to the Tencent Cloud Organization console.
3. Select **Quit Tencent Cloud Organization**.

### How do you create organizational units?
To create organizational units, follow these steps:
1. Log in as the master account administrator and navigate to the [Tencent Cloud Organization](https://console.cloud.tencent.com/organization).
2. Select the **Organization Structure** tab.
3. Select the structural location of the unit you want to create. You can create it either directly under the root, or in another organizational unit.
4. Select **Create Unit** and then provide a name for this organizational unit. This name must be unique within your organization.

>! You can rename this organizational unit later.

Now you can add Tencent Cloud accounts to this organizational unit.

### How do you add member Tencent Cloud accounts to organizational units?
Add member accounts to organizational units using the following steps:
1. In the Tencent Cloud Organization console, select the **Organization Structure** tab.
2. Select the corresponding Tencent Cloud account and then select **Move Member**.
3. In the dialog box, select the organizational unit that you want to move the Tencent Cloud account to.

### Can one Tencent Cloud account be a member of more than one organizational unit?
No. Each Tencent Cloud account can only be the member of one organizational unit at a time.

### Can one organizational unit be the member of more than one organizational unit?
No. Each organizational unit can only be the member of one organizational unit at a time.

### How many levels can an organizational unit hierarchy have?
You can nest three levels in an organizational unit. A organizational unit hierarchy can have four levels, including the top organizational unit to the Tencent Cloud accounts inside the lowest organizational unit level.
