>?
>- This document is a general instructional guide only for reference.
>- Perform the file operations with caution. You can create a snapshot or use other methods to back up data when necessary.
> 

## Problem
During [login to a Linux instance using SSH key](https://intl.cloud.tencent.com/document/product/213/32501), a message indicating that the connection is unavailable or failed appears.

## Troubleshooting[](id:ProcessingSteps)
Check below for the solutions for common SSH login errors.

<dx-accordion>
::: SSH\slogin\serror\s“User\sroot\snot\sallowed\sbecause\snot\slisted\sin\sAllowUsers”

#### Cause[](id:userNotListAllowUsers)
The login is restricted by the user login control parameters.
- **AllowUsers**: only users listed in this parameter are allowed to log in.
- **DenyUsers**: users listed in this parameter are denied to log in.
- **AllowGroups**: only user groups listed in this parameter are allowed to log in.
- **DenyGroups**: user groups listed in this parameter are denied to log in.

<dx-alert infotype="explain" title="">
The **Deny** policy takes priority over the **Allow** policy.
</dx-alert>


#### Solution
1. Open the SSH config file `sshd_config` as instructed in [Steps](#ProcessingSteps1)
2. Delete the user login control parameters and restart the SSH service.


#### Steps[](id:ProcessingSteps1)
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following commands to open the `sshd_config` configuration file with VIM editor.
```shell
vim /etc/ssh/sshd_config
```
3. Press **i** to enter the edit mode. Locate and delete the following configurations, or add a pound sign (`#`) at the beginning of each line to comment them out.
```shell
AllowUsers root test
DenyUsers test
DenyGroups test
AllowGroups root
```
4. Press **Esc** to exit the edit mode, and enter **:wq** to save the modification.
5. Run the following commands based on the operating system to restart the SSH service.
  - CentOS
```shell
systemctl restart sshd.service
```
  - Ubuntu
```shell
service sshd restart
```

Then you can <a href="https://intl.cloud.tencent.com/document/product/213/32501">log in to the Linux CVM instance via SSH key</a> normally.


::: 
::: SSH\slogin\serror\s“Disconnected:No\ssupported\sauthentication\smethods\savailable”

#### Problem[](id:noSupportesAuthentication)
When logging in via SSH key, the following error message appears:
```
Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
sshd[10826]: Connection closed by xxx.xxx.xxx.xxx.
Disconnected:No supported authentication methods available.
```

#### Cause
SSH service modifies the `PasswordAuthentication` parameter and disables the password login.


#### Solution
1. Open the SSH config file `sshd_config` as instructed in [Steps](#ProcessingSteps2)
2. Modify the `PasswordAuthentication` parameter and restart the SSH service.


#### Steps[](id:ProcessingSteps2)
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following commands to open the `sshd_config` configuration file with VIM editor.
```shell
vim /etc/ssh/sshd_config
```
3. Press **i** to enter the edit mode and change `PasswordAuthentication no` to `PasswordAuthentication yes`.
4. Press **Esc** to exit the edit mode, and enter **:wq** to save the modification.
5. Run the following commands based on the operating system to restart the SSH service.
  - CentOS
```shell
systemctl restart sshd.service
```
  - Ubuntu
```shell
service sshd restart
```
Then you can <a href="https://intl.cloud.tencent.com/document/product/213/32501">log in to the Linux CVM instance via SSH key</a> normally.

:::
::: SSH\slogin\serror\s“ssh_exchange_identification:\sread:\sConnection\sreset\sby\speer”

#### Problem[](id:connectionResetByPeer)
When logging in via SSH key, the error message “ssh_exchange_identification: read: Connection reset by peer” or as shown below appears:
- “ssh_exchange_identification: Connection closed by remote host”
- “kex_exchange_identification: read: Connection reset by peer”
- “kex_exchange_identification: Connection closed by remote host”


#### Cause
The common causes are as follows:
- The connection is blocked by the local access control policy.
- The firewall rules are modified by anti-intrusion software, such as Fail2ban, denyhost, etc.
- Reaches the the maximum number of connections configured in sshd
- Local network problem


#### Solution
Check the access policy, firewall rules, sshd configuration, and network environment as instructed in [Steps](#ProcessingSteps3)



#### Steps[](id:ProcessingSteps3)


#### Checking and modifying the access policy settings
In Linux, the allowed and denied access policy are respectively set in the `/etc/hosts.allow` and `/etc/hosts.deny` files. You can set the trusted hosts in the `hosts.allow` file, and deny all other hosts in the `hosts.deny` file. The Deny policy can be set as follows:
```
in.sshd:ALL# Deny all SSH connections
in.sshd:218.64.87.0/255.255.255.128# Deny SSH connections ranging from 218.64.87.0 to -127.
ALL:ALL# Deny all TCP connections
```


[Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494) and check the `/etc/hosts.deny` and `/etc/hosts.allow` files:
 - Correct the configurations if needed. The modification takes effect immediately.
 - If the configuration is correct, proceed to the next step.

<dx-alert infotype="explain" title="">
If no access policy is configured, both files will be empty by default and all connections are allowed.
</dx-alert>




#### Checking the iptables firewall rules
Check whether the iptables firewall rules are modified, for example, by the anti-intrusion software (such as Fail2ban, denyhost, etc.). Run the following command to check whether the firewall denies SSH connections.
```
sudo iptables -L --line-number
```
 - If yes, please modify the allowlist settings.
 - If no, proceed to the next step.


#### Checking and modifying the sshd configuration
1. Run the following command to open the `sshd_config` configuration file with VIM editor.
```
vim /etc/ssh/sshd_config
```
2. Check the `MaxStartups` value, which specifies the maximum number of connections allowed. If many connections are required to establish in a short period, adjust the value as needed.
 - Follow the steps below to modify the value:
    1. Press **i** to enter the edit mode. After the modification is complete, press **Esc** to exit the edit mode and enter **:wq** to save the modification.
<dx-alert infotype="explain" title="">
This parameter specifies the maximum number of unauthenticated concurrent connections the SSH daemon allows. The default value is `MaxStartups 10:30:100`, which means to allow the first ten unauthenticated connections, refuse connection attempts with a probability of 30%, and reject all new connections when there are 100 connections.
</dx-alert>
    2. Run the following command to restart the sshd service.
```
service sshd restart
```
 - If no modification is required, proceed to the next step.


#### Testing the network environment
1. Check whether a [private IP](https://intl.cloud.tencent.com/document/product/213/5225) is used for login.
  - If yes, use a [public IP](https://intl.cloud.tencent.com/document/product/213/5224) and try again.
  - If not, proceed to the next step.
2. Test the connection by using other network environments.
  - If the connection is normal, restart the instance and log in to it via VNC.
  - If there is a connection error, solve it according to the test result.


If the SSH login error persists, it may be caused by kernel exceptions or other unknown reasons. In this case, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
:::
::: SSH\slogin\serror\s“Permission\sdenied,\splease\stry\sagain”

#### Problem[](id:permissionDenied)
When the root user logs in to a Linux instance via SSH key, the “Permission denied, please try again” error message appears.


#### Cause
This is because that the SELinux service is enabled, or the SSH service modifies the `PermitRootLogin` configuration.


#### Solution
Check the configuration of SELinux service and the `PermitRootLogin` parameter in `sshd_config` as instructed in [Steps](#ProcessingSteps4).

#### Steps[](id:ProcessingSteps4)


#### Checking and disabling the SELinux service
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to check the current SELinux service status.
```
/usr/sbin/sestatus -v 
```
If `enabled` as shown below is returned, the service is enabled. The `disabled` response indicates that the service is disabled.
```
SELinux status:       enabled
```
3. Disable the SELinux service temporarily or permanently as needed.
  - Disable the SELinux service temporarily
Perform the following command to temporarily disable the SELinux service. The change takes effect immediately without needing to restart the system or instance.
```
setenforce 0
```
  - Disable the SELinux service permanently
Run the following command to disable the SELinux service.
```
sed -i 's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
```
<dx-alert infotype="notice" title="">
- This command is only applicable to the SELinux service in the `enforcing` status.
- After running the command, restart the system or instance for the modification to take effect.
</dx-alert>


#### Checking and modifying the sshd configuration
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following commands to open the `sshd_config` configuration file with VIM editor.
```shell
vim /etc/ssh/sshd_config
```
3. Press **i** to enter the edit mode and change `PermitRootLogin no` to `PermitRootLogin yes`.
>?
>- If this parameter is not configured in `sshd_config`, the root user is allowed to log in by default.
>- This parameter only affects the SSH key login of the root user, who can log in to the instance normally using other methods.
>
4. Press **Esc** to exit the edit mode, and enter **:wq** to save the modification.
5. Run the following command to restart the SSH service.
```shell
service sshd restart
```
Then you can <a href="https://intl.cloud.tencent.com/document/product/213/32501">log in to the Linux CVM instance via SSH key</a> normally.
:::
::: SSH\slogin\serror\s“Too\smany\sauthentication\sfailures\sfor\sroot”

#### Problem[](id:tooManyFailures)
The error message “Too many authentication failures for root” is returned and the connection is interrupted after many failed attempts to enter the password to login via SSH key.

#### Cause
I was requested to reset the SSH service password after consecutive failed password entry.


#### Solution
1. Open the SSH config file `sshd_config` as instructed in [Steps](#ProcessingSteps5)
2. Check and modify the `MaxAuthTries` parameter for the password reset policy, and restart the SSH service.


#### Steps[](id:ProcessingSteps5)
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following commands to open the `sshd_config` configuration file with VIM editor.
```shell
vim /etc/ssh/sshd_config
```
3. Check for the configuration similar to what is shown below.
```
MaxAuthTries 5
```
<dx-alert infotype="explain" title="">
- This parameter is not enabled by default. It specifies the number of consecutive incorrect password attempts for each SSH key login, and displays the error message. However, the account will not be locked, which can be used for another SSH key login.
- Determine whether a modification is required. If so, we recommend you to back up the `sshd_config` configuration file.
</dx-alert>
4. Press **i** to enter the edit mode, and modify the following configuration or add a pound sign (`#) at the beginning of the line to comment it out.
```
MaxAuthTries <number of incorrect password attempts allowed>
```
5. Press **Esc** to exit the edit mode, and enter **:wq** to save the modification.
6. Run the following command to restart the SSH service.
```shell
service sshd restart
```
Then you can <a href="https://intl.cloud.tencent.com/document/product/213/32501">log in to the Linux CVM instance via SSH key</a> normally.

:::
::: SSH\sstartup\serror\s“error\swhile\sloading\sshared\slibraries”

#### Problem[](id:errorLibraries)
When the SSH service is started in a Linux instance, an error message similar to the following is displayed in the `secure` log or directly returned:
- “error while loading shared libraries: libcrypto.so.10: cannot open shared object file: No such file or directory”
- “PAM unable to dlopen(/usr/lib64/security/pam_tally.so): /usr/lib64/security/pam_tally.so: cannot open shared object file: No such file or directory”


#### Cause
This is because that the relevant system library files the SSH service depends on are lost or have an exception, such as the permission configuration exception.


#### Solution
Check and fix the system library files as instructed in [Steps](#ProcessingSteps6).



#### Steps[](id:ProcessingSteps6)
<dx-alert infotype="explain" title="">
The following example guides you through resolving a `libcrypto.so.10` library file exception.
</dx-alert>



#### Obtaining the library file
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to view the `libcrypto.so.10` library file information.
```
ll /usr/lib64/libcrypto.so.10
```
The information similar to what is shown below is returned, indicating that `/usr/lib64/libcrypto.so.10` is the soft link of the `libcrypto.so.1.0.2k` library file.
```
lrwxrwxrwx 1 root root 19 Jan 19  2021 /usr/lib64/libcrypto.so.10 -> libcrypto.so.1.0.2k
```
2. Run the following command to view the `libcrypto.so.1.0.2k` library file information.
```
ll /usr/lib64/libcrypto.so.1.0.2k
```
Information similar to the following is returned:
```
-rwxr-xr-x 1 root root 2520768 Dec 17  2020 /usr/lib64/libcrypto.so.1.0.2k
```
3. Note down the path, permission, group and other information of a normal library file, and try the following.
	 - [Find and replace the library file](#findAndReplace)
	 - [Upload an external file](#fileUpload)
	 - [Recover with snapshots](#snapshotRollback)



#### Finding and replacing the library file[](id:findAndReplace)
1. Run the following command to find the `libcrypto.so.1.0.2k` file.
```
find / -name libcrypto.so.1.0.2k
```
2. Run the following command to copy the library file to a normal directory.
```
cp <absolute path of the library file obtained in the step 1> /usr/lib64/libcrypto.so.1.0.2k
```
3. Run the following commands to modify the file permission, owner, and group.
```
chmod 755 /usr/lib64/libcrypto.so.1.0.2k
```
```
chown root:root /usr/lib64/libcrypto.so.1.0.2k
```
4. Run the following commands to create a soft link.
```
ln -s /usr/lib64/libcrypto.so.1.0.2k /usr/lib64/libcrypto.so.10
```
5. Run the following command to start the SSH service.
```
service sshd start
```


#### Uploading an external file[](id:fileUpload)
1. Upload the `libcrypto.so.1.0.2k` library file of a normal CVM to the `\tmp` directory of the target CVM using FTP.
<dx-alert infotype="explain" title="">
`\tmp` is used in this example. You can replace with the actual directory.
</dx-alert>
2. Run the following command to copy the library file to a normal directory.
```
cp /tmp/libcrypto.so.1.0.2k /usr/lib64/libcrypto.so.1.0.2k
```
3. Run the following commands to modify the file permission, owner, and group.
```
chmod 755 /usr/lib64/libcrypto.so.1.0.2k
```
```
chown root:root /usr/lib64/libcrypto.so.1.0.2k
```
4. Run the following commands to create a soft link.
```
ln -s /usr/lib64/libcrypto.so.1.0.2k /usr/lib64/libcrypto.so.10
```
5. Run the following command to start the SSH service.
```
service sshd start
```


#### Recovering with snapshot[](id:snapshotRollback)
You can roll back to snapshot of the system disk to recover the library file. For more information, see [Rolling Back Snapshots](https://intl.cloud.tencent.com/document/product/362/5756).

<dx-alert infotype="notice" title="">
- Note that snapshot rollback will cause loss of data stored after the snapshot creation.
- We recommend you to roll back to snapshots one by one from the latest to the earliest till the SSH service resumes. If the SSH service still cannot run properly after the rollback, the system at that point in time has been abnormal.
</dx-alert>

:::
::: SSH\sservice\sstartup\serror\s“fatal:\sCannot\sbind\sany\saddress”
#### Problem[](id:cannotBindAddress)
When the SSH service is started in a Linux instance, an error message similar to the following is displayed in the `secure` log or directly returned:
```
FAILED.
fatal: Cannot bind any address.
address family must be specified before ListenAddress.
```


#### Cause
Incorrect configuration of `AddressFamily`. This parameter specifies the protocol suite used at runtime. If only IPv6 is configured here, but the IPv6 is not enabled or invalidly configured in the system, this problem may occur.


#### Solution
1. Open the SSH config file `sshd_config` as instructed in [Steps](#ProcessingSteps7)
2. Modify the `AddressFamily` parameter and restart the SSH service.



#### Steps[](id:ProcessingSteps7)
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following commands to open the `sshd_config` configuration file with VIM editor.
```
vim /etc/ssh/sshd_config
```
3. Check for the configuration similar to what is shown below.
```
AddressFamily inet6
​``` Parameter description:
 - **inet**: IPv4 protocol suite, the default value
 - **inet6**: IPv6 protocol suite
 - **any**: both IPv4 and IPv6 protocol suites
4. Press **i** to enter the edit mode, and modify the configuration as follows or add a pound sign (`#`) at the beginning of the line to comment it out. 
```
AddressFamily inet
```
<dx-alert infotype="notice" title="">
The `AddressFamily` parameter takes effect only after being configured before `ListenAddress`.
</dx-alert>
5. Press **Esc** to exit the edit mode, and enter **:wq** to save the modification.
6. Run the following command to restart the SSH service.
```shell
service sshd restart
```
Then you can <a href="https://intl.cloud.tencent.com/document/product/213/32501">log in to the Linux CVM instance via SSH key</a> normally.

:::
::: SSH\sservice\sstartup\serror\s“Bad\sconfiguration\soptions”

#### Problem[](id:badConfigureOptions)
When the SSH service is started in a Linux instance, an error message similar to the following is displayed in the `secure` log or directly returned:
```
/etc/ssh/sshd_config: line 2: Bad configuration options:\\ 
/etc/ssh/sshd_config: terminating, 1 bad configuration options
```


#### Cause
This is caused by the incorrect encoding or configuration of the configuration file.


#### Solution
Fix the `sshd_config` configuration file as instructed below.
- [Modifying the configuration file according to the error message](#changeSetting)
- [Uploading an external file](#upload)
- [Reinstalling the SSH service](#installSSH)
- [Using the snapshot rollback for recovery](#rollBack)


#### Steps


#### Modifying the configuration file according to the error message[](id:changeSetting)
If the error message tells the incorrect configuration, modify `/etc/ssh/sshd_config` with VIM editor by referring to the correct configuration file of another instance.


#### Uploading an external file[](id:upload)
1. Upload the `/etc/ssh/sshd_config` library file of a normal CVM to the `\tmp` directory of the target CVM using FTP.
<dx-alert infotype="explain" title="">
`\tmp` is used in this example. You can replace with the actual directory.
</dx-alert>
2. Run the following command to copy the library file to a normal directory.
```
cp /tmp/sshd_config /etc/ssh/sshd_config
```
3. Run the following commands to modify the file permission, owner, and group.
```
chmod 600 /etc/ssh/sshd_config
``` ```
chown root:root /etc/ssh/sshd_config
```
4. Run the following command to start the SSH service.
```
service sshd start
```


#### Reinstalling the SSH service[](id:installSSH)
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to uninstall the SSH service.
```
rpm -e openssh-server
```
3. Run the following command to install the SSH service.
```
yum install openssh-server
```
4. Run the following command to start the SSH service.
```
service sshd start
```

#### Recovering with snapshot[](id:rollBack)
You can roll back the system disk snapshot of the instance to recover the library file. For more information, see [Rolling Back Snapshots](https://intl.cloud.tencent.com/document/product/362/5756).

<dx-alert infotype="notice" title="">
- Note that snapshot rollback will cause loss of data stored after the snapshot creation.
- We recommend you to roll back to snapshots one by one from the latest to the earliest till the SSH service resumes. If the SSH service still cannot run properly after the rollback, the system at that point in time has been abnormal.
</dx-alert>



:::
</dx-accordion>



If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

