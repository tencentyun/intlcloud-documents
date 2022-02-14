## Overview   
The content on CSS is open by default. Anyone with a playback address can access the content. To control access to your live streaming content, you can enable playback authentication.


## How to Configure
To enable playback authentication, you need to generate an encrypted URL and provide it to end users. When an end user requests content using the encrypted URL from a CSS cache node, the node will check the authentication information of the request to determine whether it is valid. If it is, the node will return the content; otherwise, it will reject the request, protecting your live streaming content from unauthorized access.
 

## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live).
- You have added a **playback domain name**.

## Directions
1. Select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the **playback domain** for which you want to enable authentication or click **Manage**.
2. Select **Access Control** and click **Edit** in **Authentication Configuration**.
3. Complete the following settings on the authentication configuration page:
	1. Click the switch next to **Playback Authentication** to enable playback authentication.
	2. Enter a custom primary key, such as `testlive`.
	3. (Optional) Enter a custom backup key, such as `testing`.
	4. Enter the signature validity period, such as `20`.
	5. Click **Save** to save the configuration.

>?
>- Playback authentication of a playback domain name is **disabled** by default.
> - **Authentication Key**: It is user-defined and can contain uppercase and lowercase letters and digits. It includes a primary key (required) and a backup key (optional). You can switch smoothly to the backup key if your primary key is disclosed.
> - **Validity Period**: the validity period of the signature, which is a hexadecimal Unix timestamp.

![](https://main.qcloudimg.com/raw/b2dcc1a646a2e9e6c9bcac665aa5043c.png)
>! After authentication is enabled for the playback domain name, the original playback URL will be inaccessible and an error 403 will be returned. Before enabling this feature, please make sure that your live streaming platform is compatible with the following authentication algorithm so that your streaming services will not be affected.

## Example
Original playback URL:
```
http://www.test.com/live/test01.flv
```

The authentication parameters configured are as follows:
```
Primary key: ngoeiq03
Backup key: -
Validity period: 12495 seconds
```

>! 
>- If you have enabled authentication, the actual expiration time of a URL will be `txTime` plus the validity period of the key.
>- For the sake of convenience, the time you set in the console is the actual expiration time. **If you have enabled authentication, the system will calculate the `txTime` when generating playback URLs.**
>- As long as you start push or playback before the expiration time and the stream is not interrupted, the push or playback can continue even after the URL expires.

Timestamp calculation:
```
Setting time: 2018.12.01 08:30:00
Decimal Unix timestamp: 1543624200
Hexadecimal Unix timestamp: 5C01D608 (case-insensitive). CSS uses hexadecimal timestamps for authentication.
```

Authentication signature calculation:
```
txSecret = MD5(key+StreamName+txTime) 
StreamName is the stream name, which is the same as the StreamID
txTime is the timestamp
key is the authentication key
txSecret = MD5(ngoeiq03+test01+5C01D608)
txSecret = MD5(ngoeiq03test015C01D608)
txSecret = ce797dc6238156d548ef945e6ad1ea20
```

New playback URL:
```
http://www.test.com/live/test01.flv?txSecret=ce797dc6238156d548ef945e6ad1ea20&txTime=5C01D608
```
The expiration time of this URL is 2018.12.01 08:30:00 + 12495 seconds, i.e., 2018.12.01 11:58:15 Beijing time.
If authentication fails or the URL expires, CSS will return 403.
