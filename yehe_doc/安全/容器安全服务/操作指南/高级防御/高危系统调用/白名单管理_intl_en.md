The allowlist policies module displays the option to configure the allowlist and the configured allowlist.

## Filtering and Refreshing Allowed Images
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **High-risk Syscalls** > **Allowlist policies** on the left sidebar.
2. On the **Allowlist policies** tab, click the search box and search the configured allowlist by process path or syscall name.
![](https://qcloudimg.tencent-cloud.cn/raw/3af7f9a072e7259e4d5ffffc1aa4deb2.png)
3. On the **Allowlist policies** tab, click ![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png) on the right of the **Operation** column to refresh the allowlist.

## Adding an Allowlist Policy
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **High-risk Syscalls** > **Allowlist policies** on the left sidebar.
2. On the **Allowlist policies** tab, click **Add allowlist policy**.
![](https://qcloudimg.tencent-cloud.cn/raw/bf7552706d1f26034c719fe625826e81.png)
3. On the **Add allowlist policy** page, configure the target process path, syscall name, and scope.
   - Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) on the left of the **Process path** and **Syscall name**, enter the process path, and select the syscall name.
>? The process path is required.

  ![](https://qcloudimg.tencent-cloud.cn/raw/060e1bf87ac7a95c29f9d3907fb26dd0.png)
   - The scope of the allowlist is **All images** or **Specified images**. Click ![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png) or ![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png) to select or delete the target specified image.
>? You can press Shift to select multiple ones.

   ![](https://qcloudimg.tencent-cloud.cn/raw/af04a100e2244f44bd54c622c4417f71.png)
4. After selecting the target content, click **OK** or **Cancel**.

## Editing the Allowlist
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **High-risk Syscalls** > **Allowlist policies** on the left sidebar.
2. On the **Allowlist policies** tab, click **Edit** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/265a29fb233439ffd391ea8a5fbad3b3.png)
3. On the **Edit allowlist** page, modify the target process path, syscall name, and scope.  
![](https://qcloudimg.tencent-cloud.cn/raw/549e549ae6b9e422fe63af687d99fd84.png)
4. After selecting the target content, click **OK** or **Cancel**.

## Deleting the Allowlist
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **High-risk Syscalls** > **Allowlist policies** on the left sidebar.
2. On the **Allowlist policies** tab, click **Delete** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/a0b4718e31b3a45c87ff72050d3115c1.png)
3. In the pop-up window, click **Delete** or **Cancel**.
>? The allowlist cannot be recovered once deleted, and alerts will be generated when images associated with the allowlist trigger the preset policy.

## Custom List Management
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **High-risk Syscalls** > **Allowlist policies** on the left sidebar.
2. On the **Allowlist policies** tab, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
3. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/78d398e43f2ba372a820c01d2b92360b.png" style="zoom:67%;" />

### Key fields in the list
1. Images: Images for which the allowlist takes effect.
2. Process path: Process path for which the allowlist takes effect.
3. Syscall name: Syscall name for which the allowlist takes effect.
4. Operation: Editing or deleting the allowlist.
