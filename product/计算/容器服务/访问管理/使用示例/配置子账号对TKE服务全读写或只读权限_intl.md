## Operation Scenario

You can grant a user the permissions to view and use specific resources in the TKE console by using a CAM policy. The examples in this document guide you through the process of configuring certain permissions in the console.

## Steps

### Configuring Full Read/write Permission

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. In the left navigation pane, click [Policies](https://console.cloud.tencent.com/cam/policy) to go to the policy management page.
3. On the "Policy management" page, click **Associate a user/group** in the row of **QcloudCCSFullAccess** policy. See the figure below:
![QcloudCCSFullAccess policy](https://main.qcloudimg.com/raw/c695ca64920265a99815814d9c89de48.png)
4. In the **Associate a user/user** window that pops up, select the account that needs full read/write permission for the TKE service, and click **OK** to grant full read/write permission for the TKE service to the sub-accounts.
5. On the "Policy management" page, click **Associate a user/group** in the row of **QcloudCCRFullAccess** policy. See the figure below:
![QcloudCCRFullAccess policy](https://main.qcloudimg.com/raw/00a475b724671615217205c57bdcff63.png)
6. In the **Associate a user/group** window that pops up, select the account that needs full read/write permission for Image Registry, and click **OK** to grant full read/write permission for Image Registry to the sub-accounts.
> If you want to use the trigger and automatic building features of Image Registry, you also need to configure additional permissions for TKE - continuous integration (CCB).

### Configuring Read-only Permission

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. In the left navigation pane, click [Policies](https://console.cloud.tencent.com/cam/policy) to go to the policy management page.
3. On the "Policy management" page, click **Associate a user/group** in the row of **QcloudCCSReadOnlyAccess** policy. See the figure below:
![QcloudCCSReadOnlyAccess policy](https://main.qcloudimg.com/raw/9e08736c48dd13bfb96c70abf36300f3.png)
4. In the **Associate a user/user** window that pops up, select the account that needs read-only permission for the TKE service, and click **OK** to grant read-only permission for the TKE service to the sub-accounts.
5. On the "Policy management" page, click **Associate a user/group** in the row of **QcloudCCRReadOnlyAccess** policy. See the figure below:
![QcloudCCRReadOnlyAccess policy](https://main.qcloudimg.com/raw/fe1dabaac6b5b812072222860b9b86e3.png)
6. In the **Associate a user/group** window that pops up, select the account that needs read-only permission for Image Registry, and click **OK** to grant read-only permission for Image Registry to the sub-accounts.
> If you want to use the trigger and automatic building features of Image Registry, you also need to configure additional permissions for TKE - continuous integration (CCB).

