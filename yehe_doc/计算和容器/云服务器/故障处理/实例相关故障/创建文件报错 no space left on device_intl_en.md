## Issue Description
When you create a file in the Linux CVM, the error "no space left on device" is reported.


## Common Causes
- The disk space is full
- The file system's `inode` is full
- `df` and `du` are different
 - Files have been deleted, but there are still processes holding corresponding file handles, resulting in the disk space not being released.
 - Mounts are nested. For example, if the `/data` directory of the system disk uses a lot of space, and `/data` is used as a mount point of other data disks, then the `df` and `du` of the system disk will be different.


## Solution
Troubleshoot the problems as instructed in [Steps](#ProcessingSteps).


## Steps[](id:ProcessingSteps)

### Solving the problem of full disk space
1. Log in to the Linux instance [in the standard login method](https://intl.cloud.tencent.com/document/product/213/5436).
2. [](id:Step2)Run the following command to check the disk utilization.
```
df -h
```
3. Locate the mount point with a high disk utilization and run the following command to enter the mount point.
```
cd mount point
```
For example, to enter the system disk mount point, run `cd /`.
4. Run the following command to find directories that occupy a large space.
```
du -x --max-depth=1 | sort -n
```
Perform the following steps for the located directory with the largest occupied space:
   - If the directory capacity is much lower than the total disk space, proceed to the [Solving the problem of `df` and `du` inconsistency](#dfdu) step.
   - If the directory capacity is large, perform [step 2](#Step2) to locate files that occupy a large space and evaluate whether they can be deleted based on the business conditions. If not, expand the disk capacity as instructed in [Expanding Cloud Disks](https://intl.cloud.tencent.com/document/product/213/32377).


### Solving the problem of full file system inode
1. Log in to the Linux instance [in the standard login method](https://intl.cloud.tencent.com/document/product/213/5436).
2. [](id:Step2)Run the following command to check the disk utilization.
```
df -h
```
3. Locate the mount point with a high disk utilization and run the following command to enter the mount point.
```
cd mount point
```
For example, to enter the system disk mount point, run `cd /`.
4. Run the following command to find the directory with the largest number of files. This command is time-consuming, so wait patiently.
```
find / -type f | awk -F / -v OFS=/ '{$NF="";dir[$0]++}END{for(i in dir)print dir[i]" "i}' | sort -k1 -nr | head
```


### Solving the problem of `df` and `du` inconsistency[](id:dfdu)

#### Solving the problem of processes occupying file handles
Run the following command to view the processes occupying files.
```
lsof ｜ grep delete
```
Perform the following steps according to the returned result:
 - Kill the corresponding processes.
 - Restart the service.
 - If many processes occupy file handles, restart the server.


#### Solving the problem of nested mounts
1. Run the `mount` command to mount a highly utilized disk to `/mnt`; for example:
```
mount /dev/vda1 /mnt
```
2. Run the following command to enter `/mnt`.
```
cd /mnt
```
3. Run the following command to find directories that occupy a large space.
```
du -x --max-depth=1 | sort -n
```
According to the returned result, evaluate whether the directories or files can be deleted based on the business conditions.
4. Run the `umount` command to unmount the disk; for example:
```
umount /mnt
```
