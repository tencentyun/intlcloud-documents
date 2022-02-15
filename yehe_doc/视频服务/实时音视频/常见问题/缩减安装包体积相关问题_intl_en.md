### How much will the file increment be after the TRTC SDK is integrated?
The file size increment varies by TRTC SDK version. For more information, please see [SDK Download](https://intl.cloud.tencent.com/document/product/647/34615).

[](id:ios)
### How do I reduce the size of an installation package for iOS?
<dx-tabs>
::: Method 1. Only package the ARM64 architecture (recommended)
 For iPhone models after 5s, you can just package x64 architecture by setting "Build Active Architecture Only" in "Build Settings" in Xcode to "Yes" and write only `arm64` into "Valid Architectures". The single-architecture IPA increment of the TRTC SDK will be 1.9 MB only.
![](https://main.qcloudimg.com/raw/4aea00771567fcff58697bf5433ba0dd.png)
:::
::: Method 2. Enable Bitcode
 For iPhone 5s and older models, **if all third-party libraries in the project support Bitcode,** you can enable Bitcode to reduce the size of the installation package. Toggle on "Enable Bitcode" in "Build Settings" > "Build Options" to enable bitcode.
 ![](https://main.qcloudimg.com/raw/516c0065d97eee4569a1d4061ba019cb.png)
 From 2016 on, Apple started to support Bitcode compilation in the Xcode development environment. After Bitcode is enabled, the compiler will generate the application's intermediate code instead of the actual assembly code, and users will download and install the machine code generated for the specific mobile CPU architecture from App Store, which greatly reduces the installation package size.
:::
</dx-tabs>

[](id:android)
### How do I reduce the size of an installation package for Android?
<dx-tabs>
::: Method 1. Only package certain .so files
 If your application is used in Mainland China only, you can just package the .so files for the `armeabi-v7a` architecture to reduce the increment in the installation package size to below 5 MB. If you want to offer your application on Google Play, you can package the .so files for the `armeabi-v7a` and `arm64-v8a` architectures.
**Directions:** add `abiFilters "armeabi-v7a"` to `build.gradle` of the current project to specify to package the .so files in a single architecture only or add `abiFilters "armeabi-v7a","arm64-v8a"` to specify to package .so files in two architectures.
 - If only .so files in `armeabi-v7a` architecture are packaged (i.e., your application is not offered on Google Play):
  ![](https://main.qcloudimg.com/raw/72065de8f9cd1c95b23fb797d383b527.png)
 - If .so files in `armeabi-v7a` and `arm64-v8a` architectures are packaged (i.e., your application is offered on Google Play):
  ![](https://main.qcloudimg.com/raw/a6dcbef3c71fe9f2f7b5d52d6b0784ae.png)
:::
:::**Method 2. Only package JAR files (i.e., .so files will be downloaded after installation)**
>! If you want to offer your application on Google Play, please do not use this method, as it may cause a failure in offering the application.
 
 The size of .so files takes the greatest proportion of the total size of the SDK for Android. If you want to reduce your installation package to below 1 MB, you can use the method of downloading .so files after installation:
[](id:step1)
 1. In the folder on [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Android), find and download the package named in the format of `LiteAVSDK_TRTC_x.x.xxx.zip`, decompress it, and find the .so files for the specified architecture.
 2. Upload the .so files downloaded in [step 1](#step1) to your server (or Tencent Cloud [COS](https://intl.cloud.tencent.com/product/cos)) and record the download address such as `http://xxx.com/so_files.zip`.
 3. Before an SDK feature such as video playback is started by the user, use a loading animation to prompt the user that the relevant feature module is being loaded.
  When the user is waiting, the application can download the .so files from `http://xxx.com/so_files.zip` and store the files in the application directory (such as the `files` folder in the application's root directory). To ensure that this process is not affected by ISP DNS hijacking, please verify the integrity of the .so files after download to check whether the zip package has been tampered with the ISP.
 4. After all .so files are ready, call the `setLibraryPath()` API in the `TXLiveBase` class (the earliest basic module of `LiteAVSDK`) to set the target paths of the downloaded .so files to the paths in the SDK, so that the SDK can load the required .so files at those paths and start the relevant features.
:::
</dx-tabs>

