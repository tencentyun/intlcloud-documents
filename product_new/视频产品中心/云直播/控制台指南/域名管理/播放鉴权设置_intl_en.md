## Scenario
The content on LVB is public by default, and you can access live streaming content once you get the playback address. If you want to control access, you can enable authentication.


## How to Configure
To enable URL authentication, you need an encrypted URL generated through authentication configuration and provide the URL to end users. After an end user sends a request to an LVB cache node through the encrypted URL, the node checks its permission information to see whether the request is valid. If it is, the node will return the content properly; otherwise, it will reject the request, thereby protecting the live streaming resources.


## Prerequisites
You have logged in to the [LVB Console](https://console.cloud.tencent.com/live).

## Steps
1. Select **Manage Domain** in the left sidebar, click the playback domain name to be configured or click **Manage** in the operation column to enter the domain name management page.
![](https://main.qcloudimg.com/raw/53cc67e72f3f9a2e180dcc3f2b5866a9.png)
2. In the **Access Control** tab, you can see the **Authentication Configuration** feature, which is disabled by default. Click **Edit** to configure the playback authentication.
![](https://main.qcloudimg.com/raw/28d4ceb1de74af24c3fdca8f7884c6c1.png)
3. After playback authentication is enabled, enter the **Authentication Key** and **Validity Period** based on your needs.
![](https://main.qcloudimg.com/raw/65521c61a9f37172d4e67827e71a16f1.png)
 - **Authentication Key**: it is user-defined and can contain uppercase and lowercase letters and numbers. It includes a master key (required) and a slave key (optional). The master/slave design ensures that the key can be smoothly replaced in case of leakage without interrupting the business.
 - **Validity Period**: the validity period of the signature. The timestamp used is a hexadecimal Unix timestamp.

>After authentication is enabled for the playback domain name, the original playback URL will not be accessible and an error 403 will be returned. Before enabling this feature, please make sure that your live streaming platform is compatible with the following authentication algorithm so that your streaming services will not be affected.

## Configuration Sample
If the original playback URL is:
```
http://www.test.com/live/test01.flv
```

When configuring authentication for this domain name, use the following parameters:
```
Master Key: ngoeiq03
Slave Key: None
Validity Period: 12495 seconds
```

Timestamp calculation:
```
Setting time: 2018.12.01 08:30:00
Decimal Unix timestamp: 1543624200
Hexadecimal Unix timestamp: 5c01d608 (authentication configuration in LVB uses a hexadecimal Unix timestamp)
```

Authentication signature calculation:
```
txSecret = MD5(key+StreamName+txTime) 
StreamName is the stream name, which is the same as the StreamID.
txTime is the timestamp
Key is the authentication key
txSecret = MD5(ngoeiq03+test01+5c01d608)
txSecret = MD5(ngoeiq03test015c01d608)
txSecret = 6cfcc16fa1eb1200c78b8296468b9180

```

The generated playback URL is:
```
http://www.test.com/live/test01.flv?txSecret=6cfcc16fa1eb1200c78b8296468b9180s&txTime=5c01d608
```
The expiration time of this URL is 2018.12.01 08:30:00 + 12495 seconds, i.e., 2018.12.01 11:58:15 Beijing time.
If the authentication fails or the URL has expired, LVB will return an error of 403.
