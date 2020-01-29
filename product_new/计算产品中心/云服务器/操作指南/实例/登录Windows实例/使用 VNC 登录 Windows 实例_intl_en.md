## Scenario

VNC login offered by Tencent allows users to remotely connect to a CVM via a web browser. If a client does not have remote login installed, it cannot be used or logged into via any other means, users can connect to a CVM using VNC login to observe the CVM’s status and do basic CVM management operations using the CVM account.

## Use Limits

- Features such as copy/paste, Chinese input, and file upload/download are currently not supported on CVMs using VNC login.
- Mainstream browsers must be used when using VNC login on a CVM, such as Chrome, Firefox, and IE 10 or above.
- A VNC login is a dedicated terminal, meaning only one user can use a VNC login at a time.

## Applicable OS

Windows, Linux, or macOS.

## Prerequisites

You must already have admin account/password for logging into Windows instance remotely.
- If you use a system default password to log in to the instance, obtain it by visiting [Internal Message](https://console.cloud.tencent.com/message).
If you forgot the password, then [reset instance password](http://intl.cloud.tencent.com/document/product/213/16566).

## Steps

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the instance’s management page, select the Windows CVM that you want to log in to and click **Log In**, as shown below:
![](https://main.qcloudimg.com/raw/038fce530c6c6827796e51d896306a93.png)
3. In the **Log into Windows instance** pop-up window, select **Alternative login methods (VNC)** and click **Log In Now**, as shown below.
![](https://main.qcloudimg.com/raw/9f282782aa5096a82c05af675ff02203.png)
4. In the login window, select “Send Remote Command” in the top left corner, and press **Ctrl-Alt-Delete** to enter the system login interface as shown below:
![](https://main.qcloudimg.com/raw/2dec43fa6ddb5e442da59c75f7a34b0f.png)



