## Overview

This document describes how to upgrade a file system.

## Directions

1. Log in to the CFS console and go to the [File System](https://console.cloud.tencent.com/cfs/fs?rid=1) page.
2. In the pop-up window, click **Upgrade Now**.

>? If you select **Don't prompt again** and click **Not Now**, when you want to perform an upgrade later, you can view the upgradable file systems as instructed in [Related Operations](#RelatedOperation).
>
3. Select the file system to be upgraded and click **Upgrade File System**.

4. In the pop-up window, view the upgrade advantages and click **Next**.

5. Check the precautions on upgrade and click **Next**.

6. View the client connection status and click **Next**.

7. Select **I have confirmed that the file system has been unmounted from all clients** and click **Confirm Upgrade**.

8. In the pop-up window, click **Confirm Upgrade**.

9. Wait for the upgrade to complete, which will take 2–5 minutes.



<span id="RelatedOperation"></span>
## Related Operations

1. On the file system management page, click the **Filter** column.
2. Select **File System Upgrade**, select **Upgradable**, and click **Confirm** to view the file systems upgradable in the region.


## FAQs

#### 1. How do I determine whether a CFS instance needs to be upgraded?
If an **Upgrade** button is displayed on the right of a file system, the instance needs to be upgraded.

#### 2. What are the advantages of upgrade?
- Higher performance
For legacy Standard instances, the maximum throughput of a file system is 100 MiB/s.
After they are upgraded to the new version, the minimum throughput of a file system will be increased to 100 MiB/s. The bandwidth calculation formula is Min[100 + storage capacity in GiB\*0.1, 300].
- Higher maximum storage capacity
The maximum storage capacity of file systems on the legacy version is 40 TiB, and that on the new version is increased to 160 TiB.

#### 3. How long does the upgrade take?
The upgrade takes 2–5 minutes. Before the upgrade, you need to unmount the file system from all clients. After the upgrade, you need to remount the file system. Therefore, we recommend you spare at least half an hour.

#### 4. Will the upgrade fail?
Generally, the upgrade will not fail. If the task fails on the backend under rare circumstances, an alarm will be triggered, and Tencent Cloud technical support will provide assistance promptly.

#### 5. Can I purchase a new instance on the legacy version?
No. New Standard CFS instances are all on the latest version.

#### 6. Will upgrading an instance affect the data and compatibility?
No.

#### 7. When I access a file after the upgrade, I am prompted that "Unable to access xx. The handle is invalid.". What should I do?
This is because you did not perform unmounting from the client during the upgrade. Restart the client before mounting.


