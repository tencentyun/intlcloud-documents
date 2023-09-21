Multi-Factor Authentication (MFA) is a simple and effective security authentication method. It adds another layer of account protection in addition to a username and password. An MFA device, also called a dynamic password card or token, is a device that provides this type of secure authentication method. Tencent Cloud currently provides virtual MFA devices.


## Virtual MFA Device
A virtual MFA device is an application program that generates dynamic authentication codes. It is compliant with the time-based one-time password (TOTP) standard as defined in RFC 6238. Tencent Cloud's virtual MFA devices are currently only supported by Google Authenticator.


### Binding a virtual MFA device
1. Log in to the [Tencent Cloud console](https://console.tencentcloud.com), click the account name in the top-right corner, and click **Security settings**.
2. Go to **Basic Settings** > **MFA Device** and click **Bind**.
3. Complete the identity authentication as prompted on the authentication window that pops up.
4. Select the virtual MFA device, and follow the directions on the page to perform the binding operation.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/93Gu802_MFA1.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fJg3864_MFA2.png)
5. Click **Submit** to complete the binding of the virtual MFA device.


### Unbinding a virtual MFA device
1. Log in to the [Tencent Cloud console](https://console.tencentcloud.com), click the account name in the top-right corner, and click **Security settings**.
2. Go to **Basic Settings** > **MFA Device** and click **Unbind**.
3. Click **OK** in the pop-up window.
4. In the identity verification page that pops up, enter the 6-character dynamic authentication code and click **OK** to complete the unbinding.
