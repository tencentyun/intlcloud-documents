## Scenario


VNC login offered by Tencent allows users to remotely connect to a CVM via a web browser. If a client does not have remote login installed, it cannot be used or logged into via any other means, users can connect to a CVM using VNC login to observe the CVM’s status and do basic CVM management operations using the CVM account.

## Applicable OS

Windows, Linux, or macOS.

## Use Limits

- Features such as copy/paste, Chinese input, and file upload/download are currently not supported on CVMs using VNC login. 
- Mainstream browsers must be used when using VNC login on a CVM, such as Chrome, Firefox, and IE 10 or above.
- A VNC login is a dedicated terminal, meaning only one user can use a VNC login at a time.

## Prerequisites
You must already have the admin account/password (or key) for logging into Linux instance.
- If you use a system default password to log in to the instance, obtain it by visiting [Internal Message](https://console.cloud.tencent.com/message).
If you forgot the password, then [reset instance password](http://intl.cloud.tencent.com/document/product/213/16566).

## Steps

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the instance’s management page, select the Linux CVM that you want to log in to and click **Log In**, as shown below:
![](https://main.qcloudimg.com/raw/b7f0594ddecad128707ee720502e10b0.png)
3. In the **Log into Linux instance** pop-up window, select **Alternative login methods (VNC)** and click **Log In Now**, as shown below.
![](https://main.qcloudimg.com/raw/6d4eb31a5c3e127f7214b31db263bc5a.png)
4. Enter the username/password in the pop-up dialog box to complete the login process, as shown below:
![](https://main.qcloudimg.com/raw/bab14d0f56db2f3bc1ab949e08fcc0f0.png)

## Subsequent Actions

After successfully logging in to the CVM, you can build a personal website or forum on the Tencent Cloud CVM or do other operations. For related operations, refer to the following:
- [Building a personal WordPress website]
- [Building a Discuz! forum]

