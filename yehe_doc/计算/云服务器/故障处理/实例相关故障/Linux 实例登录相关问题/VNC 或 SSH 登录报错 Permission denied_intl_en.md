## Error Description
The error message “Permission denied” is reported when I log in using VNC or SSH key.
- The VNC login error is shown below:
![](https://main.qcloudimg.com/raw/5f1aedd75b6d99cddab4d83fa82d964f.png)
- The SSH login error is shown below:
![](https://main.qcloudimg.com/raw/7ab31fbb82391da2c8ae28e8ad3b961f.png)

## Possible Reasons
Using the VNC or SSH login will call `system-auth` for authentication if this module is configured in the `/etc/pam.d/login` configuration file. By default, the `system-auth` module introduces the `pam_limits.so` module. The default `system-auth` configuration is as shown below:
![](https://main.qcloudimg.com/raw/e32db00ec665388bc4c7cb0454fd6fab.png)
The `pam_limits.so` module is mainly used to limit the use of system resources during the user session. Its default configuration file `/etc/security/limits.conf` specifies the maximum number of files, the maximum number of threads, the maximum memory and other resources that a user can use. See the table below for details.
<table>
<tr>
<th style="width:20%">Parameter</th><th>Description</th>
</tr>
<tr>
<td><code>soft nofile</code></td>
<td>The maximum number of open file descriptors (soft limit)</td>
</tr>
<tr>
<td><code> hard nofile</code></td>
<td>The maximum number of open file descriptors (hard limit), which cannot be exceeded.</td>
</tr>
<tr>
<td><code>fs.file-max </code></td>
<td>The maximum number of open file handles (struct file in the kernel) at the system level.</td>
</tr>
<tr>
<td><code>fs.nr_open</code></td>
<td>The maximum number of file descriptors (fd) assigned to a process</td>
</tr>
</table> 

The login failure may be caused by incorrect configurations of the maximum number of open file descriptors for the root account in the `/etc/security/limits.conf` configuration file. The set value of `soft nofile` should be no more than `hard nofile`, and `hard nofile` should be no more than `fs.nr_open`.


## Solutions
Perform the [troubleshooting procedure](#ProcessingSteps) to correct the relationship configurations of `soft nofile`, `hard nofile` and `fs.nr_open`.

[](id:ProcessingSteps)

## Troubleshooting Procedure

1. Try to [log in to Linux CVM via SSH key](https://intl.cloud.tencent.com/document/product/213/32501).
	- If login succeeded, proceed to the next step.
	- If login failed, use single user mode.For more information, see [Booting into Linux Single User Mode](https://intl.cloud.tencent.com/document/product/213/34819).
2. Check whether the set values meet the relationship `soft nofile ≤ hard nofile ≤ fs.nr_open`.
 - Run the following command to obtain the values of `soft nofile` and `hard nofile`.
```
/etc/security/limits.conf
```
In this example, their values are 3000001 and 3000002 respectively, as shown below.
![](https://main.qcloudimg.com/raw/3bc035efb6cf46f70b30017dbefe831a.png)
 - Run the following command to check the `fs.nr_open` value.
```
sysctl -a 2>/dev/null | grep -Ei "file-max|nr_open"
```
In this example, its value is 1048576, as shown below.
![](https://main.qcloudimg.com/raw/0fee5e2cda62d6a558cf808652a6b9dd.png)
3. Edit the `/etc/security/limits.conf` file to add or modify the following configurations at the end of the file. 
 - `root soft nofile`: 100001
 - `root hard nofile`: 100002
4. Edit the `/etc/sysctl.conf` file to add or modify the following configurations at the end of the file.
>?This step is optional when the relationship `soft nofile ≤ hard nofile ≤ fs.nr_open` is met. Perform this step to increase the system limit.
>
 - `fs.file-max` = 2000000
 - `fs.nr_open` = 2000000
5. Run the following command for the configuration to take effect immediately. Then you can log in normally.
```
sysctl -p
```

