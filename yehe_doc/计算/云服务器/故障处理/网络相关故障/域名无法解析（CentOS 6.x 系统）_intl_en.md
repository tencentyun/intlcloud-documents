## Problem Description
After a CVM with CentOS 6.x operating system is restarted or executes on the `service network restart` command, its domain names cannot be resolved. In addition, DNS information in the configuration file `/etc/resolv.conf` is found to be cleared.

## Possible Reasons
In CentOS 6.x operating system, initscripts with versions earlier than 9.03.49-1 has a defect due to different grep versions.

## Solution
Upgrade initscripts to the latest version and generate DNS information again.

## Directions
1. Log in to the CVM.
2. Execute the following command to check the initscripts version, and verify whether a defect exists because the initscripts version is earlier than 9.03.49-1.
```
rpm -q initscripts
```
A message similar to the one below is returned:
```
initscripts-9.03.40-2.e16.centos.x86_64
```
As shown above, the initscripts version of initscripts-9.03.40-2 is earlier than the defective version of initscripts-9.03.49-1. There is a risk of DNS information being cleared.
3. Execute the following command to upgrade initscripts to the latest version and generate DNS information again.
```
yum makecache
yum -y update initscripts
service network restart
```
4. Execute the following command after the upgrade is completed to check the version information of initscripts, and verify whether the upgrade is successful.
```
rpm -q initscripts
```
A message similar to the one below is returned:
```
initscripts-9.03.58-1.el6.centos.2.x86_64
```
As shown above, the version displayed is different from that before the upgrade and is newer than initscripts-9.03.49-1. This indicates that initscripts has been upgraded successfully.
