## Overview
If you no longer need a Lighthouse instance, you can terminate it. Once its status becomes **Returned** or **To be repossessed**, it no longer incurs fees. For instances to be repossessed, you can renew (restore) or completely terminate them based on different scenarios and needs.

This document describes how to terminate Lighthouse instances in different status in the console.
<dx-alert infotype="explain" title="">
Currently, Lighthouse supports the sensitive operation protection feature to effectively protect the security of account resources. It can be enabled in [security settings](https://console.cloud.tencent.com/developer/security). Instance termination is a sensitive operation.
</dx-alert>



## Directions
### Terminating running/shutdown Lighthouse instances

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse).
2. Find the target Lighthouse instance in the instance list and enter its details page.
3. In the **Billing information** section on the **Overview** tab on the instance details page, select **Terminate/Return** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/67b603961cd8630f076cb8bf6a63e534.png)
4. In the pop-up window, if the instance is mounted with data disks, you can select **Return data disks mounted to the instance** to terminate the data disks at the same time as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/3ee8c1c1f31d1fee97307aa3b366d06b.png)
5. Select **Read and agree to [refund rules](https://intl.cloud.tencent.com/document/product/1103/41406)** and click **OK**.
6. Check and confirm the Lighthouse refund information and click **OK**. After the information is submitted, the system will refund and terminate the instance. Once terminated, the instance will enter the **To be repossessed** status.
<dx-alert infotype="explain" title="">
- If your instance is not renewed within seven (included) days after entering the **To be repossessed** status, the system will release it in around 24 hours. After release, all data on the instance will be cleared and cannot be recovered.
- Instances in **To be repossessed** status are unavailable, which indicates that they can neither be managed nor accessed.
- If the Lighthouse instance to be terminated contains a renewal order that hasn't taken effect, the order will also be refunded after instance termination.
- After a data disk is terminated, it will enter the **To be repossessed** status and be retained for seven days. If you confirm that you don't need to retain the data, you can completely terminate the cloud disk.
</dx-alert>




### Terminating to-be-repossessed Lighthouse instance



<dx-alert infotype="notice" title="">
This operation will terminate an instance completely from the account's instance list, and the instance cannot be restored through renewal or other methods. Therefore, proceed with caution.
</dx-alert>


1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse).
2. Find the target Lighthouse instance in **To be repossessed** status in the instance list and click **More** > **Terminate/Return** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/9edd38e07445ffe5c3097db3689417d5.png)
3. In the pop-up window, select **Read and agree** and click **OK** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/3b33a569f3160a80101ec35db9b5bc11.png)
