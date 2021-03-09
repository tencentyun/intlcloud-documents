## Overview   
The content on CSS is public by default, and you can access live streaming content once you get the playback URL. If you want to control access, you can enable authentication.


## How to Configure
To enable URL authentication, you need an encrypted URL generated through authentication configuration and provide the URL to end users. After an end user sends a request to an CSS cache node through the encrypted URL, the node checks its permission information to see whether the request is valid. If it is, the node will return the content properly; otherwise, it will reject the request, thereby protecting the live streaming resources.


## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live).
- You have added a **playback domain name**.

## Directions
1. Select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the **playback domain name** to be configured with authentication or **Manage** to enter the domain management page.
2. In **Access Control** > **Authentication Configuration**, click **Edit** to enter the authentication configuration page.
3. Make the following settings on the authentication configuration page:
	1. Click to enable playback authentication.
	2. Enter the custom primary key for authentication, such as `testlive`.
	3. (Optional) Enter the custom secondary key for authentication, such as `testing`.
	4. Enter the signature validity period, such as `20`.
	5. Click **Save** to save the configuration.

>?
>- Playback authentication of a playback domain name is **disabled** by default.
> - **Authentication Key**: it is user-defined and can contain uppercase and lowercase letters and digits. It includes a primary key (required) and a secondary key (optional). The primary-secondary design ensures that the key can be smoothly replaced in case of leakage without interrupting the business.
> - **Validity Period**: the validity period of the signature. The timestamp used is a hexadecimal Unix timestamp.

![](https://main.qcloudimg.com/raw/b2dcc1a646a2e9e6c9bcac665aa5043c.png)
>! After authentication is enabled for the playback domain name, the original playback URL will not be accessible and an error 403 will be returned. Before enabling this feature, please make sure that your live streaming platform is compatible with the following authentication algorithm so that your streaming services will not be affected.

## Configuration Case
If the original playback URL is:
```
http://www.test.com/live/test01.flv
```

When configuring authentication for this domain name, set the following parameters:
```
Primary Key: ngoeiq03
Secondary Key: none
Validity Period: 12495 seconds
```

>! 
>- If you have enabled domain name authentication, the actual expiration time will be `txTime` + authentication validity period.
>- For your convenience, the time set in the console is the actual expiration time. **If you have enabled domain name authentication, `txTime` will be calculated according to the formula when the playback URL is generated.**

Timestamp calculation:
```
Setting time: 2018.12.01 08:30:00
Decimal Unix timestamp: 1543624200
Hexadecimal Unix timestamp: 5C01D608 (authentication configuration in CSS uses a case-insensitive hexadecimal Unix timestamp)
```

Authentication signature calculation:
```
txSecret = MD5(key+StreamName+txTime) 
`StreamName` is the stream name, which is the same as the `StreamID`
`txTime` is the timestamp
`key` is the authentication key
txSecret = MD5(ngoeiq03+test01+5C01D608)
txSecret = MD5(ngoeiq03test015C01D608)
txSecret = ce797dc6238156d548ef945e6ad1ea20
```

The generated playback URL is:
```
http://www.test.com/live/test01.flv?txSecret=6cfcc16fa1eb1200c78b8296468b9180s&txTime=5C01D608
```
The expiration time of this URL is 2018.12.01 08:30:00 + 12495 seconds, i.e., 2018.12.01 11:58:15 Beijing time.
If the authentication fails or the URL has expired, CSS will return a 403 error.
