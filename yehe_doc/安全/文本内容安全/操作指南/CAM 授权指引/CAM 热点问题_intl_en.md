### How do I set a sub-user/collaborator as admin?

You can grant the sub-user/collaborator the admin permissions by assigning them the preset **AdministratorAccess** policy as instructed in *Configuring Policy for User/User Group*. The policy allows the authorized account to manage all users and their permissions, financial information, and Tencent Cloud service assets under the root account.

### How does a sub-user/collaborator get account management permission?

You can grant the sub-user/collaborator the account management permission by assigning them the preset **QcloudCamFullAccess** policy as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602). The policy allows you to manage all users and their permissions in the account.

You can also grant the sub-user/collaborator read-only access to CAM by assigning them the preset **QcloudCamReadOnlyAccess** policy.

### How does a sub-user/collaborator get the same data viewing permission as the root account?

We recommend you assign the preset **QcloudCamReadOnlyAcces** policy to the sub-user/collaborator as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602) to grant them read-only access to CAM. When they log in to the console, a user selection box will be displayed on the corresponding pages, and the default option is the current sub-account, which has the same data permissions as the root account.

>? You can also grant a sub-user/collaborator the same data viewing permission as the root account by setting them as admin. We recommend you follow the principle of least privilege when doing so.

### How do I access the financial information with a root account or financial admin account?

- Root account: log in to the Tencent Cloud console and click [Billing Center > Bills](https://console.cloud.tencent.com/expense/bill/overview) to view the usage and billing details.
- Financial admin account: you need to grant the sub-user/collaborator **financial admin permissions**, console access, and **QCloudFinanceFullAccess** as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602), so that they can manage the financial information in the account and view the usage and billing details in [Billing Center - Bills](https://console.cloud.tencent.com/expense/bill/overview) in the Tencent Cloud console.

### How do I restrict the access IPs of sub-users/collaborators?

You can set login restrictions for sub-users/collaborators in the CAM console, so that they can log in to the Tencent Cloud console only in secure environments. Specifically, you can restrict suspicious logins (from unusual login locations or 30 days after the last successful login) and allow/forbid login from specified IPs. For detailed directions, see [Login Restrictions](https://intl.cloud.tencent.com/document/product/598/33730).