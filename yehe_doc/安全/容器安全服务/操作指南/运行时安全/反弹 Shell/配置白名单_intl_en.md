This document describes how to configure an allowlist policy.

## Filtering and Refreshing Allowed Images
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Runtime Security** > **Reverse Shell** > **Allowlist policies** on the left sidebar.
2. On **Allowlist policies** tab, click the search box and search for events by connection process.
![](https://qcloudimg.tencent-cloud.cn/raw/703b8f74906ab03688a17e0a83c89915.png)
3. On the **Allowlist policies** tab, click ![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png) on the right of the **Operation** column to refresh the allowlist.

## Adding an Allowlist Policy
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Runtime Security** > **Reverse Shell** > **Allowlist policies** on the left sidebar.
2. On the **Allowlist policies** tab, click **Add allowlist policy**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/277951fcebce2462141ff9e1830ed86c.png" style="zoom:67%;" />
3. On the **Add allowlist policy** page, configure the destination address, connection process, and scope.
   - Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) on the left of the **Destination address** and enter the IP and port.
>?
>- The IP is required.
>- IP format: Single IP (127.0.0.1); IP range (127.0.0.1–127.0.0.254); range (127.0.0.1/24).
>- Port format: 80, 8080. Separate ports by comma. Leave this field empty if there is no limit on the port.

   - Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) on the left of the connection process. Wildcards are allowed in command lines.
   - The scope of the allowlist is **All images** or **Specified images**. Click ![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png) or ![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png) to select or delete the target specified image.
>? You can press Shift to select multiple ones.

   ![](https://qcloudimg.tencent-cloud.cn/raw/95abc788068f4affe27e0ca958db39f7.png)
4. After selecting the target content, click **OK** or **Cancel**.
5. After the configuration, the destination address and connection process meeting the conditions will be allowed directly without generating an alert.

## Editing the Allowlist
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Runtime Security** > **Reverse Shell** > **Allowlist policies** on the left sidebar.
2. On the **Allowlist policies** tab, click **Edit** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/469f674b997e97c5bacdb000337524bc.png)
3. On the **Edit allowlist** page, modify the destination address, connection process, and scope.  
![](https://qcloudimg.tencent-cloud.cn/raw/377525bcb5fafd761a8fb491fa2cfe4b.png)
4. After selecting the target content, click **OK** or **Cancel**.

## Deleting the Allowlist
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Runtime Security** > **Reverse Shell** > **Allowlist policies** on the left sidebar.
2. On the **Allowlist policies** tab, click **Delete** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/ef03154793f4635bfd8b85037dba76c6.png)
3. In the pop-up window, click **Delete** or **Cancel**.
>? The allowlist cannot be recovered once deleted, and alerts will be generated when images associated with the allowlist trigger the preset policy.

## Custom List Management
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Runtime Security** > **Reverse Shell** > **Allowlist policies** on the left sidebar.
2. On the **Allowlist policies** tab, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
3. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e42a3e7c272600885d699b8355a92a06.png" style="zoom:67%;" />

### Key fields in the list
1. Images: Images for which the allowlist takes effect.
2. Connection process: Connection process for which the allowlist takes effect.
3. Target server: Server IP and port for which the allowlist takes effect.
