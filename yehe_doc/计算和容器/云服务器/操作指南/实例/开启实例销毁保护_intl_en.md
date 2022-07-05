## Overview


To prevent instances from being terminated unexpectedly, you can enable Termination Protection.

When Termination Protection is enabled, the instance cannot be terminated in the console or by using APIs. You can disable this setting any time as necessary.

## Notes
- Instance termination protection is disabled by default. 
- Instance termination protection does not take effect at the system level; for example, when a pay-as-you-go instance is to be terminated due to overdue payment, the protection does not apply.


## Directions

### Enabling termination protection
<dx-tabs>
::: Existing instances
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index).
2. You can enable instance termination protection for one or multiple instances as needed:
 - **One instance**:
On the **Instances** page, find the target instance and click **More** > **Instance Settings** > **Instance Termination Protection**.
![](https://qcloudimg.tencent-cloud.cn/raw/15767ce2a7a65c8679352fbb72845596.png)
 - **Multiple instances**:
On the **Instances** page, select the target instances and select **More** > **Instance Settings** > **Instance Termination Protection**.
![](https://qcloudimg.tencent-cloud.cn/raw/0c2634e3199faed37d5fdfb68131a3ca.png)
3. In the **Instance Termination Protection** pop-up window, select **Enable** and click **OK*.

:::
::: Newly purchased instances

When purchasing an instance, select **Custom Configuration** and select **Instance termination protection** on the **2. Complete Configuration** tab.
![](https://qcloudimg.tencent-cloud.cn/raw/610370e5d6e195a41e6d1536564dedd9.png)
<dx-alert infotype="explain" title="">
For more information on other parameters, see [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
</dx-alert>

:::
</dx-tabs>




### Disabling instance termination protection
If you are sure that an instance can be terminated, follow the steps below to disable instance termination protection.


1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index).
2. You can disable instance termination protection for one or multiple instances as needed:
 - **One instance**:
On the **Instances** page, find the target instance and click **More** > **Instance Settings** > **Instance Termination Protection**.
![](https://qcloudimg.tencent-cloud.cn/raw/15767ce2a7a65c8679352fbb72845596.png)
 - **Multiple instances**:
On the **Instances** page, select the target instances and select **More** > **Instance Settings** > **Instance Termination Protection**.
![](https://qcloudimg.tencent-cloud.cn/raw/0c2634e3199faed37d5fdfb68131a3ca.png)
3. In the **Instance Termination Protection** pop-up window, select **Disable** and click **OK*.



## References
- [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855)
- [Terminating Instances](https://intl.cloud.tencent.com/document/product/213/4930)
