## Scenario


VNC login provided by Tencent Cloud allows users to remotely log in to CVM via a web browser. If a client does not have remote login installed or it cannot be used, user can log in to the CVM using VNC login to check the CVM status and perform basic management operations using the CVM account.    

## Applicable OS

Windows, Linux, or macOS.

## Use Limits

- VNC login currently does not support copy and paste, Chinese input method, and file upload or download.
- When you use VNC to log in to CVM, mainstream browsers must be used, such as Chrome, Firefox, IE 10 and above.
- VNC login is a dedicated terminal, meaning only one user can use VNC login at a time.

## Prerequisites
You must already have the admin account and password (or key) of the Linux instance to be logged in to.
- If you use a system default password to log in to the instance, first go to [Internal Message](https://console.cloud.tencent.com/message) to get it.
- If you forget your password, please [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).

## Directions

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the Instance management page, select the Linux CVM you want to log in to and click **Log In**, as shown below:
![](https://main.qcloudimg.com/raw/a4cc736f2dc7f13bf39756b8e39532d4.png)
3. In the **Log into Linux instance** window that pops up, select **Alternative login methods (VNC)** and click **Log In Now**, as shown below.
![](https://main.qcloudimg.com/raw/1bd4877abc15d06adb8c54fc7ed1318e.png)
4. In the pop-up dialog box, enter the username after **login** and press **Enter**.
5. Enter the password after **Password** and press **Enter**.
The entered password is not displayed by default, as shown below:
![](https://main.qcloudimg.com/raw/03a8492f66e8342221858709b6068669.png)
After logging in, information about the CVM that you currently log in to appears to the left of the command prompt. 

## Subsequent Operations

After logging in to the CVM, you can build a personal website or forum or perform other operations. For more information, see the following documents:
- [Build a personal WordPress site](https://intl.cloud.tencent.com/document/product/213/8044?from_cn_redirect=1)
- [Build a Discuz! forum](https://intl.cloud.tencent.com/document/product/213/8043?from_cn_redirect=1)

