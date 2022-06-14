## Error Description[](id:symptom)
Error: Unable to log in to the CVM. After logging in to the CVM via VNC, you can check the system start-up failure and view the prompt message "Welcome to emergency mode".
![](https://qcloudimg.tencent-cloud.cn/raw/dea541a48d2a01503c1dbbc85b0d396f.png)


## Possible Cause
The `/etc/fstab` is not properly configured.
For example, you've configured the auto-attaching of disk based on device name in the `/etc/fstab` file. If the device name is changed when the CVM restarts, this configuration will cause the system to fail to start up normally.


## Solutions
Repair the `/etc/fstab` configuration file and restart the CVM.


## Steps[](id:ProcessingSteps)

You can access the instance in the following two ways.

<dx-tabs>
::: Log in via VNC (recommended)[](id:useVNC)
1. [Log in to the Linux Instance by using VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. In the VNC page, enter the root account and password and press **Enter** to log in to the server.
 - The password is invisible by default.
 - If you do not have the root account and password, try the Rescue mode.
3. [](id:Step3)Run the following command to back up the `/etc/fstab` file. In the following example, the file is backed up to the `/home` directory. 
```shellsession
cp /etc/fstab /home
```
4. Run the following command to open the `/etc/fstab` file in VI editor.
```shellsession
vi /etc/fstab
```
5. Press **i** to enter the edit mode. Move the cursor to the beginning of the error line and enter `#` to comment out this configuration.
<dx-alert infotype="explain" title="">
If you are not sure about the error, comment out the configurations of all attached disks except the system disks. You can recover these configurations as instructed in [Step 8](#Step8) after fixing the problem.
</dx-alert>
<img src="https://qcloudimg.tencent-cloud.cn/raw/1c238789186d7f24c0244e0307bc3a22.png"/>
6. [](id:Step6)Press **Esc**, enter **:wq**, and press **Enter** to save the configuration and exit the editor.
7. Restart the instance through the console, and verify whether it can be started up and logged in normally.
<dx-alert infotype="explain" title="">
See [Restarting Instances](https://intl.cloud.tencent.com/document/product/213/4928).
</dx-alert>
8. [](id:Step8)After successful login, if you need to configure the auto-attaching of the disk, see [Cloud Disk Automount Failed upon Linux CVM Restart](https://intl.cloud.tencent.com/document/product/362/40001).

:::
::: Rescue mode[](id:useRescue)
1. Enter the instance rescue mode. See [Using Rescue Mode](https://intl.cloud.tencent.com/document/product/213/46157).
<dx-alert infotype="notice" title="">
Run the `mount` and `chroot` commands described in [Using rescue mode to repair system](https://intl.cloud.tencent.com/document/product/213/46157?lang=en&pg=#using-rescue-mode-to-repair-system), and make sure that you have entered the target system.
</dx-alert>
2. Follow [Step 3](#Step3) - [Step 6](#Step6) in Method 1 to repair the `/etc/fstab` file.
3. Exit the instance rescue mode. See [Exiting rescue mode](https://intl.cloud.tencent.com/document/product/213/46157?lang=en&pg=#exiting-rescue-mode).
4. After the instance exits the rescue mode, it is still shut down. Start it up as instructed in [Starting Up Instances](https://intl.cloud.tencent.com/document/product/213/38168). Then, verify whether the system can be started up and logged in normally.
5. After successful login, if you need to configure the auto-attaching of the disk, see [Cloud Disk Auto-mount Failed upon Linux CVM Restart](https://intl.cloud.tencent.com/document/product/362/40001).

:::
</dx-tabs>







