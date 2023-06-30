## Problem
When you try to log in to the CVM via VNC, the following message appears even you enter the correct password. Later, you are required to enter the account name again.
![](https://main.qcloudimg.com/raw/13b30f4ccfc97afd0e704e2e5c600047.png)
And when you try to log in remotely using the SSH key, the message **Permission denied, please try again** appears.
![](https://main.qcloudimg.com/raw/db09e73d2a057fb8b297ffd31bf67b62.png)

## Common Cause
The `/var/log/btmp` log file is oversized due to brute force attacks. This file keeps logs of failed logins. If it is too large, logs can not be written into it, which may cause login error.
![](https://main.qcloudimg.com/raw/c19f9e57a67ce6b1ed30cee22af9964c.png)

## Solutions
1. Check whether the `/var/log/btmp` log file is oversized as instructed in [Troubleshooting Procedure](#ProcessingSteps).
2. Confirm whether it is caused by brute force attacks and improve security policy.

## Troubleshooting Procedure[](id:ProcessingSteps)
1. Try to [log in to a Linux CVM instance via SSH key](https://intl.cloud.tencent.com/document/product/213/32501).
	- If the login succeeds, proceed to the next step.
	- If the login fails, try the single user mode. For detailed directions, see [Booting into Linux Single User Mode](https://intl.cloud.tencent.com/document/product/213/34819).
2. Access `/var/log` and check the size of the `/var/log/btmp` log file.
3. Run the following command to clear the oversized `/var/log/btmp` log file. Then you can log in normally.
```
cat /dev/null > /var/log/btmp
```
4. Check whether the account lock is caused by misoperations or brute force attacks. In the later case, it is recommended to strengthen the security policy as follows:
	- Change the CVM password to a stronger password containing 12-16 characters, including uppercase letters, lowercase letters, special characters, and numbers. For more information, see [Resetting Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).
	- Delete unused CVM login accounts.
	- Change the default sshd port 22 to a less common port between 1024-65525. For more information, see [Modifying the Default Remote Port of CVM](https://intl.cloud.tencent.com/document/product/213/35376).
	- Manage the associated security group rules to open only ports and protocols required by your business. For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
	- Close the port for internet access for core applications such as MySQL and Redis databases.
	- Install security software (such as CWPP agent), and configure real-time alarms to get noticed about suspicious logins instantly.
