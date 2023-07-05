Generally, you can troubleshoot most Linux system issues via VNC and rescue mode. This document describes how to troubleshoot the issues such as a failure to log in to a Linux Instance via SSH Key and system failures.


## Troubleshooting Tool
- Login via VNC is a method of remotely connecting to a CVM through a Web browser. This enables you to directly observe the CVM status, or modify the configuration file in the system. Usually when you cannot remotely log in to the instance via SSH key, you can use this login method.
- Rescue mode is generally used when the Linux system cannot be started up normally, or the Linux instance cannot be logged in via VNC. Common usage cases: abnormal fstab configuration, missing key system files, and damaged/missing .lib and .dll files, etc.

## Identifying and Fixing Issues

<dx-accordion>
::: Using VNC to troubleshoot the SSH key login failure[](id:cantSSHlogin)
#### Error description
When I tried to log in to a Linux instance via SSH key, the error message **ssh_exchange_identification: Connection closed by remote host** is displayed.
![](https://qcloudimg.tencent-cloud.cn/raw/4cfe14beb79b3b7b1b617fce540a53a0.png)



#### Possible cause
The connection reset error in the kex_exchange_identification stage generally means that the ssh-related process has been started, but the configuration may be abnormal, for example, the sshd configuration file permissions have been modified.


#### Solutions
See [Steps](#ProcessingSteps1) to check the sshd process, locate and fix the problem.


#### Steps[](id:ProcessingSteps1)
1. [](id:ProcessingSteps1Step1) Follow the steps to log in to the Linux instance via VNC:
   i. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index), find the target Linux CVM, and click **Login** under the "Operation" column.
   ![](https://qcloudimg.tencent-cloud.cn/raw/93c135917fbe34913151bbefc5b48832.png)
    ii. In the **Standard login | Linux instance** window, click **Login via VNC**.
    iii. Enter the username after "login" and press **Enter**, and enter the password after "Password" and press **Enter**. The login is successful when the following information is displayed.
    ![](https://qcloudimg.tencent-cloud.cn/raw/0db1a72ceca22fbf56f8872f60baff4f.png)
2. Run the following command to check whether the sshd process is running normally.
```shellsession
ps -ef | grep sshd
```
If the result shown below is returned, the sshd process is normal.
![](https://qcloudimg.tencent-cloud.cn/raw/c1024ca17237af64df91503164854983.png)
3. Run the following command to view the error cause:
```shellsession
sshd -t
```
If a message similar to "/var/empty/sshd must be owned by root and not group or world-writable." shown below is returned,
the error can be caused by a `/var/empty/sshd/` permission issue.
![](https://qcloudimg.tencent-cloud.cn/raw/19912fbd3406488556cf2e2937a6c2de.png)
You can also check the error messages in the `/var/log/secure` logs to facilitate troubleshooting.
![](https://qcloudimg.tencent-cloud.cn/raw/a696b1ce175631aebcfb92037680b506.png)
4. Run the following command to view the permission of the `/var/empty/sshd` directory.
```shellsession
ll -d /var/empty/sshd/
```
The returned result is shown below. The permission configuration is `777`.
![](https://qcloudimg.tencent-cloud.cn/raw/952ac209bb81e882474f413b31bedfc1.png)
5. Run the following command to modify the permissions of the `/var/empty/sshd/` file.
```shellsession
chmod 711 /var/empty/sshd/
```
The instance can be logged in remotely after a test of [Logging into Linux Instance (SSH Key)](https://intl.cloud.tencent.com/document/product/213/32501).


:::
::: Using VNC to troubleshoot Linux system startup failures[](id:OSStartupFailed)

#### Error description[](id:symptom)
Error: Unable to remotely log in to the Linux CVM via SSH. After logging in to the CVM via VNC, you can check the system start-up failure and view the prompt message "Welcome to emergency mode".
![](https://qcloudimg.tencent-cloud.cn/raw/dea541a48d2a01503c1dbbc85b0d396f.png)


#### Possible cause
The `/etc/fstab` is not properly configured.
For example, you've configured the auto-attaching of disk based on device name in the `/etc/fstab` file. If the device name is changed when the CVM restarts, this configuration will cause the system to fail to start up normally.


#### Solutions
See [Steps](#ProcessingSteps2) to repair the `/etc/fstab` configuration file. Then, restart the CVM to verify the repaired file.


#### Steps[](id:ProcessingSteps2)
1. Follow the [step 1](#ProcessingSteps1Step1) to log in to the Linux instance via VNC.
2. After entering the VNC interface, you see the interface shown in [Error Description](#symptom). Enter the root account password (which is not displayed by default) and press **Enter** to log in to the server.
![](https://qcloudimg.tencent-cloud.cn/raw/7b9a8cdc6fe38ca6cb1e571790a54894.png)
3. After entering the system, run the following command to check whether the drive letter information in the `fstab` file is correct.
```shellsession
lsblk
```
If the result shown below is returned, the drive letter in the file is incorrect:
![](https://qcloudimg.tencent-cloud.cn/raw/be6158d53fcb6e261be719f523cacb93.png)
4. Run the following command to back up the `fstab` file.
```shellsession
cp /etc/fstab /home
```
5. Run the following command to use VI editor to open the `/etc/fstab` file.
```shellsession
vi /etc/fstab
```
6. Press **i** to enter the edit mode. Move the cursor to the beginning of the error line and enter `#` to comment out this configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/a2d9e675d6586341e6b5e3a221ee7906.png)
7. Press **ESC**, enter **:wq**, and press **Enter** to save the configuration and exit the editor.
8. Restart the instance in the CVM console. For more information, see [Restarting Instances](https://intl.cloud.tencent.com/document/product/213/4928).
9. Check if it can be started and logged in properly.


:::
::: Using the rescue mode to troubleshoot Linux system startup failures[](id:rescueModeStartupFailed)
#### Error description

The instance cannot be started up normally after the Linux system restarts. There are many `FAILED` startup failure items in the prompt message.
![](https://qcloudimg.tencent-cloud.cn/raw/ac026f0cbea1eab4761a8557d5078cde.png)



#### Possible cause
The key system files such as. `.bin` and `.lib` files are missing.


#### Solutions
See [Steps](#ProcessingSteps3) to enter the instance rescue mode through the console to troubleshoot.


#### Steps[](id:ProcessingSteps3)

1. Before you enter the rescue mode, we strongly recommend you back up the instance to avoid the impact of maloperations. You can [create snapshots](https://intl.cloud.tencent.com/document/product/362/5755) to back up cloud disks and [create a custom image](https://intl.cloud.tencent.com/document/product/213/4942) to back up local system disks.
2. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1). On the "Instances" page, find the target instance, select **More** > **Ops and check** > **Enter rescue mode**.
![](https://qcloudimg.tencent-cloud.cn/raw/e695226792081b7cebe90507586a1d0f.png)
3. [](id:step3)In the pop-up window, set the instance login password for the rescue mode.
![](https://qcloudimg.tencent-cloud.cn/raw/fdceacda011b0b0678c76c6c1f2a3c56.png)
4. Click **Enter rescue mode**, and the instance status will change to "Entering rescue mode", which typically completes within a few minutes:
![](https://qcloudimg.tencent-cloud.cn/raw/d6ed01e61aeb960da1209040c9383cc7.png)
The status of instance entered the rescue mode changes to "Rescue mode" with a red exclamation mark.
![](https://qcloudimg.tencent-cloud.cn/raw/ca7c6bacd0f11471c23eb4980718f906.png)
5. Use the `root` account and the password set in [step 3](#step3) to log in to the instance as follows:
 - If the instance has a public IP, log in to it as instructed in [Logging in to Linux Instance (SSH Key)](https://intl.cloud.tencent.com/document/product/213/32501).
 - If the instance has no public IPs, log in to it as instructed in [Logging in to Linux Instances (VNC)](https://intl.cloud.tencent.com/document/product/213/32494).
2. This document takes login via VNC as an example. After successful login, run the following commands in sequence to mount the root partition of the system disk.
<dx-alert infotype="explain" title="">
In rescue mode, the device name of the instance system disk is `vda`, and its root partition is `vda1`, which is unmounted by default.
</dx-alert>
```shellsession
mkdir -p /mnt/vm1
```
```shellsession
mount /dev/vda1 /mnt/vm1
```
The returned result is shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/c48cd3e7b83abfc17cff3aedbf6dbfa2.png"/>
7. After successful mounting, you can manipulate the data in the root partition of the original system.
You can also use the `mount -o bind` command to mount some sub-directories in the original file system and use the `chroot` command to run commands in the specified root directory. Below are the specific commands:
```shellsession
mount -o bind /dev /mnt/vm1/dev
mount -o bind /dev/pts /mnt/vm1/dev/pts
mount -o bind /proc /mnt/vm1/proc
mount -o bind /run /mnt/vm1/run
mount -o bind /sys /mnt/vm1/sys
chroot /mnt/vm1 /bin/bash
```
When running the `chroot` command:
 - If there is no error message, you can continue to run the `cd /` command.
 - If the error message as shown below appears, the root directory cannot be switched normally. In this case, you can run `cd /mnt/vm1` to view the root partition data.
![](https://qcloudimg.tencent-cloud.cn/raw/12e2bccf5c19edb4d248ac26d257c31e.png)
8. Through the command, you can check that all files in the `/usr/bin` directory in the original system root partition have been deleted.
![](https://qcloudimg.tencent-cloud.cn/raw/0f2820f10b457378d26c9a6efaf14966.png)
9. In this case, you can create a normal instance using the same operating system, and run the following commands to compress and remotely copy the files in the `/usr/bin` directory of the normal system to the abnormal instance.
 - For the normal instance, run the following commands in sequence:
```shellsession
cd /usr/bin/ && tar -zcvf bin.tar.gz *
```
```shellsession
scp bin.tar.gz root@abnormal instance ip：/mnt/vm1/usr/bin/
```
<dx-alert infotype="explain" title="">
If the instances have public network IPs, the copy can be performed through the public network; otherwise, the copy is performed through the private network.
</dx-alert>
The execution result is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/937f1d97edda8a2b2786b856750dfb5e.png"/>
  - For the abnormal instance, run the following commands in sequence in the rescue mode:
```shellsession
cd /mnt/vm1/usr/bin/
```
```shellsession
tar -zxvf bin.tar.gz
```
```shellsession
chroot /mnt/vm1 /bin/bash
```
The execution result is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/90e4c3d4c06806f07401ec01863dcdfa.png)
10. After repairing the instance, select **More** > **Ops and check** > **Exit rescue mode** under the **Operation** column of the target instance.
![](https://qcloudimg.tencent-cloud.cn/raw/d9f8f26b745a654cb145bbfc4bb1cd2a.png)
11. After exiting the rescue mode, the instance is in a shutdown status. Start up the instance to verify the system. As shown below, the system has been restored.
![](https://qcloudimg.tencent-cloud.cn/raw/705c27323e74f424b775f88567d7252c.png)






:::
</dx-accordion>



