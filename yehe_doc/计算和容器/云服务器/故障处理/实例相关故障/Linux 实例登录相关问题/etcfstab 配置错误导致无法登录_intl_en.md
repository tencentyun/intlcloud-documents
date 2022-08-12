## Error Description[](id:symptom)
Error: Unable to remotely log in to the Linux CVM via SSH. After logging in to the CVM via VNC, you can check the system start-up failure and view the prompt message "Welcome to emergency mode".
![](https://qcloudimg.tencent-cloud.cn/raw/dea541a48d2a01503c1dbbc85b0d396f.png)


## Possible Causes
The `/etc/fstab` is not properly configured.
For example, you've configured the auto-attaching of disk based on device name in the `/etc/fstab` file. If the device name is changed when the CVM restarts, this configuration will cause the system to fail to start up normally.


## Solutions
See [Steps](#ProcessingSteps) to repair the `/etc/fstab` configuration file. Then, restart the CVM to verify the repaired file.


## Steps[](id:ProcessingSteps)

You can access the instance in the following 2 methods for troubleshooting:

<dx-tabs>
::: Method 1: Login via VNC (recommended)[](id:useVNC)
1. [Log in to Linux Instances (VNC)](https://intl.cloud.tencent.com/document/product/213/32494).
2. After entering the VNC interface, you see the interface shown in [Error Description](#symptom). Enter the root account password and press **Enter** to log in to the server.
 - The entered password is not displayed by default.
 - If you do not have or forgot the root account password, see Method 2 for troubleshooting.
3. [](id:Step3)Run the following command to back up the `/etc/fstab` file to the `/home` directory, for example:
```shellsession
cp /etc/fstab /home
```
4. Run the following command to use VI editor to open the `/etc/fstab` file.
```shellsession
vi /etc/fstab
```
5. Press **i** to enter the edit mode. Move the cursor to the beginning of the error line and enter `#` to comment out this configuration.
<dx-alert infotype="explain" title="">
If you cannot determine the error, it is recommended that you comment out the configurations of all attached disks except the system disks, and then configure the file as instructed in [Step 8](#Step8) after the server recovers.
</dx-alert>
<img src="https://qcloudimg.tencent-cloud.cn/raw/1c238789186d7f24c0244e0307bc3a22.png"/>
6. [](id:Step6)Press **Esc**, enter **:wq**, and press **Enter** to save the configuration and exit the editor.
7. Restart the instance in the CVM console to see if it can be started and logged in properly.
<dx-alert infotype="explain" title="">
Restart the instance through the console. For more information, see [Restarting Instances](https://intl.cloud.tencent.com/document/product/213/4928).
</dx-alert>
8. [](id:Step8)After successful login, if you need to configure the auto-attaching of the disk, see [Cloud Disk Automount Failed upon Linux CVM Restart](https://intl.cloud.tencent.com/document/product/362/40001).

:::
::: Method 2: Use rescue mode[](id:useRescue)
1. Enter the instance rescue mode, see [Using Rescue Mode](https://intl.cloud.tencent.com/document/product/213/46157).
<dx-alert infotype="notice" title="">
Run the `mount` and `chroot` commands as instructed in [Using rescue mode to repair system](https://intl.cloud.tencent.com/document/product/213/46157#.E4.BD.BF.E7.94.A8.E6.95.91.E6.8F.B4.E6.A8.A1.E5.BC.8F.E8.BF.9B.E8.A1.8C.E7.B3.BB.E7.BB.9F.E4.BF.AE.E5.A4.8D), and make sure that you have entered the target system.
</dx-alert>
2. Follow [Step 3](#Step3) - [Step 6](#Step6) in Method 1 to repair the `/etc/fstab` file.
3. Exit the rescue mode as instructed in [Exiting rescue mode](https://intl.cloud.tencent.com/document/product/213/46157#.E9.80.80.E5.87.BA.E6.95.91.E6.8F.B4.E6.A8.A1.E5.BC.8F).
4. After the instance exits the rescue mode, it is still shut down. Start it up as instructed in [Starting Up Instances](https://intl.cloud.tencent.com/document/product/213/38168). Then, verify whether the system can be started up and logged in normally.
5. After successful login, if you need to configure the auto-attaching of the disk, see [Cloud Disk Auto-mount Failed upon Linux CVM Restart](https://intl.cloud.tencent.com/document/product/362/40001).

:::
</dx-tabs>







