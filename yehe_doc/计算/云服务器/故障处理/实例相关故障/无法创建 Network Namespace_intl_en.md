## Problem Description
When you create a new network namespace, the corresponding command gets stuck and does not continue. Dmesg message: "unregister_netdevice: waiting for lo to become free. Usage count = 1"

## Causes
This problem is caused by a bug in the kernel. The following kernel versions have this bug:
- Ubuntu 16.04 x86_32 kernel version: 4.4.0-92-generic.
- Ubuntu 16.04 x86_32 kernel version: 4.4.0-92-generic.

## Solution

Upgrade the kernel to version 4.4.0-98-generic. In this version, the bug has already been fixed.

## Directions
1. Execute the following command to check the current kernel version.

```
uname -r
```

2. Execute the following command to check whether version 4.4.0-98-generic is available for upgrade.

```
sudo apt-get update
sudo apt-cache search linux-image-4.4.0-98-generic
```

If the following information is displayed, it means this version exists in the source and is available for upgrade. 

```
linux-image-4.4.0-98-generic - Linux kernel image for version 4.4.0 on 64 bit x86 SMP
```

3. Execute the following command to install the new kernel version and corresponding Header package.

```
sudo apt-get install linux-image-4.4.0-98-generic linux-headers-4.4.0-98-generic
```

4. Execute the following command to restart the system.

```
sudo reboot
```

5. Execute the following command to enter the system to check the kernel version.

```
uname -r
```

If the following result is displayed, it means the version upgrade is successful:

```
4.4.0-98-generic
```
