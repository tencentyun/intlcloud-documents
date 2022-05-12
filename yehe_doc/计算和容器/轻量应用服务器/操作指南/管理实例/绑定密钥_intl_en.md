## Overview
This document describes how to bind the specified key to an instance on the instance details page in the Lighthouse console.

## Prerequisites
- You can bind a key to only a Linux instance.
- You have created and saved a key. For more information, see [Creating SSH key](https://intl.cloud.tencent.com/document/product/1103/41392#directions).

## Directions

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index) and click the card of the target instance.
2. On the instance details page, select the **SSH key pair** tab and click **Bind Key Pair**.
3. In the **Bind key** pop-up window, perform the following operations based on the instance status:
<dx-tabs>
::: Running instance
1. In the **Select a key** step, select the target key and click **Next** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ee7c7af4b10044247662566d22b72839.png)
2. In the **Shutdown instance** step, select **Agree to a forced shutdown** and click **OK**.
<dx-alert infotype="explain" title="">
- During the binding process, the instance will shut down first and then start up, and the business will be interrupted momentarily. We recommend you do so during off-peak hours.
- If the instance fails to shut down normally, it will be forced to shut down. Forced shutdown may cause data losses or file system corruption. Therefore, perform forced shutdown with caution.
- Forced shutdown may take a while. Please be patient.
</dx-alert>



:::
::: Shutdown instance
1. In the **Select a key** step, select the target key and click **Next** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/4dea54103d35df0af4d507f3f4b892de.png)
2. In the **Shutdown instance** step, click **OK**.
:::
</dx-tabs>
<dx-alert infotype="notice" title="">
To improve the Lighthouse instance security, after a Linux instance is bound to a key, login to the `root` account with a password will be forbidden by default. If you want to keep the password login method, modify the configuration as instructed in [Modifying SSH configuration](https://intl.cloud.tencent.com/document/product/1103/41392#.3Ca-id.3D.22changessh.22.3Emodifying-ssh-configuration.3C.2Fa.3E).
</dx-alert>

## Related Operations
### Unbinding key
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index) and click the card of the target instance.
2. On the instance details page, select the **SSH key pair** tab.
3. Select the target key pair and click **Unbind** above the list as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/d7de6a4e40b97f0dfb825bf2b29e6df8.png)
4. In the **Unbind key** pop-up window, perform the following operations based on the instance status:
<dx-tabs>
::: Running instance
1. In the **Select a key** step, confirm the target key and click **Next** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/1747313d9fff9892263985870321e988.png)
2. In the **Shutdown instance** step, click **OK**.
:::
::: Shutdown instance
1. In the **Select a key** step, confirm the target key and click **Next** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/cf24adacd0a8f3a5be5648d70cb9e6c9.png)
2. In the **Shutdown instance** step, click **OK**.
:::
</dx-tabs>


## References
- [Managing Key](https://intl.cloud.tencent.com/document/product/1103/41392)
- [Logging in to Linux Instance via Remote Login Software](https://intl.cloud.tencent.com/document/product/1103/41524)
- [Logging in to Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/1103/41525)
