## Overview
This document describes how to use the rescue mode in the CVM console. If the server GRUB bootloader files, key system files, or .lib dynamic library files are corrupted or missing when you use the CVM operating system, the operating system may be unable to enter the single user mode and be repaired. In this case, you need to use the CVM rescue mode to repair the system.


## Directions

### Entering rescue mode

<dx-alert infotype="notice" title="">
Before you enter the rescue mode, we strongly recommend you back up the instance to avoid the impact of maloperations. You can [create snapshots](https://intl.cloud.tencent.com/document/product/362/5755) to back up cloud disks and [create custom images](https://intl.cloud.tencent.com/document/product/213/4942) to back up local system disks.
</dx-alert>

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
2. On the instance management page, proceed according to the used view mode:
<dx-tabs>
::: List mode
Select **More** > **OPS and Check** > **Enter Rescue Mode** on the right of the row of the target instance as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/1c550dfc43f5b136401f877a1621a84e.png)
:::
::: Tab mode
Click the tab of the target instance and select **More Actions** > **OPS and Check** > **Enter Rescue Mode** in the top-right corner as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/633e92a792afa8d19e735db38c7e5598.png)
:::
</dx-tabs>
3. [](id:step3)In the **Enter Rescue Mode** pop-up window, set the instance login password for the rescue mode as shown below:
<dx-alert infotype="notice" title="">
- Currently, the rescue mode supports only Linux instances but not Windows instances. If you enter the rescue mode in a Windows instance, you will enter the Linux rescue mode (on CentOS 7.5 64-bit) by default.
- The instance username is `root` by default in the rescue mode.
- You can enter the rescue mode only when the instance is shut down. Forced shutdown may cause data loss or file system corruption. We recommend you shut down the instance as instructed in [Shutting Down Instance](https://intl.cloud.tencent.com/document/product/213/4929) before entering the rescue mode.
</dx-alert>
<img src="https://qcloudimg.tencent-cloud.cn/raw/0c4462f0c86de84a23cac475e0541c84.png"/>
4. Click **Enter Rescue Mode**.
At this point, you can see that the instance is entering the rescue mode. If the instance status is as shown below, the instance has entered the rescue mode successfully. Proceed to the next step to repair the instance as soon as possible.
![](https://qcloudimg.tencent-cloud.cn/raw/46661eec9cabb65ab9ba358015373492.png)



### Using rescue mode to repair system
1. Use the `root` account and the password set in [step 3](#step3) to log in to the instance as follows:
 - If the instance has an EIP, you can log in as instructed in [Logging into Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501).
 - If the instance has no EIPs, you can log in as instructed in [Logging into Linux Instances via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. After successful login, run the following commands in sequence to mount the root system disk partition:
In rescue mode, the device name of the instance system disk is `vda`, and its root partition is `vda1`, which is unmounted by default.
```
mkdir -p /mnt/vm1
```
```
mount /dev/vda1 /mnt/vm1
```
After successful mounting, you can manipulate the data in the root partition. You can also use the `mount -o bind` command to mount some sub-directories in the original file system and use the `chroot` command to run commands in the specified root directory. Below are the specific commands:
```
mount -o bind /dev /mnt/vm1/dev
mount -o bind /dev/pts /mnt/vm1/dev/pts
mount -o bind /proc /mnt/vm1/proc
mount -o bind /run /mnt/vm1/run
mount -o bind /sys /mnt/vm1/sys
chroot /mnt/vm1 /bin/bash
```


### Exiting rescue mode
1. After repairing the instance, exit the rescue mode in the following steps according to the used view mode:
<dx-tabs>
::: List mode
Select **More** > **OPS and Check** > **Exit Rescue Mode** on the right of the row of the target instance as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/42b6657af00132b39a4b3242748a449c.png)
:::
::: Tab mode
Click the tab of the target instance and select **More Actions** > **OPS and Check** > **Exit Rescue Mode** in the top-right corner as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/24df2366e42e1bdc22c171d871073c68.png)
:::
</dx-tabs>
2. After the instance exits the rescue mode, it is still shut down. Start it up as instructed in [Starting Up Instances](https://intl.cloud.tencent.com/document/product/213/38168) to resume instance operations.

