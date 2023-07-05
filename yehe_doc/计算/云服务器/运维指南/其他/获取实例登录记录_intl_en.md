## Overview
This document describes how to obtain user login records of a CVM instance.


## Directions

<dx-tabs>
::: Linux instances
<dx-alert infotype="explain" title="">
This document uses a Linux instance on TencentOS Server 3.1 (TK4) as an example. As the steps may vary by operating system, proceed based on the actual conditions.
</dx-alert>

1. [Log in to the Linux instance by using Web Shell](https://intl.cloud.tencent.com/document/product/213/5436).
2. You can view the following user login information as needed:
<dx-alert infotype="explain" title="">
User login logs are usually stored in the `/var/run/utmp`, `/var/log/wtmp`, `/var/log/btmp`, and `/var/log/lastlog` files.
</dx-alert>
 - Run the `who` command to view the information of the currently logged-in user in the `/var/run/utmp` file. The returned result is as follows:
<img src="https://qcloudimg.tencent-cloud.cn/raw/2f54911fac9ee5cbeb2ca180a802f8bc.png"/>
 - Run the `w` command to view the username of the currently logged-in user and display the currently executed tasks of the user in the `/var/run/utmp` file. The returned result is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/401681d683aafd6cd6ab0f5ffda15cd8.png)
 - Run the `users` command to view the username of the currently logged-in user in the `/var/run/utmp` file. The returned result is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/94f318f2bfa670fae34a0a0015f7587d.png)
 - Run the `last` command to view the information of the currently and historically logged-in users in the `/var/log/wtmp` file. The returned result is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/1262a858b41be61a01d2d31e09c2cc70.png)
 - Run the `lastb` command to view the information of all the users who failed to log in to the system in the `/var/log/btmp` file. The returned result is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/2208f07aba6e73fa4de6959844d38ca5.png)
 - Run the `lastlog` command to view the last user login information in the `/var/log/lastlog` file. The returned result is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/85e42c825afa0bab0e1b25e18895ac52.png)
 - Run the `cat /var/log/secure` command to view the login information. The returned result is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/d75c5db721f325d56ed0ba7dd4a20c7b.png)

:::
::: Windows instances

<dx-alert infotype="explain" title="">
This document uses a Windows instance on Windows Server 2012 R2 English as an example. As the steps may vary by operating system, proceed based on the actual conditions.
</dx-alert>


1. [Log in to the Windows instance by using WebRDP](https://intl.cloud.tencent.com/document/product/213/41018).
2. On the desktop, click <img src="https://main.qcloudimg.com/raw/446c1e8cb7da2ce280d710c6a46b693d.png" style="margin:-6px 0px"> to open Server Manager.
3. In the **Server Manager** window, select **Tools** > **Event Viewer** in the top-right corner.
4. In the **Event Viewer** pop-up window, select **Windows Logs** > **Security** on the left and click **Filter Current Log** on the right.
5. In the **Filter Current Log** pop-up window, enter `4648` in **<All Event IDs>** and click **OK**.
6. In the **Event Viewer** window, double-click the logs that meet the filters.
7. In the **Event Property** pop-up window, click **Details** to view the client name and address as well as event recording time.



:::
</dx-tabs>



