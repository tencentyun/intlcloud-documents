

## Overview

To ensure better effects for user videos, Tencent Cloud UGSV worked with YouTu and Pitu to integrate special effects including eye enlarging, face slimming, animated stickers, and green screen into the image processing logic of the RTMP SDK. These are additional features developed for the Enterprise Edition SDK based on the face recognition technology of YouTu Lab and retouching technology of Pitu.

## Accessing the features

To apply for an Enterprise Edition license, please contact Tencent Cloud sales.

## Downloading the SDK

You can download a compressed package of the Enterprise Edition SDK at [SDK Download](https://intl.cloud.tencent.com/document/product/1069/37914). The package is encrypted. Contact Tencent Cloud sales for a license file and the password. Decompress the package and you will find `aar` and `zip` in the folder, which are for two different integration methods.

## Configuring the Project

For detailed instructions, see [SDK Integration (with Android Studio)](https://intl.cloud.tencent.com/document/product/1069/38018). 

#### Integrating the SDK

#### Integrating via aar

Replace the existing aar file in your project with the one in the Enterprise Edition SDK, and modify the name in `build.gradle` in the folder of the app.

#### Integrating using jar files

1. Decompress `zip`, and copy the so files in `libs` to your loading path for JNI. The so files associated with animated effects are listed below.

| so                        |                      |                           |
| ------------------------- | -------------------- | ------------------------- |
| libYTCommon.so            | libnnpack.so         | libpitu_device.so         |
| libpitu_tools.so          | libWXVoice.so        | libgameplay.so            |
| libCameraFaceJNI.so       | libYTFaceTrackPro.so | libimage_filter_gpu.so    |
| libimage_filter_common.so | libpitu_voice.so     | libvoicechanger_shared.so |
| libParticleSystem.so      | libYTHandDetector.so | libGestureDetectJni.so    |
| libsegmentern.so          |||

2. Copy all the resources in the `assets` folder, including the files in the root folder and the `camera` folder, to your project's `assets` folder.

### Importing the license file

You can enable the features in the Enterprise Edition SDK only after license verification. You can apply for a 30-day free license for debugging from Tencent Cloud sales.
Once you have a license, name it **YTFaceSDK.licence** and place it in the `assets` folder of your project.
>!
>- Each license is bound with a package name. Modifying the package name of your app will result in verification failure.
>- You cannot rename the license and must place it in the `assets` folder.
>- You do not need to apply for separate licenses for iOS and Android. A license can authorize a bundleid for iOS and Android at the same time.


** Since version 4.9, the SDK has used two-in-one licenses, and `YTFaceSDK.licence` is no longer needed. Just configure the license and corresponding key and URL you obtain from sales in the same way as you configure a license for the Basic Edition.**

## Enabling the Features

### 1. Animated effects

#### Example



Each animated effect template is represented by a directory that contains multiple resource files, whose number and size vary with the complexity of the animated effect.
In the sample code of the demo, animated effect resources are downloaded and then decompressed to the `sdcard` folder. You can find the download links of animated effect resources in the demo code, as shown below.

```
http://dldir1.qq.com/hudongzhibo/AISpecial/Android/156/(name of animated effect).zip
```

>?You are strongly recommended to store animated effect resources on your own servers so that they won’t be affected by changes to the demo.

After decompressing the downloaded files, you can enable the animated effects via the following API.
```
/**
 * setMotionTmpl Set the path for animated effect images.
 * @param tmplPath
 */
public void setMotionTmpl(String tmplPath);
```

### 2. AI keying

#### Example



You need to download the AI keying resources and enable it using the same API as that for animated effects.

```
/**
 * setMotionTmpl Set the path for animated effect pictures.
 * @param tmplPath
 */
public void setMotionTmpl(String tmplPath);
```

### 3. APIs for advanced beauty filters (eye enlarging, face slimming, etc)

```
// Enlarge the eyes. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setEyeScaleLevel(eyeLevel);
// Slim the face. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setFaceSlimLevel(faceSlimLevel);
// Give the face a V-shaped jawline. Value range: 0-9.
 mTXCameraRecord.getBeautyManager().setFaceVLevel(faceVLevel);
// Expand or shrink the jaw. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setChinLevel(chinSlimLevel);
// Shorten the face. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setFaceShortLevel(faceShortLevel);
// Narrow the nose. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setNoseSlimLevel(noseScaleLevel);
// Lighten the eyes. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setEyeLightenLevel(eyeLightenLevel);
// Whiten the teeth. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setToothWhitenLevel(toothWhitenLevel);
// Remove wrinkles. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setWrinkleRemoveLevel(wrinkleRemoveLevel);
// Remove eye bags. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setPounchRemoveLevel(pounchRemoveLevel);
// Remove nasolabial folds. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setSmileLinesRemoveLevel(smileLinesRemoveLevel);
// Adjust the hairline. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setForeheadLevel(foreheadLevel);
// Adjust the distance between the eyes. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setEyeDistanceLevel(eyeDistanceLevel);
// Adjust the eye corners. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setEyeAngleLevel(eyeAngleLevel);
// Reshape the lips. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setMouthShapeLevel(mouthShapeLevel);
// Reshape the nose. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setNoseWingLevel(noseWingLevel);
// Adjust the position of the nose. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setNosePositionLevel(nosePositionLevel);
// Adjust the thickness of the lips. Value range: 0-9/
mTXCameraRecord.getBeautyManager().setLipsThicknessLevel(lipsThicknessLevel);
// Reshape the face. Value range: 0-9.
mTXCameraRecord.getBeautyManager().setFaceBeautyLevel(faceBeautyLevel);
```

### 4. Green screen

Make sure you have an MP4 file for playback before using the green screen feature. Call the API below to enable the green screen feature.

```
/**
 * Configure the green screen file, which should be in formats supported by Android, including images in JPG or PNG and videos in MP4 or 3GP.
 * API (level 18)
 @param path: the path of the green screen file, which can be set via two methods.
 *             1. Place the resource file in the `assets` folder, and set the path parameter to the name of the file.
 *             2. Set the path parameter to the absolute path of the file.
 */
@TargetApi(18)
public void setGreenScreenFile(String path);
```

## Troubleshooting              
### 1. Is my license working?
After license configuration, the SDK will download the license file to the phone. This may take a while. The exact time needed depends on network conditions. You can view your license information, including when it takes effect and expires, as well as the app package name bound, via `getLicenceInfo()` of `TXUGCBase`.

```java
public void onCreate() {
      super.onCreate();
      String licenceURL = ""; // The license URL obtained
      String licenceKey = ""; // The license key obtained
      TXUGCBase.getInstance().setLicence(this, licenceURL, licenceKey);// Configure the license.
      
      // Print license information.
      Handler handler = new Handler(Looper.getMainLooper());
      handler.postDelayed(new Runnable() {
          @Override
          public void run() {
              Log.i(TAG, "onCreate: " + TXUGCBase.getInstance().getLicenceInfo(MApplication.this));
          }
      }, 5 * 1000);// Print license information in 5 seconds.
  }

```

If you need help, please save the printed license information and contact [Technical Support](https://intl.cloud.tencent.com/support).

### 2. What should I do if the following error occurs when I try to integrate the SDK?
```
java.lang.UnsatisfiedLinkError: No implementation found for void com.tencent.ttpic.util.youtu.YTFaceDetectorBase.nativeSetRefine(boolean) (tried Java_com_tencent_ttpic_util_youtu_YTFaceDetectorBase_nativeSetRefine and Java_com_tencent_ttpic_util_youtu_YTFaceDetectorBase_nativeSetRefine__Z)
        at com.tencent.ttpic.util.youtu.YTFaceDetectorBase.nativeSetRefine(Native Method)
```

Please check if the module structure in `build.gradle` of your project has multiple layers. For example, if the app module references the ugckit module, and the ugckit module references the Tencent Cloud SDK, you need to add the following configuration to the app and ugckit modules.

```
packagingOptions {
        pickFirst '**/libc++_shared.so'
        doNotStrip "*/armeabi/libYTCommon.so"
        doNotStrip "*/armeabi-v7a/libYTCommon.so"
        doNotStrip "*/x86/libYTCommon.so"
        doNotStrip "*/arm64-v8a/libYTCommon.so"
}
```

After the configuration, clean your project and build it again.

### 3. What should I do if beauty filters (e.g. eye enlarging and face slimming) and animated effects do no work?
- Check the validity of your UGSV license via `TXUGCBase.getInstance().getLicenceInfo(mContext)`.
- Check the validity of your YouTu license (obtained from Tencent Cloud sales when you purchase the SDK license).
- Check if the edition of the SDK you downloaded is the same as the edition of the license you purchased.

Only the Enterprise Edition SDK supports the use of AI special effects (eye enlarging, V-shaped jawline, nose augmentation, animated stickers, and green screen keying).

If you fail to call the APIs, check for `support EnterPrise above!!!` in the log via Logcat. The message indicates mismatch between the edition of the SDK you are using and the license you purchased.
>! Please use the newest API `TXUGCRecord getBeautyManager()` to enable beauty filters and animated effects.

The [Query Tool](https://mc.qcloudimg.com/static/archive/9c0f8c02466d08e5ac14c396fad21005/PituDateSearch.zip) can be used to query license validity. It is an Xcode project and is only supported on macOS currently. Other query methods will be made available soon.

### 4. What should I pay attention to when I integrate the SDK by dynamically loading the jar and so files?

- Check if you have distributed all the so files. Set the path of the so files via `TXLiveBase.setLibraryPath(soPath);`.
>! You can not dynamically distribute some of the so files and store the others locally. Either locally store or dynamically distribute them all.
- In the jar + so loading method, the decompressed resources fall under two categories: `assets-static` and `assets-dynamic`. `assets-static` resources must be stored locally, and `asset-dynamic` resources must be dynamically distributed to the same directory of the so files.
- If you use SDK 6.8 or above, please do not manually load the so files via the system. The SDK will make sure that the so files are loaded in the correct order.

Check the above if you run into one of the following errors.

```
YTFaceDetectorBase: (GLThread 5316)
com.tencent.ttpic.util.youtu.YTFaceDetectorBase(54)[c]: nativeInitCommon, ret = -2
YTFaceDetectorBase: (GLThread 5316)com.tencent.ttpic.util.youtu.YTFaceDetectorBase(57)[c]: nativeInitCommon failed, ret = -1001
YTFaceDetectorBase: (GLThread 5316)com.tencent.ttpic.util.youtu.YTFaceDetectorBase(26)[a]: initCommon, ret = -1001
YTFaceDetectorBase: (GLThread 5316)com.tencent.ttpic.util.youtu.YTFaceDetectorBase(28)[a]: initCommon failed, ret = -1001
```
