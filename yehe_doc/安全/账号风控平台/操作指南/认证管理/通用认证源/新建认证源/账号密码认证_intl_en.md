## Scenarios
Customer Identity and Access Management (CIAM) supports authenticating users with their usernames and passwords.

## Steps
1. Log in to the [CIAM console](https://console.cloud.tencent.com/ciam) and select **Authentication management** -> **General authentication source** in the left navigation pane.
2. On the **General authentication source** page, click **Create authentication source**.
![img](https://qcloudimg.tencent-cloud.cn/raw/d99c08fba5148404b496ff5ea1d56861.png)
3. On the **Create authentication source** page, select **Username-password authentication** and click **Next**.
![img](https://qcloudimg.tencent-cloud.cn/raw/914a229db4c3e9dd4f97159e433366b1.png)
4. On the **Create authentication source** page, configure the icon, name, attribute, and description of the authentication source, and then click **Next**.
>?
>- Authentication source icon: The icon displayed in lists and portals. Click **Upload again** to change the default icon.
>- Authentication source name: A name to identify the authentication source.
>- Authentication source attribute: The user attribute used to verify the identities of users during username-password authentication.
>- Authentication source description: A brief description of the authentication source.

![img](https://qcloudimg.tencent-cloud.cn/raw/9fc172925d737eb1916f15042e4e3b22.png)

5. On the **Create authentication source** page, configure the parameters and click **OK** to create the authentication source.
![img](https://qcloudimg.tencent-cloud.cn/raw/e3a6598da4110fa13f39b21bab1487af.png)

#### Policy configuration parameter description [](id:CSSM)
- **Configure password policy**
 - Select password policy: Specifies the required strength of passwords set by users. 5 password policies are supported. By default, the required strength is strong.
 - Password history: Historical passwords. Do not use passwords repeatedly in a short period. The valid range of values is 1-128.
- **Password lock**
 - Password lock: If the password lock is enabled, the number of failed login attempts will be restricted.
 - Lockout threshold: This field is required if the password lock is enabled. If a user's failed login attempts exceed the specified limit, the user is locked and cannot log in until they are unlocked. The valid range of values is 1-999.
 - Retry period: This field is required if the password lock is enabled. If a user exceeds the lockout threshold within the specified period, the user is locked. The valid range of values is 1-99,999 hours.
 - Auto-unlock time: This field is required if the password lock is enabled. The time to wait before a locked user is unlocked. The valid range of values is 1-999,999 minutes.

- **Verification code**
 - Verification code: If verification codes are enabled, when a user exceeds the maximum number of consecutive failed login attempts, verification code-based verification will be automatically enabled.
 - Max attempts: This field is required when verification codes are enabled. If a user's failed login attempts exceed the specified limit, verification code-based verification will be enabled for login. The valid range of values is 1-999.
>! If the password lock is enabled at the same time, we recommend that you set this field to a value smaller than the lockout threshold. Otherwise, a user may be locked before a verification code is triggered.

- **Test password strength**
After configuring a password policy, you can enter a test password to verify whether it meets the password policy.
![img](https://qcloudimg.tencent-cloud.cn/raw/86e57e591d291d1ec7be8d862853c29c.png)