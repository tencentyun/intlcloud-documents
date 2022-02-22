## Overview

To experience better CLS log collection service, you can upgrade the LogListener automatically or manually via the console. After the LogListener version is upgraded, you don’t need to download the latest-version installer. You can set a time period for auto upgrade or select specific machines to upgrade manually by one click.

>? 
> - Auto upgrade is supported for LogListener v2.5.0 and above. For better user experience, you are advised to [install or upgrade to the latest-version LogListener](https://intl.cloud.tencent.com/document/product/614/17414).
> - Python 2 is needed for auto upgrade.Auto upgrade cannot be performed on a LogListener with Python 3 installed.

## Directions

You can choose auto upgrade or manual upgrade.

### Auto upgrade

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. In the left sidebar, click **Machine Group** to go to the machine management page.
3. Find the target machine group, move the mouse under ![](https://main.qcloudimg.com/raw/7b707f1dcef1dc117d4446da1265e2c8.png) in the **Auto Upgrade** column, and then click **Enable Now**.

4. In the pop-up, toggle the button on and specify the upgrade time period (the default period is from the current time to two hours later, such as 08:39-10:39). 

5. Click **OK**. When the status of the target machine group changes to **Enabled** as displayed in the **Auto Upgrade** column, auto upgrade has been enabled successfully.

>?
> - You can set any time period for the auto upgrade, and the system will check if upgrade is needed every day in the specified time period. If the upgrade conditions are met, the auto-upgrade will be performed; otherwise, the operation will be performed.
> - You can select multiple target machine groups and click **Auto Upgrade** to upgrade them in batches.


### Manual upgrade

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. In the left sidebar, click **Machine Group** to go to the management page.
3. Find the target machine group, and click **Upgrade Now** in the **Operation** column. 

4. In the pop-up, check the target machine with status as **To be upgraded**, and then click **Manual Upgrade**.

The system will upgrade LogListener to the latest version by default. When you see **This is the latest version**, that means the manual upgrade is successful.


>? 
> - When the status is "Unable to upgrade", you cannot upgrade the LogListener in the console, and you need to download the latest-version installer to upgrade. For details, please see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).
> - If "Abnormal heartbeat" appears, please see [Machine Group Exception](https://intl.cloud.tencent.com/document/product/614/17424) for troubleshooting tips.
> 


