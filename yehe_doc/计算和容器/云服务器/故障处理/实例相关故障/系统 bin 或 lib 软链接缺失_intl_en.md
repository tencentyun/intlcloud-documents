## Issue Description
During command execution or system startup, an error message that the command or lib was not found is reported.


## Common Causes
The bin, sbin, lib, and lib64 of CentOS 7, CentOS 8, and Ubuntu 20 are soft links as follows:
```
lrwxrwxrwx   1 root root     7 Jun 19  2018 bin -> usr/bin
lrwxrwxrwx   1 root root     7 Jun 19  2018 lib -> usr/lib
lrwxrwxrwx   1 root root     9 Jun 19  2018 lib64 -> usr/lib64
lrwxrwxrwx   1 root root     8 Jun 19  2018 sbin -> usr/sbin
```
If a soft link is deleted, an error will be reported during command execution or system startup.


## Solution
Check and create the required soft links as instructed in [Steps](#ProcessingSteps).


## Steps[](id:ProcessingSteps)
1. Enter the rescue mode.
2. Run commands such as `mount` and `chroot`. When running the `chroot` command:
 - If there is an error, run `cd /mnt/vm1`.
 - Otherwise, run `cd /`.
3. Run the following command to check whether the corresponding soft link exists.
```
ls -al / | grep -E "lib|bin"
```
 - If yes, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
 - If no, run the following commands as needed to create corresponding soft links.
```
ln -s usr/lib64 lib64
ln -s usr/sbin sbin
ln -s usr/bin bin
ln -s usr/lib lib
```
4. Run the following command to check the soft links.
```
chroot /mnt/vm1 /bin/bash
```
If no error is reported, the soft links have been successfully repaired.
5. Exit rescue mode and start the system.
