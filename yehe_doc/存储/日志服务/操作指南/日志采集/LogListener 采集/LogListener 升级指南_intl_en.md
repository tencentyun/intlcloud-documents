## Overview

To experience better CLS log collection service, you can upgrade the LogListener automatically or manually via the console or semi-automatically via scripts. After the LogListener version is upgraded, you don't need to download the latest-version installer. You can set a time period for auto upgrade or select specific machines to upgrade manually by one click.

>? 
> - Auto upgrade is supported for LogListener v2.5.0 and later. For a better user experience, we recommend you [install or upgrade to the latest version of LogListener](https://intl.cloud.tencent.com/document/product/614/17414).
> - The auto upgrade feature requires Python 2. If Python 3 is installed on the collection machine, the upgrade process will not be fully executed.
> - The script-based semi-auto upgrade feature requires Python 2.7. If this version is not installed on the collection machine, this upgrade mode cannot be used.
>

You can choose auto upgrade or manual upgrade for LogListener in the console.
If Agent upgrade fails or auto upgrade cannot be used due to version restrictions, you can use the semi-auto upgrade mode.

## Directions

<span id="AutoUpdate"></span>

### Auto upgrade

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Machine Group** to enter the management page.
3. Find the target machine group, move the cursor under ![](https://main.qcloudimg.com/raw/7b707f1dcef1dc117d4446da1265e2c8.png) in the **Auto Upgrade** column, and click **Enable Now**.

4. In the pop-up, toggle the button on and specify the upgrade time period (the default period is from the current time to two hours later, such as 08:39-10:39).

5. Click **OK**. When the status of the target machine group changes to **Enabled** as displayed in the **Auto Upgrade** column, auto upgrade has been enabled successfully.

>?
> - You can set any time period for the auto upgrade, and the system will check if upgrade is needed every day in the specified time period. If the upgrade conditions are met, the auto-upgrade will be performed; otherwise, the operation will be performed.
> - You can select multiple target machine groups and click **Auto Upgrade** to upgrade them in batches.
> 

<span id="ManualUpdate"></span>
### Manual upgrade

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Machine Group** to enter the management page.
3. Find the target machine group and click **Upgrade Now** in the **Operation** column.

4. In the pop-up window, select the target machine with status as **To be upgraded** and click **Manual Upgrade**.

The system will upgrade LogListener to the latest version by default. When you see **This is the latest version**, the manual upgrade is successful.


>? 
> - When the status is **Unable to upgrade**, you cannot upgrade the LogListener in the console, and you need to download the latest-version installer to upgrade. For details, see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).
> - If **Abnormal heartbeat** appears, see [Machine Group Exception](https://intl.cloud.tencent.com/document/product/614/17424) for troubleshooting tips.
> 

### Semi-auto upgrade

1. Run the following command to check the Python version.
```
python -V
```
If the Python version is not 2.7, use [auto](#AutoUpdate) or [manual](#ManualUpdate) upgrade.
2. Run the following command to download the script.
```
wget http://mirrors.tencentyun.com/install/cls/agent-update.py
```
2. Run the following command to execute the script.
```
/usr/bin/python2.7 agent-update.py http://mirrors.tencentyun.com/install/cls/loglistener-linux-x64-x.tar.gz
```
Here, `x` in `loglistener-linux-x64-x.tar.gz` represents the version number of LogListener to upgrade to (such as 2.7.2). The latest version of LogListener is as displayed in [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414). If the entered version does not exist, the download will fail. If the version entered is earlier than the current version installed on the machine, the upgrade will not take effect.

