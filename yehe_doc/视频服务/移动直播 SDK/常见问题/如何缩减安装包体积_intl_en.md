### How do I reduce the size of an installation package for iOS?

#### Packaging arm64 only (recommended) 

You can package only arm64 into applications for iPhone 5S and later. In Xcode, set **Build Active Architecture Only** to **Yes** and enter `arm64` only for **Valid Architectures**. Packaging only 1 architecture can reduce the amount the SDK adds to an IPA file by half.
![](https://main.qcloudimg.com/raw/e8f7a3d2f5ee4c11df8b3fae4cc1ed31.png)

### How do I reduce the size of an installation package for Android?

#### 1. Packaging only 1 or 2 SO files
If your application is intended for the Chinese mainland, you can package only the SO file for `armeabi-v7a`, in which case the SDK will add 5 MB or less to your installation package. If you want to publish your application on Google Play, then you can package the SO files for `armeabi-v7a` and `arm64-v8a`.

Specifically, you need to add `abiFilters "armeabi-v7a"` in `build.gradle` of your project to package only the `armeabi-v7a` SO file, and `abiFilters "armeabi-v7a", "arm64-v8a"` to package the `armeabi-v7a` and `arm64-v8a` SO files.

- If you do not intend to publish your application on Google Play:
![](https://main.qcloudimg.com/raw/52cc4e459ce5cb922bfc01cf6f2f08ac.png)
- If you want to publish your application on Google Play:
![](https://main.qcloudimg.com/raw/a03cf098ce88a1b69b91f3920fca1ecb.png)


#### 2. Downloading SO files after installation (packaging JAR only)

SO files take up most of the size of the MLVB SDK for Android. Therefore, if you want the SDK to add 1 MB or less to your installation package, you can have SO files downloaded to users’ phones after installation.

- **Step 1. Download the SO files**
At [GitHub](https://github.com/tencentyun/MLVBSDK/tree/master/Android), look for a ZIP file named `LiteAVSDK_x.x.xxx.zip` in the folders and decompress it. Find the SO files for the architectures you want to use.

- **Step 2. Upload the SO files to your server**
Upload the SO files downloaded in Step 1 to your server (or to Tencent Cloud [COS](https://intl.cloud.tencent.com/product/cos)) and note the download URL, such as `http://xxx.com/so_files.zip`.

- **Step 3. Download the SO files at the SDK’s first launch**
Before users use the SDK’s features, for example, to play video, show a loading animation on the UI and tell users that modules are being loaded.

 While users wait, your application can download the SO files from `http://xxx.com/so_files.zip` and save them in the `files` folder of your application’s root directory. Given the possibility of DNS hijacking and file tampering by the carrier, please check the integrity of the SO files after download.

- **Step 4. Use an API to load the SO files**
After the SO files are in place, call the `setLibraryPath()` API in the `TXLiveBase` class (the earliest underlying module of LiteAVSDK), setting the SDK’s library paths to the target paths of the downloaded SO files. The SDK will load the SO files from the paths and enable related features.

>! Do not use this method if you want to publish your application on Google Play.
