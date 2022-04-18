
## Overview
This document describes how to get the configuration information in the HTTPDNS console and what information items mean. You need to get such configuration information before you can connect to HTTPDNS.

## Prerequisites
You have activated HTTPDNS as instructed in [Activating HTTPDNS](https://intl.cloud.tencent.com/document/product/1130/44461).


## Directions
Log in to the [**Development Configuration** page](https://console.cloud.tencent.com/httpdns/configure) in the HTTPDNS console to query your configuration information.
![](https://qcloudimg.tencent-cloud.cn/raw/79eee38b6975ee2a6c23bd86a558488e.png)

- **Authorization ID**: It is the unique ID of a development configuration used in HTTPDNS, i.e., the authorization ID parameter passed in when you call the HTTP query API `http://119.29.29.28` of HTTPDNS.
- **DES encryption key**: The key used to encrypt the DNS request data when you call the HTTP DNS API `http://119.29.29.98` of HTTPDNS with DES encryption used.
- **AES encryption key**: The key used to encrypt the DNS request data when you call the HTTP DNS API `http://119.29.29.98` of HTTPDNS with AES encryption used.
- **HTTPS encryption token**: The token used to authenticate the DNS request data when you call the HTTPS DNS API `https://119.29.29.99` of HTTPDNS.
>?If the following two items are not displayed in the console, **request an application** first to view them. For detailed directions, see [SDK Activation Process](https://intl.cloud.tencent.com/document/product/1130/44474).
>
-  **iOS APPID**: The `appId (application ID)` authentication information for using the [SDK for iOS](https://intl.cloud.tencent.com/document/product/1130/44472) provided by HTTPDNS.
- **Android APPID**: The `business appkey` authentication information for using the [SDK for Android](https://intl.cloud.tencent.com/document/product/1130/44473) provided by HTTPDNS.


