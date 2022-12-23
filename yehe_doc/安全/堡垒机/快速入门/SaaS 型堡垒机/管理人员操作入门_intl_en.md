This document describes operations performed by admins after logging in to the BH console, mainly including:
<dx-steps>
- Add a managed asset
- Add an Ops user
- Grant the Ops user the permission to access the asset
- Inform the Ops user of the Ops login address
- Audit the Ops user's asset access behaviors
</dx-steps>


## Prerequisites
You have [purchased BH](https://intl.cloud.tencent.com/document/product/1151/47158).

## Step 1. Add a managed asset
1. Log in to the [BH console](https://console.intl.cloud.tencent.com/bh) and select **Asset management** > **Server assets** on the left sidebar.
2. On the **Server assets** page, click **Sync**.
3. In the pop-up window, click **OK**.
>?
>- Synced regions: Hong Kong (China) and Singapore.
>- Synced asset type: CVM.
>- Before enabling automatic sync, authorize a role as instructed.
>
4. After the sync is completed, select the server on the **Server assets** page and click **Modify BH service** to bind the BH service to the server.
5. In the **Modify BH service** window, select the target BH service and click **OK**.
6. Select a server from the server list and click **Account**.
7. In the **Account management** pop-up window, click **Add asset account**, enter the asset account name, and click **OK**.
8. In the **Account management** window, click **Settings** next to **Unmanaged password**, enter the password, and click **OK**.

## Step 2. Add an Ops user
1. Log in to the [BH console](https://console.intl.cloud.tencent.com/bh) and select **User management** > **Users** on the left sidebar.
2. On the **Users** page, click **Create user**.
3. In the pop-up window, enter the required fields such as username, name, and mobile number, as well as the optional ones such as email, user group, and validity period, and click **OK**.
 
## Step 3. Grant the Ops user the permission to access the asset
1. Log in to the [BH console](https://console.intl.cloud.tencent.com/bh) and select **Permission management** > **Access permission configuration** on the left sidebar.
2. On the **Access permissions** page, click **Create access permission**.
3. On the **Create access permission** page, perform the following operations as instructed:
<dx-steps>
- Set the permission name
- Select a user
- Select an asset
- Select an asset account
- Set an access operation
- Select a high-risk command template
</dx-steps>

3. After performing the above operations, confirm the configuration information and click **Confirm and submit** for the authorization information to take effect.

## Step 4. Inform the Ops user of the Ops login address
1. Log in to the [BH console](https://console.intl.cloud.tencent.com/bh) and select **Overview** on the left sidebar.
2. On the **Overview** page, copy the link to the **Ops page** in the **Help** section and send it to the authorized Ops user.

## Step 5. Audit the Ops user's asset access behaviors
1. Log in to the [BH console](https://console.intl.cloud.tencent.com/bh) and select **Audit management** > **Session audit** on the left sidebar.
2. On the **Session audit** page, audit the operation behaviors performed by the Ops user on the managed asset.