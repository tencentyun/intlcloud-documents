This document describes how to quickly integrate the IM SDK for Unity to your projects. To configure and integrate the SDK, follow these steps.

## Method 1: UPM-Based Integration (Recommended)
1. Find the `manifest.json` file:
![img](https://qcloudimg.tencent-cloud.cn/raw/4ea52e320700dc37770a5405ac14d1a7.jpg)

2. Modify it as follows:
```json
{
    "dependencies":{
    "com.tencent.imsdk.unity":"1.6.4" // Set to the latest version. To get all versions, visit https://www.npmjs.com/package/com.tencent.imsdk.unity.
  },
  "registry": "https://registry.npmjs.org"
}
```

3. Open the project in the Unity Editor, wait until dependencies are loaded, and confirm the Tencent Cloud IM is successfully loaded.
![img](https://qcloudimg.tencent-cloud.cn/raw/d98dfb17bbee6c0319e370de6f2ba9dd.jpg)

4. Perform a test: [Download the test script](https://imgcache.qq.com/operation/dianshi/other/Demo.1fdc6bd474aa3d12f0f3061155d4a5accdf30c7b.zip), decompress the file, import the decompressed file to the project, and bind TestApi.cs to any scenario.
![img](https://qcloudimg.tencent-cloud.cn/raw/b4d770775523fdd76b75f1d80f07c925.jpg)
![img](https://qcloudimg.tencent-cloud.cn/raw/940da8044cd80db27d08a7b0dff45b94.png)

## Method 2: Unity Package Integration

1. Download [Unity package](https://comm.qq.com/im/sdk/unity_plus/im_unity_sdk_plus_v1.6.0.unitypackage).
2. Select **Assets** > **Import Package** to add the downloaded Unity package to the project.
