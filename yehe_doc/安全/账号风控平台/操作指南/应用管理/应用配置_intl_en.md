## Scenarios
Customer Identity and Access Management (CIAM) allows administrators to configure created applications as needed, including the basic information (such as the icon and name), the parameters (such as the redirect and logout addresses), and the processes (such as registration, login, password reset, and protocol management).

## Steps
1. Log in to the [CIAM console](https://console.tencentcloud.com/ciam) and select **Application management** in the left navigation pane.
2. On the **Application management** page, click **Configuration** in the operation column.
![img](https://qcloudimg.tencent-cloud.cn/raw/f62642ab3f8f7daee9f1fb96f4e64f95.png)

### Basic information
![img](https://qcloudimg.tencent-cloud.cn/raw/e59c8e64dc4077735087dbb24ccc54dc.png)

### Parameter configuration
1. On the **Application configuration** page, click the **Parameter configuration** tab.
2. On the **Parameter configuration** tab, fill in the required information and click **OK** to save the configuration.
![img](https://qcloudimg.tencent-cloud.cn/raw/a63735cbd86086674c779b1a10948c1b.png)

Parameter description:

| Parameter                 | Description                                                         | Example                                    |
| -------------------- | ------------------------------------------------------------ | ----------------------------------------- |
| Redirect URI        | A complete URL starting with http or https for receiving the OAuth authorization code. After the user authorizes the request, this code will be redirected to the address. | [https://www.qq.com](https://www.qq.com/) |
| Logout Redirect URI | A complete URL starting with http or https, to which the user will be redirected after logout. | https://www.qq.com/logout                 |
| Access_token validity | The validity period of access tokens. The default validity is 600 seconds.                               | 600                                       |
| refresh_token         | Specifies whether refresh tokens are enabled.                                       | -                                         |
| Refresh_token validity period | The validity period of refresh tokens. This parameter is displayed when refresh tokens are enabled. The default validity is 86,400 seconds. | 86400                                     |


### Process configuration
You can configure the registration, login, MFA, username retrieval, and password reset processes. By configuring different parameters, you can customize the registration, login, and other processes for applications.

For Web applications, one-page applications, and mobile apps, you can configure the registration, login, MFA, username retrieval, and password reset processes.

#### Configuring Web applications, one-page applications, and mobile apps
1. On the **Application configuration** page, click the **Process configuration** tab.
2. The **Process configuration** tab contains five modules for the registration, login, MFA, username retrieval, and password reset processes.
 - **Registration**: Click **Edit** in the upper right corner of the module to configure the parameters, and then click **OK** to save the configuration.
 ![img](https://qcloudimg.tencent-cloud.cn/raw/065bed07c86f39ec36f01089c5a8797c.png)

 **Parameter description:**
   - On/Off: By default, the toggle is turned on. Users cannot register for the application if the toggle is turned off.
    
   - Authentication attribute: This field is filled in by users during registration. It can be used as a unique user identifier.
    
   - SMS OTP authentication source: The policy for sending SMS OTPs during registration. This field must be configured if you select the phone number as the authentication attribute.
    
   - Email OTP authentication source: The policy for sending email OTPs during registration. This field must be configured if you select the email address as the authentication attribute.
    
   - General attribute: This field is filled in by users during registration. It cannot be used as a unique user identifier.
    
   - User group: The group to which users belong after successful registration.
    
   - Auto login: If the toggle is turned on, users are automatically logged in to the application after successful registration. If the toggle is turned off, users are redirected to the login page after successful registration and need to log in.
    
   - Consent statement: If the toggle is turned on, you can configure the consent statement displayed on the registration page as instructed below.
     
      ![img](https://qcloudimg.tencent-cloud.cn/raw/07c36b6b77876cd8b7dfe66a33ccf9e6.png)

 - **Login**: Click **Edit** in the upper right corner of the module to configure the parameters, and then click **OK** to save the configuration.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/70c557c7ff753110251c74f27e1a0bb8.png)
   **Parameter description:**
   
   - On/Off: By default, the toggle is turned on. Users cannot log in to the application if the toggle is turned off.
   - Preferred authentication source: The preferred authentication method displayed on the login page.
   - Associate authentication source: The alternative authentication method displayed on the login page.
   - claims: The obtained token and the user attribute field returned by the DescribeUserInfo API.
   - Remember password: Specifies whether the browser remembers the password.
   - Consent statement: If the toggle is turned on, you can configure the consent statement displayed on the login page.
   
 - **MFA**: Click **Edit** in the upper right corner of the module to configure the parameters, and then click **OK** to save the configuration.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/406d568e4bb00ca61bc8e7d6ee75fb5d.png)
**Parameter description:**
   
   - On/Off: By default, the toggle is turned off. If the toggle is turned on, 2FA will be enabled.
   - Associate authentication source: The authentication method. The valid values include SMS OTP and email OTP authentication sources.
   
 - **Process of retrieving username**: Click **Edit** in the upper right corner of the module to configure the parameters, and then click **OK** to save the configuration.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/d7ec0398ce185af23d034c3c39f449a8.png)
**Parameter description:**
   
   - On/Off: By default, the toggle is turned on. Users cannot retrieve their usernames if the toggle is turned off.
   - Retrieving method: The method of receiving usernames, such as email.
   
 - **Process of resetting password**: Click **Edit** in the upper right corner of the module to configure the parameters, and then click **OK** to save the configuration.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/4f995aab8e8fa8278b7f411df15c5bd3.png)

 **Parameter description:**

   - On/Off: By default, the toggle is turned on. Users cannot reset their passwords if the toggle is turned off.
   - Retrieving method: The method of receiving verification codes to reset passwords, such as email.

### CORS
To call CIAM APIs by using JavaScript, you need to configure trusted CORS security domains. Up to 10 security domains are allowed.
1. On the **Application configuration** page, click **CORS** to go to the **CORS configuration** page.
2. On the **CORS configuration** page, click **Edit**.
![img](https://qcloudimg.tencent-cloud.cn/raw/8867afd3c9121938488b9e7613af4f09.png)
3. Fill in the required information and click **OK** to save the configuration.
![img](https://qcloudimg.tencent-cloud.cn/raw/710a263544c07ee2cbe3ecdc59735227.png)


#### Notes
- The redirect URI of the application is added to the CORS security domain by default. You do not need to configure it here.
- Format of CORS: <protocol> "://" <domain or IP> [ ":" <port> ]. For example, https://sample.portal.tencentciam.com or http://127.0.0.1:8080. Note that it must start with https:// or http://, and cannot include the request path.
- The domain name can only contain [a-z], [0-9] and [.*-]. "-" cannot be used at the beginning or end of the domain name, and it cannot be used consecutively. The wildcard (*) is only allowed in the first part of the domain name, e.g. https://*.example.com.