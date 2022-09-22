CVMs may be intruded by hackers due to weak passwords and vulnerabilities of open-source components. This document describes how to determine whether a CVM has been infected with a virus and how to fix it.

## Troubleshooting the Issue
 Use [SSH](https://intl.cloud.tencent.com/document/product/213/32501) or [VNC](https://intl.cloud.tencent.com/document/product/213/32494) to log in to the instance and check whether it has been infected with a virus in the following ways:


<dx-accordion>
::: Malicious commands were added to rc.local
Run the following command to view the `rc.local` file.
```
cat /etc/rc.local 
```
If the output information contains a command not added by the business team or public image, such as `wget xx` and `/tmp/xx`, the CVM has probably been infected with a virus.

:::
::: Malicious tasks were added to crontab

Run the following command to list the current schedule.
```
crontab -l
```
If the output information contains a command not added by the business team or public image, such as `wget xx` and `/tmp/xx`, the CVM has probably been infected with a virus.

:::
::: Dynamic library hijacking was added to ld.so.preload
Run the following command to view the `/etc/ld.so.preload` file.
```
cat /etc/ld.so.preload
```
If the output information contains a dynamic library not added by the business team, the CVM has probably been infected with a virus.

:::
::: Huge page memory was configured in sysctl.conf
Run the following command to check the usage of huge page memory.
```
sysctl -a | grep "nr_hugepages "
```
If the output is not 0, and the business program does not use huge page memory, the CVM has probably been infected with a virus.

:::

</dx-accordion>

## Troubleshooting Procedure
1. Back up the system data as instructed in [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
2. Reinstall the instance system as instructed in [Reinstalling System](https://intl.cloud.tencent.com/document/product/213/4933) and take the following security hardening measures:
 - Change the CVM password to a stronger password containing 12-16 characters, including uppercase letters, lowercase letters, special characters, and numbers. For more information, see [Resetting Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).
 - Delete unused CVM login accounts.
 - Change the default sshd port 22 to a less common port between 1024-65525. For more information, see [Modifying the Default Remote Port of CVM](https://intl.cloud.tencent.com/document/product/213/35376).
 - Manage the associated security group rules to open only ports and protocols required by your business. For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
 - Close the port for internet access for core applications such as MySQL and Redis databases.
 - Install security software (such as CWPP agent), and configure real-time alarms to get noticed about suspicious logins instantly.
