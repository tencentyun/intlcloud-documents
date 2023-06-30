## Error Description
The error “Account locked due to XXX failed logins” appears before I enter the login password.
![](https://main.qcloudimg.com/raw/0dcc0c3b62a36ba0f269e629a3365564.png)

## Possible Reasons
This issue may be caused by the `pam_tally2.so` configuration in `/etc/pam.d/login` file. For VNC login, `/etc/pam.d/login` is called for authentication, while `pam_tally2.so` indicates to automatically lock the user account temporarily or permanently after the specified number of consecutive failed logins. When an account is permanently locked, you need to unlock it manually.

The login account will be locked when the number of consecutive failed logins exceeds the configured value. Note that the account may also be locked for brute force attacks.
![](https://main.qcloudimg.com/raw/806c1d8ccded0746f5457320df479177.png)
See below for the parameters of `pam_tally2` module.
<table>
<tr>
<th>Parameter</th><th>Description</th>
</tr>
<tr>
<td><code>deny=n</code></td>
<td>Lock the account if the number of consecutive failed logins exceeds <code>n</code>.</td>
</tr>
<tr>
<td><code>lock_time=n </code></td>
<td>Lock the account for <code>n</code> seconds when the number of consecutive failed logins exceeds the limit</td>
</tr>
<tr>
<td><code>un lock_time=n</code></td>
<td>Unlock the account automatically <code>n</code> seconds later</td>
</tr>
<tr>
<td><code>no_lock_time </code></td>
<td>Do not use <code>.fail_locktime</code> field in <code>/var/log/faillog</code></td>
</tr>
<tr>
<td><code>magic_root   </code></td>
<td>If the module is invoked by a root user (uid=0), the counter is not incremented.</td>
</tr>
<tr>
<td><code>even_deny_root </code></td>
<td>The root user will be locked after <code>deny=n</code> consecutive failed logins.</td>
</tr>
<tr>
<td><code>root_unlock_time=n  </code></td>
<td>This parameter is required if <code>even_deny_root</code> is configured. It indicates how long the the root user is locked when the number of consecutive failed logins exceeds the limit. </td>
</tr>
</table>

## Solutions
1. Refer to [troubleshooting procedure](#ProcessingSteps) to access the login configuration file and temporarily comment out the configuration of the `pam_limits.so` module.
2. Find the reason why your account is locked, and improve your security policy.

[](id:ProcessingSteps)

## Troubleshooting Procedure

1. Try to [log in to Linux CVM via SSH key](https://intl.cloud.tencent.com/document/product/213/32501).
	- If the login succeeded, proceed to the next step.
	- If the login failed, try the single user mode.
2. Run the following command to view logs.
```
vim /var/log/secure
```
This file records the security information, mostly CVM login logs. You can check the error logs of `pam_tally2` as shown below.
![](https://main.qcloudimg.com/raw/f45fb4564cfea44f0210a6e9b7124b73.png)
3. Run the following commands in sequence to open `/etc/pam.d` directory and search for `pam_tally2`.
```
cd /etc/pam.d
```
```
find . | xargs grep -ri "pam_tally2" -l
```
If the result similar to the following figure is returned, `pam_tally2` is included in `login` file.
![](https://main.qcloudimg.com/raw/a5d272e11a88d4f9cee347244fb98441.png)
4. Run the following command to temporarily comment out the `pam_tally2.so` configurations. Then you can log in normally.
```
sed -i "s/.*pam_tally.*/#&/" /etc/pam.d/login
```
5. Check whether the account is locked due to misoperations or brute force attacks. In the later case, it is recommended to strengthen the security policy as follows:
 - Change the CVM password to a stronger password containing 12-16 characters, including uppercase letters, lowercase letters, special characters, and numbers. For more information, see [Resetting Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).
 - Delete unused CVM login accounts.
 - Change the default sshd port 22 to a less common port between 1024-65525. For more information, see [Modifying the Default Remote Port of CVM](https://intl.cloud.tencent.com/document/product/213/35376).
 - Manage the associated security group rules to open only ports and protocols required by your business. For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
 - Close the port for internet access for core applications such as MySQL and Redis databases. 
 - Install security software (such as CWPP agent), and configure real-time alarms to get notices about suspicious logins instantly.


