The status check provides a report of instance exceptions. This document mainly describes the symptoms, causes and solutions of kernel and IO problems shown in the status check report.

## Troubleshooting Kernel Failures

### Problems
The kernel failure may cause login failure or abnormal restart.

### Common causes
#### Kernel hung_task
The kernel hung task is based on a single kernel thread named as `khungtaskd`, which monitors processes in the `TASK_UNINTERRUPTIBLE` status. If a process stuck in D state during the period specified by `kernel.hung_task_timeout_secs` (defaults to 120 seconds), the stack information of this hung task process will be printed.

If `kernel.hung_task_panic=1` is configured, the hung task will trigger kernel panic and system restart.



#### Kernel soft lockup
A soft lockup refers to a kernel thread using and not releasing a CPU, without giving other tasks a chance to run. Each CPU is assigned with a timed kernel thread `watchdog/x`. If this thread is not executed during the specified period (the default period is two times the `kernel.watchdog_thresh` value. For example, the default `kernel.watchdog_thresh` value is 10 seconds for a 3.10 kernel), soft lockup occurs.

If `kernel.softlockup_panic=1` is configured, the soft lockup will trigger kernel panic and system restart.


#### Kernel panic
A kernel panic refers to a kernel crash that causes the abnormal restart. The kernel panic will be generally caused by:
- Kernel hung_task, with `kernel.hung_task_panic=1` configured.
- Kernel soft lockup, with `kernel.softlockup_panic=1` configured.
- Kernel bug

### Solution
Due to the difficulty, we recommend you [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category
) for the troubleshooting.


## Troubleshooting Disk Failures

### The inode is full
**Problem**: the error message “No space left on device” is prompted when you create a file. After you run the `df -i` command, you will see inode is 100% used.
**Common causes**: the file system exhausted all inodes.
**Procedure**: delete useless files or expand the disk.

### The disk space is full
**Problem**: the error message “No space left on device” is prompted when you create a file. After you run the `df -h` command, you will see the disk space is 100% used.
**Common causes**: the disk space runs out.
**Procedure**: delete useless files or expand the disk.

### The disk is read-only
**Problem**: the file system can read files only without creating one.
**Common cause**: the file system is damaged.
**Procedure**:
1. Create a snapshot to back up the disk data. For detailed directions, see [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
2. Perform the troubleshooting procedure according to the disk type.
<dx-tabs>
::: System disk
We recommend directly restarting the instance, please see [Restart Instances](https://intl.cloud.tencent.com/document/product/213/4928).
::: 
::: Data disk
1. Run the following command to check the type of the read-only disk file system.
```
lsblk -f
```
2. Run the following command to detach the data disk.
```
umount <mount point of the data disk>
```
3. Run the file system-specific command to fix the file system.
 - Run the following command on the **ext3/ext4** file system:
```
fsck -y /dev/[data disk]
```
 - Run the following command on the **xfs** file system:
```
xfs_repair /dev/[data disk]
```
:::
</dx-tabs>

### The disk %util is high
**Problem**: the instance lags, and responds slowly or stop responding to the SSH or VNC login.
**Common cause**: high IO causes the disk %util to reach 100%.
**Procedure**: check the high IO status, and assess whether to reduce IO reads/writes, or use a disk with higher performance.




