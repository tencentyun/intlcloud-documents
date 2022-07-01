>?
>- This document is a general instructional guide only for reference.
>- Perform the file operations with caution. You can create a snapshot or use other methods to back up data when necessary.
> 

## Error Description
During [login to a Linux instance using SSH key](https://intl.cloud.tencent.com/document/product/213/32501), a message indicating that the connection is unavailable or failed appears.

## Troubleshooting[](id:ProcessingSteps)
Check below for the solutions for common SSH login errors.

<dx-accordion>
::: SSH login error "User root not allowed because not listed in AllowUsers"

#### Problem[](id:userNotListAllowUsers)
Login to a Linux instance via SSH key fails, and a message similar to the following appears in the `secure` log of the client or server:
- Permission denied, please try again.
- User test from 192.X.X.1 not allowed because not listed in AllowUsers.
- User test from 192.X.X.1 not allowed because listed in DenyUsers.
- User root from 192.X.X.1 not allowed because a group is listed in DenyGroups.
- User test from 192.X.X.1 not allowed because none of user's groups are listed in AllowGroups.


#### Cause
The login is restricted by the user login control parameters.
- **AllowUsers**: only users listed in this parameter are allowed to log in.
- **DenyUsers**: users listed in this parameter are denied to log in.
- **AllowGroups**: only user groups listed in this parameter are allowed to log in.
- **DenyGroups**: user groups listed in this parameter are denied to log in.

<dx-alert infotype="explain" title="">
The **Deny** policy takes priority over the **Allow** policy.
</dx-alert>


#### Solutions
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
::: SSH login error "Disconnected:No supported authentication methods available"

#### Problem[](id:noSupportesAuthentication)
When logging in via SSH key, the following error message appears:
```
Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
sshd[10826]: Connection closed by xxx.xxx.xxx.xxx.
Disconnected:No supported authentication methods available.
```

#### Cause
SSH service modifies the `PasswordAuthentication` parameter and disables the password login.


#### Solutions
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
::: SSH login error "ssh_exchange_identification: read: Connection reset by peer"

#### Problem[](id:connectionResetByPeer)
When logging in via SSH key, the error message "ssh_exchange_identification: read: Connection reset by peer" or as shown below appears:
- "ssh_exchange_identification: Connection closed by remote host"
- "kex_exchange_identification: read: Connection reset by peer"
- "kex_exchange_identification: Connection closed by remote host"


#### Cause
The common causes are as follows:
- The connection is blocked by the local access control policy.
- The firewall rules are modified by anti-intrusion software, such as Fail2ban, denyhost, etc.
- Reaches the maximum number of connections configured in sshd
- Local network problem


#### Solutions
Check the access policy, firewall rules, sshd configuration, and network environment as instructed in [Steps](#ProcessingSteps3)



#### Steps[](id:ProcessingSteps3)


#### Checking and modifying the access policy settings
In Linux, the allowed and denied access policy are respectively set in the `/etc/hosts.allow` and `/etc/hosts.deny` files. You can set the trusted hosts in the `hosts.allow` file, and deny all other hosts in the `hosts.deny` file. The Deny policy can be set as follows:
```
in.sshd:ALL			# Deny all SSH connections
in.sshd:218.64.87.0/255.255.255.128	# Deny SSH connections ranging from 218.64.87.0 to -127.
ALL:ALL				# Deny all TCP connections
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


If the SSH login error persists, it may be caused by kernel exceptions or other unknown reasons. In this case, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder).
:::
::: SSH login error "Permission denied, please try again"

#### Problem[](id:permissionDenied)
When the root user logs in to a Linux instance via SSH key, the "Permission denied, please try again" error message appears.


#### Cause
This is because that the SELinux service is enabled, or the SSH service modifies the `PermitRootLogin` configuration.


#### Solutions
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
::: SSH login error "Too many authentication failures for root"

#### Problem[](id:tooManyFailures)
The error message "Too many authentication failures for root" is returned and the connection is interrupted after many failed attempts to enter the password to login via SSH key.

#### Cause
I was requested to reset the SSH service password after consecutive failed password entry.


#### Solutions
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
- Determine whether a modification is required. If so, we recommend you back up the `sshd_config` configuration file.
</dx-alert>
4. Press **i** to enter the edit mode, and modify the following configuration or add a pound sign (`#`) at the beginning of the line to comment it out.
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
::: SSH startup error "error while loading shared libraries"

#### Problem[](id:errorLibraries)
When the SSH service is started in a Linux instance, an error message similar to the following is displayed in the `secure` log or directly returned:
- "error while loading shared libraries: libcrypto.so.10: cannot open shared object file: No such file or directory"
- "PAM unable to dlopen(/usr/lib64/security/pam_tally.so): /usr/lib64/security/pam_tally.so: cannot open shared object file: No such file or directory"


#### Cause
This is because that the relevant system library files the SSH service depends on are lost or have an exception, such as the permission configuration exception.


#### Solutions
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
You can roll back the system disk snapshot of the instance to recover the library file. For more information, please see [Rolling Back Snapshots](https://intl.cloud.tencent.com/document/product/362/5756).

<dx-alert infotype="notice" title="">
- Note that snapshot rollback will cause loss of data stored after the snapshot creation.
- We recommend you roll back to snapshots one by one from the latest to the earliest till the SSH service resumes. If the SSH service still cannot run properly after the rollback, the system at that point in time has been abnormal.
</dx-alert>

:::
::: SSH service startup error "fatal: Cannot bind any address"
#### Problem[](id:cannotBindAddress)
When the SSH service is started in a Linux instance, an error message similar to the following is directly returned or appears in the `secure` log:
```
FAILED.
fatal: Cannot bind any address.
address family must be specified before ListenAddress.
```


#### Cause
Incorrect configuration of `AddressFamily`. This parameter specifies the protocol suite used at runtime. If only IPv6 is configured here, but the IPv6 is not enabled or invalidly configured in the system, this problem may occur.


#### Solutions
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
```The common parameters are described as follows:
 - **inet**: IPv4 protocol suite, the default value
 - **inet6**: IPv6 protocol suite
 - **any**: both IPv4 and IPv6 protocol suites
4. Press **i** to enter the edit mode, and modify the configuration as follows or add a pound sign (`#`) at the beginning of the line to comment it out. 
```
AddressFamily inet
```<dx-alert infotype="notice" title="">
The `AddressFamily` parameter takes effect only after being configured before `ListenAddress`.
</dx-alert>
5. Press **Esc** to exit the edit mode, and enter **:wq** to save the modification.
6. Run the following command to restart the SSH service.
```shell
service sshd restart
```Then you can <a href="https://intl.cloud.tencent.com/document/product/213/32501">log in to the Linux CVM instance via SSH key</a> normally.

:::
::: SSH service startup error "Bad configuration options"

#### Problem[](id:badConfigureOptions)
When the SSH service is started in a Linux instance, an error message similar to the following is directly returned or appears in the `secure` log:
```
/etc/ssh/sshd_config: line 2: Bad configuration options:\\ 
/etc/ssh/sshd_config: terminating, 1 bad configuration options
```


#### Cause
This is caused by the incorrect encoding or configuration of the configuration file.


#### Solutions
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
You can roll back the system disk snapshot of the instance to recover the library file. For more information, please see [Rolling Back Snapshots](https://intl.cloud.tencent.com/document/product/362/5756).

<dx-alert infotype="notice" title="">
- Note that snapshot rollback will cause loss of data stored after the snapshot creation.
- We recommend you roll back to snapshots one by one from the latest to the earliest till the SSH service resumes. If the SSH service still cannot run properly after the rollback, the system at that point in time has been abnormal.
</dx-alert>


:::
::: Enabling UseDNS for SSH led to slow login or data transfer via SSH key
#### Problem[](id:useDNSSlow)
Login or data transfer via SSH key over the private network in a Linux instance is slow, and after switch to the private network, the problem persists.


#### Cause
This may be because that the UseDNS feature of the SSH service is enabled. This feature is a security enhancement, which is not enabled by default. After it is enabled, the server will first perform a reverse DNS PTR record query based on the client IP to get the client's host name, then perform a forward DNS A record query based on the client's host name, and finally compare whether the obtained IP is the same as the original IP so as to prevent client frauds.
In general, the client uses a dynamic IP, and there is no corresponding PTR record; therefore, after this feature is enabled, no comparison can be made, and the relevant query operations increase the delay, eventually leading to slow client connection.


#### Solutions
1. Open the SSH config file `sshd_config` as instructed in [Steps](#ProcessingSteps9)
2. Check and modify the UseDNS configuration and restart the SSH service.


#### Steps[](id:ProcessingSteps9)
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following commands to open the `sshd_config` configuration file with VIM editor.
```
vim /etc/ssh/sshd_config
```
3. Check for the following configuration:
```
UseDNS yes
```
4. Press **i** to enter the edit mode, and delete the configuration or add a pound sign (`#`) at the beginning of the line to comment it out.
5. Run the following command to restart the SSH service.
```shell
service sshd restart
```Then you can <a href="https://intl.cloud.tencent.com/document/product/213/32501">log in to the Linux CVM instance via SSH key</a> normally.

:::
::: SSH login error "No supported key exchange algorithms"

#### Problem[](id:noSupportedkey)
Login to a Linux instance via SSH key fails, and an error message similar to the following may appear in the `secure` log of the client or server:
- Read from socket failed: Connection reset by peer.
- Connection closed by 192.X.X.1.
- sshd error: could not load host key.
- fatal: No supported key exchange algorithms [preauth].
- DSA host key for 192.X.X.1 has changed and you have requested strict checking.
- Host key verification failed.
- ssh_exchange_identification: read: Connection reset by peer.



#### Cause
Usually, this is because that the relevant key file of the SSH service is exceptional, so the sshd daemon cannot load the correct SSH host key. Common causes include the following:
- The relevant key file is exceptional; for example, the file is corrupted, deleted, or tampered with.
- The permission configuration of the relevant key file is exceptional, so it cannot be read correctly.



#### Solutions
Check and modify the configuration as instructed below.
- [Checking and modifying file permission](#filePermissions)
- [Checking and modifying file validity](#effectiveness)



#### Steps


#### Checking and modifying file permission[](id:filePermissions)
The SSH service will check the permission of the relevant key file. For example, the default permission of a private key file is `600`, and if other permissions such as `777` are configured, then other users also have permissions to read or modify the file. In this case, the SSH service will deem that the configuration involves security risks, which causes client connection failures. The troubleshooting process is as follows:

1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following commands to restore the default permission of the relevant file.
```
cd /etc/ssh/
``` ```
chmod 600 ssh_host_*
``` ```
chmod 644 *.pub
```
3. Run the `ll` command to view the file permission. If the following result is returned, the file permission is normal.
```
total 156
-rw-------. 1 root root 125811 Nov 23 2013 moduli
-rw-r--r--. 1 root root 2047 Nov 23 2013 ssh_config
-rw------- 1 root root 3639 May 16 11:43 sshd_config
-rw------- 1 root root 668 May 20 23:31 ssh_host_dsa_key
-rw-r--r-- 1 root root 590 May 20 23:31 ssh_host_dsa_key.pub
-rw------- 1 root root 963 May 20 23:31 ssh_host_key
-rw-r--r-- 1 root root 627 May 20 23:31 ssh_host_key.pub
-rw------- 1 root root 1675 May 20 23:31 ssh_host_rsa_key
-rw-r--r-- 1 root root 382 May 20 23:31 ssh_host_rsa_key.pub
```

 
#### Checking and modifying file validity[](id:effectiveness)
1. The SSH service will automatically rebuild a lost key file upon start. Run the following commands to check for the `ssh_host_*` file.
```
cd /etc/ssh/
``` ```
ll
```If the following result is returned, the `ssh_host_*` file exists.
```
total 156
-rw-------. 1 root root 125811 Nov 23  2013 moduli
-rw-r--r--. 1 root root   2047 Nov 23  2013 ssh_config
-rw-------  1 root root   3639 May 16 11:43 sshd_config
-rw-------  1 root root    672 May 20 23:08 ssh_host_dsa_key
-rw-r--r--  1 root root    590 May 20 23:08 ssh_host_dsa_key.pub
-rw-------  1 root root    963 May 20 23:08 ssh_host_key
-rw-r--r--  1 root root    627 May 20 23:08 ssh_host_key.pub
-rw-------  1 root root   1675 May 20 23:08 ssh_host_rsa_key
-rw-r--r--  1 root root    382 May 20 23:08 ssh_host_rsa_key.pub
```
2. Run the following command to delete the relevant file.
```
rm -rf ssh_host_*
```On Ubuntu or Debian, run the following command to delete the relevant file.
```
sudo rm -r /etc/ssh/ssh*key
```
3. Run the `ll` command to check whether the file has been deleted successfully. If the following result is returned, it has been deleted successfully.
```
total 132
-rw-------. 1 root root 125811 Nov 23  2013 moduli
-rw-r--r--. 1 root root   2047 Nov 23  2013 ssh_config
-rw-------  1 root root   3639 May 16 11:43 sshd_config
```
4. Run the following command to restart the SSH service, and the relevant file will be generated automatically.
```
service sshd restart
```On Ubuntu or Debian, run the following command to restart the SSH service.
```
sudo dpkg-reconfigure openssh-server
```
5. Run the `ll` command to check whether the `ssh_host_*` file has been generated successfully. If the following result is returned, it has been generated successfully.
```
total 156
-rw-------. 1 root root 125811 Nov 23  2013 moduli
-rw-r--r--. 1 root root   2047 Nov 23  2013 ssh_config
-rw-------  1 root root   3639 May 16 11:43 sshd_config
-rw-------  1 root root    668 May 20 23:16 ssh_host_dsa_key
-rw-r--r--  1 root root    590 May 20 23:16 ssh_host_dsa_key.pub
-rw-------  1 root root    963 May 20 23:16 ssh_host_key
-rw-r--r--  1 root root    627 May 20 23:16 ssh_host_key.pub
-rw-------  1 root root   1671 May 20 23:16 ssh_host_rsa_key
-rw-r--r--  1 root root    382 May 20 23:16 ssh_host_rsa_key.pub
```Log in to the instance via SSH key. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/32501">Logging into Linux Instance via SSH Key</a>.


:::
::: SSH service startup error "must be owned by root and not group or word-writable"
#### Problem[](id:mustBeOwnerByRoot)
When the SSH service is started on a Linux instance, the "must be owned by root and not group or word-writable" error message is returned.


#### Cause
Usually, this is because that the relevant permission or grouping of the SSH service is exceptional. For security reasons, the service has certain requirements for the permission configuration and grouping of directories or files.


#### Solutions
Check and modify the incorrect configuration as instructed below.
 - [Checking and repairing the configuration of `/var/empty/sshd` directory](#repairSshd)
 - [Checking and repairing the configuration of `/etc/securetty` file](#repairSecuretty)


#### Steps

<dx-alert infotype="explain" title="">
This document uses CentOS 7.6 as an example. Please proceed based on the actual business conditions.
</dx-alert>


#### Checking and repairing the configuration of `/var/empty/sshd` directory[](id:repairSshd)
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to view the permission configuration of the `/var/empty/sshd` directory. 
```
ll -d /var/empty/sshd/
```The following is the default permission configuration.
```
drwx--x--x. 2 root root 4096 Aug  9  2019 /var/empty/sshd/
```
3. Compare the returned result with the default permission configuration, and if they are different, run the following command to restore the default configuration.
<dx-alert infotype="explain" title="">
The `/var/empty/sshd` directory has the permission `711` and is a root user in the root group by default.
</dx-alert> ```
chown -R root:root /var/empty/sshd
``` ```
chmod -R 711 /var/empty/sshd
```
4. Run the following command to restart the SSH service.
```
systemctl restart sshd.service
```


#### Checking and repairing the configuration of `/etc/securetty` file[](id:repairSecuretty)
1. Run the following command to view the permission configuration of the `/etc/securetty` file.
```
ll /etc/securetty
```The following is the default permission configuration.
```
-rw-------. 1 root root 255 Aug  5  2020 /etc/securetty
```
2. Compare the returned result with the default permission configuration, and if they are different, run the following command to restore the default configuration.
<dx-alert infotype="explain" title="">
The `/etc/securetty` file has the permission `600` and is a root user in the root group by default.
</dx-alert> ```
chown root:root /etc/securetty
``` ```
chmod 600 /etc/securetty
```
3. Run the following command to restart the SSH service.
```
systemctl restart sshd.service
```Log in to the instance via SSH key. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/32501">Logging into Linux Instance via SSH Key</a>.


:::
::: SSH login error "Host key verification failed"
#### Problem[](id:hostKeyVerification)
Login to a Linux instance via SSH key fails, and the following error message appears:
```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@ WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that the RSA host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
ae:6e:68:4c:97:a6:91:81:11:38:8d:64:ff:92:13:50.
Please contact your system administrator.
Add correct host key in /root/.ssh/known_hosts to get rid of this message.
Offending key in /root/.ssh/known_hosts:70
RSA host key for x.x.x.x has changed and you have requested strict checking.
Host key verification failed.
```
If the client runs on Windows, the following error message will usually appear during an SSH client connection:
```
The host key of `X.X.X.X` (port: XX) is not the same as the one saved in the host key database. The host key has been changed or someone is attempting to eavesdrop this connection. If you are not sure, we recommend you cancel this connection.
```


#### Cause
After the Linux instance is reinstalled, changes in the account information lead to the change in the SSH public key, so the public key fingerprint saved on the client is not the same as that saved on the server, resulting in SSH authentication failure and denied login.


#### Solutions
Fix the problem as instructed below based on the operating system of the client.
- [Windows client](#windows)
- [Linux client](#linux)



#### Steps


#### Windows client[](id:windows)

<dx-alert infotype="explain" title="">
This document uses PuTTY as an SSH client example. Please proceed based on the actual conditions.
</dx-alert>

1. Start PuTTY.
2. On the login page, select a session and click **Delete** to delete it as shown below:
![](https://main.qcloudimg.com/raw/fba29dcb992ff9458484aeb09b3d3a97.png)
3. Log in to the instance with the username and password again as instructed in [Logging in to Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502). After confirming that the new public key fingerprint is saved, you can log in successfully. 


#### Linux client[](id:linux)

<dx-alert infotype="explain" title="">
This document uses CentOS 6.5 as an operating system example of the Linux instance. As the steps may vary by operating system, please proceed based on the actual conditions.
</dx-alert>


1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to open the `known_hosts` file of the corresponding account.
```
vi ~/.ssh/known_hosts
```
3. Press **i** to enter the edit mode and delete the entry of the Linux instance IP similar to the following:
```
1.14.xxx.xx
skowcenw96a/pxka32sa....
dsaprgpck2wa22mvi332ueddw...
```
4. Press **Esc** and enter **:wq** to save and close the file.
5. Reconnect to the Linux instance as instructed in [Logging into Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501). After confirming that the new public key fingerprint is saved, you can log in successfully.

:::
::: SSH login error "pam_listfile(sshd:auth): Refused user root for service sshd"

#### Problem[](id:canNotLogIn)
Login to a Linux instance via SSH key fails with the correct password entered. When this problem occurs, login in the console and via SSH key may both fail, or only one of them can succeed. An error message similar to the following appears in the `secure` log:
- sshd[1199]: pam_listfile(sshd:auth): Refused user root for service sshd
- sshd[1199]: Failed password for root from 192.X.X.1 port 22 ssh2
- sshd[1204]: Connection closed by 192.X.X.2



#### Cause
The relevant access control policy of the PAM module (pam_listfile.so) causes the user login to fail.


#### Overview of PAM module
Pluggable Authentication Module (PAM) is an authentication mechanism proposed by Sun. It provides some dynamic link libraries and a set of unified APIs to separate a system service from its authentication method. This allows the system admin to flexibly configure different authentication methods for different services as needed without modifying service programs and add new authentication methods to the system easily.
Each application with the PAM module enabled has a configuration file named after it in the `/etc/pam.d` directory; for example, the configuration file of the `login` command is `/etc/pam.d/login`, where you can configure specific policies. 


#### Solutions
Check and repair the PAM module as instructed in [Steps](#ProcessingSteps13).


#### Steps[](id:ProcessingSteps13)

<dx-alert infotype="explain" title="">
The steps in this document are for CentOS 6.5 as an example. As the steps may vary by operating system, please proceed based on the actual conditions.
</dx-alert>

1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Use the `cat` command to view the corresponding PAM configuration file as described below:
<table>
<tr>
<th>File</th>
<th>Feature Description</th>
</tr>
<tr>
<td><code>/etc/pam.d/login</code></td>
<td>Configuration file of the console (VNC)</td>
</tr>
<tr>
<td><code>/etc/pam.d/sshd</code></td>
<td>Configuration file of SSH login</td>
</tr>
<tr>
<td><code>/etc/pam.d/system-auth</code></td>
<td>Global configuration file of the system</td>
</tr>
</table>
3. Check for the configuration similar to what is shown below.
```
auth required pam_listfile.so item=user sense=allow file=/etc/ssh/whitelist onerr=fail
```Description:
	 - **item**: set the object type for access control. Valid values: tty, user, rhost, ruser, group, shell.
	 - **sense**: find the control method that meets the conditions in the configuration file. Valid values: allow (allowlist), deny (blocklist).
	 - **file**: specify the full path name of the configuration file.
	 - **onerr**: define the default value to be returned when an error occurs; for example, the configuration file cannot be opened.
4. Use Vim to delete the policy configuration or add a pound sign (`#`) at the beginning of the line to comment it out.
<dx-alert infotype="explain" title="">
The relevant policy configuration can improve the server security. We recommend you back up the configuration before modifying it as needed.
</dx-alert> ```
# auth required pam_listfile.so item=user sense=allow file=/etc/ssh/whitelist onerr=fail
```
5. Log in to the instance via SSH key. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/32501">Logging into Linux Instance via SSH Key</a>.


:::
::: SSH login error "requirement "uid >= 1000" not met by user "root""

#### Problem[](id:requirementUidNotMet)
Login to a Linux instance via SSH key fails with the correct username and password entered. When this problem occurs, login in the console and via SSH key may both fail, or only one of them can succeed. An error message similar to the following appears in the `secure` log:
```
pam_succeed_if(sshd:auth): requirement "uid >= 1000" not met by user "root".
```


#### Cause
The policy configuration of the PAM module bans users with a UID of below `1000` from logging in.



#### Solutions
Check and repair the PAM module as instructed in [Steps](#ProcessingSteps14).



#### Steps[](id:ProcessingSteps14)
<dx-alert infotype="explain" title="">
The steps in this document are for CentOS 6.5 as an example. As the steps may vary by operating system, please proceed based on the actual conditions.
</dx-alert>

1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Use the `cat` command to view the corresponding PAM configuration file as described below:
<table>
<tr>
<th>File</th>
<th>Feature Description</th>
</tr>
<tr>
<td><code>/etc/pam.d/login</code></td>
<td>Configuration file of the console (VNC)</td>
</tr>
<tr>
<td><code>/etc/pam.d/sshd</code></td>
<td>Configuration file of SSH login</td>
</tr>
<tr>
<td><code>/etc/pam.d/system-auth</code></td>
<td>Global configuration file of the system</td>
</tr>
</table> 
3. Check for the configuration similar to what is shown below.
```
auth required pam_succeed_if.so uid >= 1000
```
4. Use Vim to modify or delete the policy configuration or add a pound sign (`#`) at the beginning of the line to comment it out. We recommend you back up the configuration before modifying it as needed.
```
auth        required      pam_succeed_if.so uid <= 1000    # Modify the policy
# auth        required      pam_succeed_if.so uid >= 1000  # Comment out the relevant configuration
```
5. Log in to the instance via SSH key. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/32501">Logging into Linux Instance via SSH Key</a>.

:::
::: SSH login error "Maximum amount of failed attempts was reached" 
#### Problem[](id:maximumAmountFailed)
During login to a Linux instance via SSH key, the "Maximum amount of failed attempts was reached" error message appears.



#### Cause
Entering incorrect passwords several consecutive times triggered the policy restriction of the PAM module, causing the user account to be locked.

<dx-alert infotype="explain" title="">
For more information on PAM, please see [pam_tally2 - login counter (tallying) module](http://www.linux-pam.org/Linux-PAM-html/sag-pam_tally2.html?spm=a2c4g.11186623.0.0.44262fc7r2i3PU).
</dx-alert>





#### Solutions
Please proceed based on the actual conditions as instructed below:

- [Root user not locked](#notLocked)
- [Root user locked](#locked)


#### Steps
<dx-alert infotype="explain" title="">
The steps in this document are for CentOS 7.6 and 6.5 as an example. As the steps may vary by operating system, please proceed based on the actual conditions.
</dx-alert>



#### Root user not locked[](id:notLocked)
1. Log in to the instance as the root user. For more information, please see [Logging into Linux Instances via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to view the global PAM configuration file of the system.
```
cat /etc/pam.d/system-auth
```
3. Run the following command to view the PAM configuration file of the local terminal.
```
cat /etc/pam.d/login
```
4. Run the following command to view the PAM configuration file of the SSH service. 
```
cat /etc/pam.d/sshd
```
5. Use Vim to modify or delete the configuration in the above configuration files or add a pound sign (`#`) at the beginning of the line to comment it out. This document uses commenting the configuration out as an example. After the modification, the relevant configuration is as shown below:
```
#auth required pam_tally2.so deny=3 unlock_time=5
#auth required pam_tally.so onerr=fail no_magic_root
#auth requeired pam_tally2.so deny=5 lock_time=30 unlock_time=10 even_deny_root root_unlock_time=10
```Description:
 - The `pam_tally2` module is used here; if it is not supported, use the `pam_tally` module. The settings may vary by PAM version. For more information on how to use a specific module, please see the corresponding rules.
 - Both the `pam_tally2` and `pam_tally` modules can be used for account lockout policy control. They differ in that the former has the automatic unlock time feature.
 - `even_deny_root` indicates to restrict the root user.
 - `deny` indicates to set the maximum number of consecutive incorrect login attempts for general users and root users. After it is exceeded, the user will be locked.
 - `unlock_time` indicates to unlock general users after they are locked for a specified period of time in seconds.
 - `root_unlock_time` indicates to unlock root users after they are locked for a specified period of time in seconds.
6. Log in to the instance via SSH key. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/32501">Logging into Linux Instance via SSH Key</a>.



#### Root user locked[](id:locked)
1. Enter the single user mode and log in to the instance. For detailed directions, please see [Booting into Linux Single User Mode](https://intl.cloud.tencent.com/document/product/213/34819).
2. Run the following commands to manually unlock the root user. 
```
pam_tally2 -u root # View the number of consecutive incorrect password attempts made by the root user
``` ```
pam_tally2 -u root -r # Clear the number of consecutive incorrect password attempts made by the root user
``` ```
authconfig --disableldap --update # Update the PAM authentication record
```
3. Restart the instance.
4. Comment out, modify, or update the corresponding PAM configuration file as instructed in [Root user not locked](#notLocked).
5. Log in to the instance via SSH key. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/32501">Logging into Linux Instance via SSH Key</a>.

:::
::: SSH login error "login: Module is unknown"

#### Problem[](id:moduleIsUnknown)
Login to a Linux instance via SSH key fails, and a message similar to the following is displayed in the `secure` log:
```
login: Module is unknown.
login: PAM unable to dlopen(/lib/security/pam_limits.so): /lib/security/pam_limits.so: cannot open shared object file: No such file or directory.
```


#### Cause
Each application with the PAM module enabled has a configuration file named after it in the `/etc/pam.d` directory; for example, the configuration file of the `login` command is `/etc/pam.d/login`, where you can configure specific policies as shown below:
<table>
<tr>
<th>File</th>
<th>Feature Description</th>
</tr>
<tr>
<td><code>/etc/pam.d/login</code></td>
<td>Configuration file of the console (VNC)</td>
</tr>
<tr>
<td><code>/etc/pam.d/sshd</code></td>
<td>Configuration file of SSH login</td>
</tr>
<tr>
<td><code>/etc/pam.d/system-auth</code></td>
<td>Global configuration file of the system</td>
</tr>
</table>
During remote login, certain applications with PAM enabled may fail to load the module, causing the login method with the corresponding policy configured to fail.



#### Solutions
Check and repair the configuration file as instructed in [Steps](#ProcessingSteps15).



#### Steps[](id:ProcessingSteps15)

<dx-alert infotype="explain" title="">
This document discusses the `/etc/pam.d/sshd` and `/etc/pam.d/system-auth` files. If `/etc/pam.d/login` is exceptional, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder) for assistance.
</dx-alert>


1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to view the PAM configuration file.
```
cat [absolute path of the corresponding PAM configuration file] 
```Check for the configuration similar to what is shown below. The file path is `/lib/security/pam_limits.so`.
```
session    required     pam_limits.so
```
3. Run the following command to check whether the `/lib/security/pam_limits.so` path is incorrect.
```
ll /lib/security/pam_limits.so
```
  - If yes, use Vim to edit the PAM configuration file and repair the path of the `pam_limits.so` module. The correct path should be `/lib64/security` on a 64-bit Linux instance. The modified configuration information should be as shown below:
```
session     required     /lib64/security/pam_limits.so
```
  - If no, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder) for assistance.
4. Log in to the instance via SSH key. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/32501">Logging into Linux Instance via SSH Key</a>.

:::
::: SSH service exception error due to virus "fatal: mm_request_send: write: Broken pipe"

#### Problem[](id:writeBrokenPipe)
The "fatal: mm_request_send: write: Broken pipe" error message is displayed due to an SSH service exception caused by a virus.



#### Cause
This may be because that viruses such as udev-fall affect the normal execution of the SSH service.


#### Solutions
Fix the virus issue based on actual conditions as instructed below.
- [Temporary solution](#temporary)
- [Reliable solution](#reliable)



#### Steps


#### Temporary solution[](id:temporary)
This document uses the udev-fall virus as an example. You can temporarily make the SSH service work normally as instructed below.
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to view the process information of the udev-fall virus and record the process ID.
```
ps aux | grep udev-fall
```
3. Run the following command to end the process. 
```
kill -9 [virus process ID]
```
4. Run the following command to ban udev-fall from automatically starting.
```
chkconfig udev-fall off
```
5. Run the following command to delete all the instructions and startup configuration related to udev-fall. 
```
for i in ` find / -name "udev-fall"`;
do echo '' > $i && rm -rf $i;
done
```
6. Run the following command to restart the SSH service.
```
systemctl restart sshd.service
```



#### Reliable solution[](id:reliable)

As it is unclear whether the virus or intruder has made other changes to the system or hides other virus files, to ensure the long-term stable operations of the server, we recommend you restore the server to its normal state by rolling back the system disk snapshot of the instance. For more information, please see [Rolling Back Snapshots](https://intl.cloud.tencent.com/document/product/362/5756).
<dx-alert infotype="notice" title="">
- Note that snapshot rollback will cause loss of data stored after the snapshot creation.
- We recommend you roll back to snapshots one by one from the latest to the earliest till the SSH service resumes. If the SSH service still cannot run properly after the rollback, the system at that point in time has been abnormal.
</dx-alert>


:::
::: SSH service start error "main process exited, code=exited"

#### Problem[](id:mainProcessExited)

When the SSH service is started by the `service` or `systemctl` command on a Linux instance, the command line does not return any error message, but the service cannot run properly, and an error message similar to the following is displayed in the `secure` log:
```
sshd.service: main process exited, code=exited, status=203/EXEC.
init: ssh main process (1843) terminated with status 255.
```



#### Cause
Usually, this is because that configuration of the `PATH` environment variable is exceptional or the relevant files of the SSH software package are removed.



#### Solutions
Check and repair the `PATH` environment variable or reinstall the SSH software package as instructed in [Steps](#ProcessingSteps18).



#### Steps[](id:ProcessingSteps18)

<dx-alert infotype="explain" title="">
The steps in this document are for CentOS 6.5 as an example. As the steps may vary by operating system, please proceed based on the actual conditions.
</dx-alert>

1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to check the environment variable configuration.
```
echo $PATH
```
3. Compare the returned value of the `PATH` environment variable with its default value as shown below:
```
/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin
```If the returned value of the `PATH` environment variable is not the same as the default value, you need to run the following command to reset it.
```
export PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin
```
4. Run the following command to find and confirm the path of the sshd program.
```
find / -name sshd
```
  - If the following result is returned, the sshd program files already exist.
```
/usr/sbin/sshd
``` 
  - If the corresponding files do not exist, please reinstall the SSH software package.
5. Run the following command to restart the SSH service.
```
service sshd restart
```Log in to the instance via SSH key. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/32501">Logging into Linux Instance via SSH Key</a>.


:::
::: SSH login error "pam_limits(sshd:session): could not sent limit for 'nofile'"

#### Problem[](id:pamLimits)
During login to a Linux instance via SSH key, the following error message is returned:
```
-bash: fork: retry: Resource temporarily unavailable.
pam_limits(sshd:session): could not sent limit for 'nofile':operaton not permitted.
Permission denied.
```



#### Cause
Usually, this is because that the number of currently opened shell processes or files exceeds the ulimit system environment limit of the server.



#### Solutions
Modify the `limits.conf` file to permanently change the ulimit system environment limit based on the operating system version as instructed in [Steps](#ProcessingSteps19).



#### Steps[](id:ProcessingSteps19)

<dx-alert infotype="explain" title="">
- Since CentOS 6, the `X-nproc.conf` file is used to manage the ulimit system environment limits. The steps for versions below and above CentOS 6 are differentiated here. The prefix number of the `X-nproc.conf` file varies by system version; for example, it is `90-nproc.conf` on CentOS 6 and `20-nproc.conf` on CentOS 7. Please proceed based on the actual environment.
- This document uses CentOS 7.6 and CentOS 5 as an example. Please proceed based on the actual business conditions.
</dx-alert>


#### Below CentOS 6[](id:beforeCentOS6)
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to view the current ulimit system resource limits.
```
cat /etc/security/limits.conf
```Description:
  - **&lt;domain&gt;**: target system user. You can use \* to indicate all users.
  - **&lt;type&gt;**: `soft`, `hard`, and `-`. 
      - `soft` is the &lt;value&gt; of the current system that has taken effect.
      - `hard` is the maximum &lt;value&gt; set in the system.
      - The limit of `soft` cannot be greater than that of `hard`. `-` indicates to set the values of `soft` and `hard` at the same time.
  - **&lt;item&gt;**: target resource type. 
      - `core` limits the kernel file size.
      - `rss` is the maximum resident set size.
      - `nofile` is the maximum number of opened files.
      - `noproc` is the maximum number of processes.
3. No system resource limits are set by default. Please judge based on the actual conditions. If system resource limits are enabled and configured, you need to edit the `limits.conf` file to comment out, modify, or delete the resource type code limited by the `noproc` or `nofile` parameter.
We recommend you run the following command to back up the `limits.conf` file before modifying it.
```
cp -af /etc/security/limits.conf /root/limits.conf_bak
```
4. After completing the modification, restart the instance.



#### CentOS 6 and above
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to view the current ulimit system resource limits.
```
cat /etc/security/limits.d/20-nproc.conf
```If the returned result is as shown below, system resource limits have been enabled and the maximum number of connection processes allowed for all users except root users is 4,096.
![](https://main.qcloudimg.com/raw/c4d7105cc05a172ee1f9f501690788bf.png)
3. Modify the `/etc/security/limits.d/20-nproc.conf` file as instructed in [Below CentOS 6](#beforeCentOS6). We recommend you back up the file before doing so.
4. After completing the modification, restart the instance.

:::
::: SSH login error "pam_unix(sshdsession) session closed for user"

#### Problem[](id:sessionClosedForUser)
Login to a Linux instance via SSH key fails with the correct username and password entered. An error message similar to the following is directly returned or appears in the `secure` log:
- This account is currently not available.
- Connection to 127.0.0.1 closed.
- Received disconnect from 127.0.0.1: 11: disconnected by user.
- pam_unix(sshd:session): session closed for user test.



#### Cause
Usually, this is because that the default shell of the corresponding user is modified.


#### Solutions
Check and repair the default shell configuration of the corresponding user as instructed in [Steps](#ProcessingSteps20).


#### Steps[](id:ProcessingSteps20)
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to view the default shell of the test user.
```
cat /etc/passwd | grep test
```If a message similar to the following is returned by the system, the shell of the test user has been changed to `nologin`. 
```
test:x:1000:1000::/home/test:/sbin/nologin
```
3. Run the following command and use Vim to edit the `/etc/passwd` file. We recommend you back up the file before doing so.
```
vim /etc/passwd
```
4. Press **i** to enter the edit mode and change `/sbin/nologin` to `/bin/bash`. 
5. Press **Esc** and enter **:wq** to save and close the file.
6. Log in to the instance via SSH key. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/32501">Logging into Linux Instance via SSH Key</a>.

::: 
</dx-accordion>


<br>
If the problem persists, please <a href="https://console.intl.cloud.tencent.com/workorder">submit a ticket</a> for assistance.






