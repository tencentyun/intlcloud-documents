## Scenarios
Customer Identity and Access Management (CIAM) supports the SMS OTP authentication source. That is, the system authenticates a user by sending an OTP to the mobile number of the user.

## Steps
1. Log in to the [CIAM console](https://console.cloud.tencent.com/ciam) and select **Authentication management** -> **General authentication source** in the left navigation pane.
2. On the **General authentication source** page, click **Create authentication source**.
![img](https://qcloudimg.tencent-cloud.cn/raw/d9b4ac30768e6f063a4deaaf669172f8.png)
3. On the **Create authentication source** page, select **SMS OTP** and click **Next**.
4. On the **Create authentication source** page, configure the icon, name, attribute, and description of the authentication source, and then click **Next**.
>?
>- Authentication source icon: The icon displayed in lists and portals. Click **Upload again** to change the default icon.
>- Authentication source name: A name to identify the authentication source.
>- Authentication source attribute: The SMS OTP authentication source uses the phone number attribute by default. This field cannot be modified.
>- Authentication source description: A brief description of the authentication source.

![img](https://qcloudimg.tencent-cloud.cn/raw/d2f0420d5d7932bb4fc96533043250af.png)

5. On the **Create authentication source** page, configure the parameters and click **OK** to create the authentication source.
>?
>- Length of verification code: The length of SMS OTPs sent to users. The valid range of values is 1-6 bit.
>- Validity period of SMS verification code: The validity period of SMS OTPs. The valid range of values is 1-300 seconds.

![img](https://qcloudimg.tencent-cloud.cn/raw/1c99eb78341a597428ddf987d625a89a.png)