## Error Description
I entered the correct password, but still could not log in to the CVM using VNC. The message “Module is unknown” appears.
![](https://main.qcloudimg.com/raw/117961622ff73a5859a56bd890011302.png)

## Possible Reasons
This issue may be caused by the `/etc/pam.d/system-auth` configuration in `/etc/pam.d/login` file. 
![](https://main.qcloudimg.com/raw/334e393e16d8a03eec44009be9265ea9.png)
If the path of the `pam_limits.so` module is not configured correctly in the `system-auth` configuration file, the login fails.
![](https://main.qcloudimg.com/raw/36f36e0f2f5d0954f6fcebd39095d3b6.png)
<dx-alert infotype="explain" title="">
The `pam_limits.so` module limits the system resource usage of a user during the session. If the module path is not configured correctly according to the actual operating system, the login authentication fails.

</dx-alert>



## Solutions
1. Perform the [troubleshooting procedure](#ProcessingSteps) to locate the `pam_limits.so` path configuration in the `system-auth` file.
2. Correct the `pam_limits.so` module path. 

[](id:ProcessingSteps)

## Troubleshooting Procedure

1. Try to [log in to Linux CVM via SSH key](https://intl.cloud.tencent.com/document/product/213/32501).
 - If the login succeeded, proceed to the next step.
 - If login failed, use single user mode.For more information, see [Booting into Linux Single User Mode](https://intl.cloud.tencent.com/document/product/213/34819).
2. Run the following command to view logs.
```
vim /var/log/secure
```
This file records the security information, mostly CVM login logs. You can check the error logs of `/lib/security/pam_limits.so` as shown below.
![](https://main.qcloudimg.com/raw/8f9f992d1835a9058020b435f1ef3c99.png)
3. Run the following commands in sequence to enter `/etc/pam.d` directory and search for `/lib/security/pam_limits.so`.
```
cd /etc/pam.d
```
```
find . | xargs grep -ri "/lib/security/pam_limits.so" -l
```
If the result similar to the following figure is returned, /lib/security/pam_limits.so is configured in the `system-auth` file.
![](https://main.qcloudimg.com/raw/eab27cf686eccfeb8a8b796360010bb5.png)
4. Access the `system-auth` file to correct the `pam_limits.so` module path.
For example, you can use the absolute path `/lib64/security/pam_limits.so` or a relative path `pam_limits.so` in a 64-bit operating system.


