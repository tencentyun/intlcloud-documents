## Overview
VNC login allows for remote login of Lighthouse instances by using a web browser. If the remote login client is not available and all the other login methods failed, you can log in to an instance via VNC to check the instance status and perform basic management operations.

## Usage Limits
- VNC does not support copy and paste, and file upload or download.
- Use a mainstream browser, such as Chrome, Firefox, and IE 10 or later.
- Only one user can log in to an instance by using VNC at a time.

## Prerequisites
You must have the admin account and password for logging in to a Linux instance remotely.

<dx-alert infotype="notice" title="">
Make sure you’ve set the login password. For more information, see [Resetting Password](https://intl.cloud.tencent.com/document/product/1103/41553).
</dx-alert>


## Directions
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Find the target instance and enter its details page.
3. Select **Remote login** and click **Log in** under **VNC Login**.
![](https://qcloudimg.tencent-cloud.cn/raw/d5c30961df2a9c3234bc0daa3112a684.png)
4. In the pop-up window, enter the username after *login* and press Enter.
5. Enter the password after **Password** and press Enter.
The entered password is invisible by default.
![](https://qcloudimg.tencent-cloud.cn/raw/82ce6bce1fd5cbde4ddce81b97b7091f.png)
Once logged in, you can see the information of the instance on the left of the command prompt.
<dx-alert infotype="explain" title="">
Click **Send remote command** in the top-left corner and select the command you want.
</dx-alert>

