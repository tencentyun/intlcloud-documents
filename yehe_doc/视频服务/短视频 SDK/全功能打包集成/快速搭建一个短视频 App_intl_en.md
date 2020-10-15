
## Client

Use XCode or Android Studio to compile and debug client source code of User Generated Short Video (UGSV) by the following three steps.


### Step 1. Download App source code
Find [UGSV source code](https://intl.cloud.tencent.com/document/product/1069/37914#.E5.85.A8.E5.8A.9F.E8.83.BD.E5.B0.8F.E8.A7.86.E9.A2.91-app.EF.BC.88demo.EF.BC.89.E6.BA.90.E4.BB.A3.E7.A0.81) and click “Download”.

### Step 2. Apply for SDK license
Please see [License Application](https://intl.cloud.tencent.com/document/product/1069/38041).

### Step 3. Prepare the debugging environment
**iOS platform** 
- XCode 9 or above
- OS X 10.10 or above

**Android platform**
- Android NDK: android-ndk-r12b
- Android SDK Tools: android-sdk_26.0.2
  - minSdkVersion: 15
  - targetSdkVersion: 21

### Step 4. Compile and run the SDK
Click “Build” button of XCode or Android Studio to compile and run the SDK. As Tencent’s test server address `http://demo.vod2.myqcloud.com/lite/` has been added in the source code, you can quickly run our App in the debugging environment.


## Backend

For more information about the backend, please see [VOD UGSV server](https://github.com/tencentyun/vod-xiaoshipin-server)