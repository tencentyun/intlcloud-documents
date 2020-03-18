## iOS Platform

### 1. Packaging of arm64 Architecture Only (Recommended)

Apple iPhone 5s and later can all support the packaging of arm64 architecture only. Set the Build Active Architecture Only setting in XCode’s Build Settings to YES. Also set it to only write arm64 in Valid Architectures. The single-architecture .ipa for TRTC SDK is delta compressed to only 1.9 MB.
![](https://main.qcloudimg.com/raw/4aea00771567fcff58697bf5433ba0dd.png)
If you do not wish to give up using an early model like the iPhone 5s, you can consider enabling BitCode to solve the problem.

### 2. Enabling BitCode

Apple has supported the BitCode compilation option in its XCode development environment since 2016. After enabling BitCode, the compiler will generate intermediate code for the application instead of the actual assembly machine code. What the user downloads and installs from the App Store is machine code generated for the CPU architecture of the specific phone. Therefore, this method can greatly reduce installation package size.

- **How do I enable the feature?**
Turn on the Enable BitCode option under Build Settings => Build Options to enable BitCode.
![](https://main.qcloudimg.com/raw/516c0065d97eee4569a1d4061ba019cb.png)
- **What if there is a compilation problem?**
The prerequisite for successfully enabling BitCode is that the third-party libraries in your project must all support BitCode. As long as there is one that does not support it, a compilation error will be reported. Therefore, we strongly recommend that you use the method of packaging arm64 architecture only to reduce installation package size.

## Android Platform

### 1. Packaging of Some .sos Only
If your application is only used in the mainland China region, you can package the .so file with `armeabi-v7a` only. Such an installation package is delta compressed to within 5M. If your application is to be listed on Google Play, you can package the .so file with the two architectures of `armeabi-v7a` and `arm64-v8a`. 

The specific method of its operation is to add `abiFilters "armeabi-v7a"` to the current project’s build.gradle to specify the packaging of a single-architecture .so file or to add `abiFilters "armeabi-v7a", "arm64-v8a"` to specify the packaging of a dual-architecture .so file.

- If you do not plan for it to be listed on Google Play:
![](https://main.qcloudimg.com/raw/72065de8f9cd1c95b23fb797d383b527.png)
- If you do plan for it to be listed on Google Play:
![](https://main.qcloudimg.com/raw/a6dcbef3c71fe9f2f7b5d52d6b0784ae.png)


### 2. Downloading .so After Installation (Packaging JAR Only)

The size of SDK on Android mainly comes from the .so files, and if you wish to delta compress the installation package to within 1M, you can consider using the method of downloading the .so files after installation:

- **Step 1: download the .so file for the specified architecture**
Look for a compressed file with a name like `LiteAVSDK_TRTC_x.x.xxx.zip` under the [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Android) folder and decompress it. Then look for the .so file for the specified architecture.

- **Step 2: upload the .so file to the server**
Upload the .so file downloaded in Step 1 to your server (or to the Tencent Cloud [COS](https://intl.cloud.tencent.com/product/cos) cloud object storage service) and record the download location, such as `http://xxx.com/so_files.zip`.

- **Step 3: download the .so file before starting SDK for the first time**
Before playing videos or using other SDK features, you are prompted with a loading animation indicating "Loading relevant features".

 During the loading process, the application downloads .so files from `http://xxx.com/so_files.zip` and saves them in the application directory, such as the Files folder under the application's root directory. To ensure that this process is not affected by the ISP's DNS hijacking, check the integrity of the .so files after downloading, thus preventing the .zip files from being tampered with by the ISP.

- **Step 4: use API to load .so files**
After waiting for all .so files to be in place, call the `setLibraryPath()` API that is the `TXLiveBase` class (LiteAVSDK’s earliest basic module) and set the target path of the downloaded .so files as SDK. After that, SDK will load the required .so files under these paths and enable the related features.

> Do not use this method if your application is intended to be listed on Google Play because it could cause it to fail to be listed.
