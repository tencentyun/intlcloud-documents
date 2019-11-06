Multi-Factor Authentication (MFA) is a simple and effective security authentication method. It adds an additional layer of protection to strengthen the user name and password credentials. An MFA device, also called a dynamic password card or token, is a device that provides this type of secure authentication method. Tencent Cloud currently offers two types of MFA devices: hardware MFA devices and virtual MFA devices.


## Hardware MFA Devices
The figure below shows some examples of our hardware MFA devices. The 6-digit dynamic authentication code displayed is updated every 30 seconds, and the serial number of the MFA device is on the back. Currently this device is only available to beta users.
![](https://main.qcloudimg.com/raw/efbf89cf14546aaf0b775df9af863b8a.png)


### Binding a Hardware MFA Device
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com), and click the account name in the upper right corner. Click **Security Settings**.
2. When on the security settings page, select **Basic Settings** > **MFA Device**. Click **Bind**.
3. The identity verification window will pop up. Complete the identity verification according to the prompts.
4. Select the hardware MFA device, and enter the serial number and authentication code. Follow the directions on the page to perform the binding operation.
<!--![]()-->
5. Click **Submit** to complete the binding of the hardware MFA device.


### Unbinding a Hardware MFA Device
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com), and click the account name in the upper right corner. Click **Security Settings**.
2. When on the security settings page, select **Basic Settings** > **MFA Device**. Click **Unbind**.
3. Click **OK** in the popup box.
4. The identity verification window will pop up. Complete the identity verification according to the prompts.
5. Complete the unbinding.




## Virtual MFA Device
A virtual MFA device is an application program that generates a dynamic authentication code. It is compliant with the time-based one-time password (TOTP) standard, RFC 6238. Tencent Cloud’s virtual MFA device is supported by the Tencent Cloud Assistant mini program.


### Binding a Virtual MFA Device
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com), and click the account name in the upper right corner. Click **Security Settings**.
2. When on the security settings page, select **Basic Settings** > **MFA Device**. Click **Bind**.
3. The identity verification window will pop up. Complete the identity verification according to the prompts.
4. Select the virtual MFA device, and follow the directions on the page to perform the binding operation.
<!-- ![]() -->
5. Click **Submit** to complete the binding of the virtual MFA device.




### Unbinding a Virtual MFA Device
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com), and click the account name in the upper right corner. Click **Security Settings**.
2. When on the security settings page, select **Basic Settings** > **MFA Device**. Click **Unbind**.
3. Click **OK** in the popup box.
4. In the identity verification page that pops up, enter the 6-character dynamic authentication code and click **OK** to complete the unbinding.



