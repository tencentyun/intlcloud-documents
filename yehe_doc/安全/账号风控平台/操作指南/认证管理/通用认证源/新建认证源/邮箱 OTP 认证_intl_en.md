## Scenarios
Customer Identity and Access Management (CIAM) supports the email OTP authentication source. That is, the system authenticates a user by sending an OTP to the email address of the user.

## Steps
1. Log in to the [CIAM console](https://console.cloud.tencent.com/ciam) and select **Authentication management** -> **General authentication source** in the left navigation pane.
2. On the **General authentication source** page, click **Create authentication source**.
![img](https://qcloudimg.tencent-cloud.cn/raw/10fdc9fbf08d31cda7af0281de00ad23.png)
3. On the **Create authentication source** page, select **Email OTP** and click **Next**.
4. On the **Create authentication source** page, configure the icon, name, attribute, and description of the authentication source, and then click **Next**.
>?
>- Authentication source icon: The icon displayed in lists and portals. Click **Upload again** to change the default icon.
>- Authentication source name: A name to identify the authentication source.
>- Authentication source attribute: The email OTP authentication source uses the email attribute by default. This field cannot be modified.
>- Authentication source description: A brief description of the authentication source.

![img](https://qcloudimg.tencent-cloud.cn/raw/e738c79f6a17cd0d2af6f3776db7fef9.png)

5. On the **Create authentication source** page, configure the parameters and click **OK** to create the authentication source.
>?
>- Email verification code length: The length of email OTPs sent to users. The valid range of values is 1-128 bit.
>- Email verification code validity: The validity period of email OTPs. The valid range of values is 1-300 seconds.

![img](https://qcloudimg.tencent-cloud.cn/raw/befb2dc82fa5ce452d28404d37ae4242.png)