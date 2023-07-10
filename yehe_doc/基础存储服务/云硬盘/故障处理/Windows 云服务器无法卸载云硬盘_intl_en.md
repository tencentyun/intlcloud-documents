## Symptom
After a disk is set to offline status for a Windows CVM instance, [detaching the cloud disk](https://intl.cloud.tencent.com/document/product/362/32400) in the console failed.

## Possible Causes
Processes of the operating system, such as Taskmgr.exe, svchost.exe, and System, are using the disk, causing the detaching to fail.

## Solutions
1. Check whether the disk is in offline status.
2. View the processes that use the disk in the Event Viewer. End them and try to detach the disk again.

## Troubleshooting

<dx-alert infotype="explain" title="">
This document uses a CVM instance with Windows Server 2012 R2 DataCenter 64-bit English installed as an example. Note that the steps may vary by operating system version.
</dx-alert>

### Checking the disk status
1. Log in to the Windows CVM instance as the admin as instructed in [Logging in Using Standard Method (Recommended)](https://intl.cloud.tencent.com/document/product/213/41018).
2. On the desktop, right-click <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-3px 0px"> in the bottom-left corner.
3. In the pop-up menu, select **Disk Management**.
4. In the **Disk Management** window, check whether the cloud disk to be detached is in offline status.

 - If so, proceed to the next step.
 - If not, right-click the status area of the disk and click **Offline** in the pop-up menu.


### Locating and ending processes
1. On the desktop, right-click <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-3px 0px"> in the bottom-left corner.
2. In the pop-up menu, select **Event Viewer**.
3. In the **Event Viewer** window, select **Windows Logs** > **System** on the left.
4. In the system logs, click to view the alarm information and determine that the process using the disk is Taskmgr.exe.

5. End the process and try to [detach the cloud disk in the console](https://intl.cloud.tencent.com/document/product/362/32400#useConsole) again.
If you cannot manually end the process (system processes such as svchost.exe or System), shut down the CVM instance as instructed in [Shutting Down Instances](https://intl.cloud.tencent.com/document/product/213/4929) and then try to [detach the cloud disk in the console](https://intl.cloud.tencent.com/document/product/362/32400#useConsole) again.
