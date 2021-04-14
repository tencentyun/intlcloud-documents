Multi-Factor Authentication (MFA) is a simple and effective security authentication method. It adds an additional layer of protection to strengthen the username and password credentials. An MFA device, also called a dynamic password card or token, is a device that enables this authentication method. Tencent Cloud currently offers two types of MFA devices: hardware MFA devices and virtual MFA devices.

## Hardware MFA Devices
>?Currently, hardware MFA devices are only available for beta users.

The figure below shows some examples of hardware MFA devices. The 6-digit dynamic authentication code displayed is updated every 30 seconds, and the serial number of the MFA device is on the back.
![](https://main.qcloudimg.com/raw/00e6a241a9091978fbb2e11a9e126a88.png)

### Binding a hardware MFA device
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com), click the account name in the top-right corner, and click **Security Settings**.
2. Go to **Basic Settings** > **MFA Device** and click **Bind**.
3. Complete the identity authentication as prompted on the authentication window that pops up.
4. Select a hardware MFA device, enter the serial number and authentication code, and bind the device as prompted.
5. Click **Submit** to complete the binding of the hardware MFA device.


### Unbinding a hardware MFA device
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com), click the account name in the top-right corner, and click **Security Settings**.
2. Go to **Basic Settings** > **MFA Device** and click **Unbind**.
3. Click **Confirm** in the pop-up box.
4. Complete the identity authentication as prompted on the authentication window that pops up.
5. Complete the unbinding.




## Virtual MFA Device
A virtual MFA device is an application program that generates dynamic authentication codes. It is compliant with the time-based one-time password (TOTP) standard as defined in RFC 6238. Tencent Cloud's virtual MFA devices are supported by the Tencent Cloud Assistant mini program.


### Binding a virtual MFA device
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com), click the account name in the top-right corner, and click **Security Settings**.
2. Go to **Basic Settings** > **MFA Device** and click **Bind**.
3. Complete the identity authentication as prompted on the authentication window that pops up.
4. Select a virtual MFA device and bind it as prompted.
![](https://main.qcloudimg.com/raw/d6a3683609538ffc9e88d6eec502e7b6.png)
5. Click **Submit** to complete the binding of the virtual MFA device.




### Unbinding a virtual MFA device
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com), click the account name in the top-right corner, and click **Security Settings**.
2. Go to **Basic Settings** > **MFA Device** and click **Unbind**.
3. Click **Confirm** in the pop-up box.
4. On the authentication page that pops up, enter the 6-digit dynamic authentication code and click **OK** to complete the unbinding.



