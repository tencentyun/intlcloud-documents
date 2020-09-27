This document describes how to configure an iOS project for the GME APIs for iOS.

## SDK Preparations

1. Download the applicable demo and SDK. For more information, please see [Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).
2. Decompress the obtained SDK resources.
3. The folder contains:
 - GMESDK.framework: native resource related to iOS development.
 - libGMESDK.a: Unity resource related to iOS development (you can ignore this file if you don't use the Unity engine for development).


>The SDK can run on iOS 7.0 and higher.


## Configuration Guide

1. Add the following dependent libraries to `Link Binary With Libraries` in Xcode as needed and configure `Framework Search Paths` to point to the directory where the SDK is located as shown below:  
![](https://main.qcloudimg.com/raw/52279cead356362dce146ebb013a25d6.png)
2. Add dependent libraries as shown below:
![](https://main.qcloudimg.com/raw/b6156b8c7a596248c148607070e38f67.png)
3. Bitcode needs to support all the class libraries at the same time that the project depends on. As the SDK does not support Bitcode yet, you can temporarily disable it.
To disable this feature, search for Bitcode under **Targets** > **Build Settings** and set the corresponding option to `NO`.
![](https://main.qcloudimg.com/raw/82c628e8a7d9a4bebc842c8545d9563a.png)
4. The GME SDK for iOS requires the following permissions:
 - Required background modes: allows running in the background (optional).
 - Microphone Usage Description: grants the mic permission.
5. Grant the `Allow Arbitrary Loads` permission as shown below:
![](https://main.qcloudimg.com/raw/1aebf9111fd95e3e6b6fb4eb08193a26.png)
