
This document describes how to configure a macOS project for the GME APIs for macOS.


## SDK Preparations
1. Download the applicable demo and SDK. For more information, please see [Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).
2. Decompress the obtained SDK resources.
3. The extracted `GMESDK.framework` is the resource related to GME.




## Configuration Guide


Add the following dependent libraries to `Link Binary With Libraries` in Xcode as needed and configure `Framework Search Paths` to point to the directory where the SDK is located as shown below:  
![](https://main.qcloudimg.com/raw/b6156b8c7a596248c148607070e38f67.png)
