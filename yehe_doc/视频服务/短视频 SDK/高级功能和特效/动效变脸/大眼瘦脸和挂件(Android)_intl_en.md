

## Feature Description

Special effects such as eye enlarging, face slimming, animated stickers, and green screen keying are privileged features developed based on the face recognition technology of YouTu Lab and makeup effect technology of Pitu. By collaborating with YouTu and Pitu teams, the UGSV team deeply integrated such special effects into the video image processing process of the UGSV SDK to deliver better video special effects.

## Connection Process

Contact your sales rep to apply for an enterprise license.

## Download

Download the Enterprise Edition SDK package at the bottom of the [SDK Download](https://intl.cloud.tencent.com/document/product/1071/38150) page. The package is encrypted, and you can get the decryption password and license file from your Tencent Cloud rep. After the package is successfully decompressed, a `.aar` file and a `.zip` file will be extracted in the SDK directory, which can be used in two integration methods, respectively.

## Project Settings

For more information, please see [Project Configuration](https://intl.cloud.tencent.com/document/product/1069/38018). 

### Adding SDK

#### Integrating by using .aar file

Directly replace the non-Enterprise Edition .aar file in the project and modify the corresponding name in `build.gradle` in the `app` directory.

#### Integrating by using .jar package

1. You need to decompress the .zip file and copy the .so files in `libs` to your JNI load path. The following are the .so files related to animated effects:

| so                        |                      |                           |
| ------------------------- | -------------------- | ------------------------- |
| libYTCommon.so            | libnnpack.so         | libpitu_device.so         |
| libpitu_tools.so          | libWXVoice.so        | libgameplay.so            |
| libCameraFaceJNI.so       | libYTFaceTrackPro.so | libimage_filter_gpu.so    |
| libimage_filter_common.so | libpitu_voice.so     | libvoicechanger_shared.so | 
| libParticleSystem.so      | libYTHandDetector.so | libGestureDetectJni.so    |
| libsegmentern.so          |||

2. Copy all resources in the `assets` folder after decompression to the `assets` directory in the project, including the files in the `assets` root directory and the `camera` folder.

### Importing license file

The features of Enterprise Edition can take effect only after the license is successfully verified. You can apply for a debugging license with 30-day validity free of charge to your Tencent Cloud rep.
After getting the license, you need to name it **`YTFaceSDK.licence`** and place it in the `assets` directory.
>!
>- Each license has been bound to a specific `package name`. If you modify the application's `package name`, the verification will fail.
>- The filename of `YTFaceSDK.licence` is fixed and should not be modified. The file must be placed in the `assets` directory.
>- You do not need to apply for two licenses for iOS and Android respectively. A license can authorize both an iOS `bundleid` and an Android `packageName`.


**From v4.9 on, the SDK supports two-in-one license. In this way, `YTFaceSDK.licence` is no longer needed; instead, you can get the corresponding `key` and `url` of the license from your Tencent Cloud rep and set the license information in the same way as for Basic Edition.**

## Feature Call

### 1. Animated effect feature

#### Sample code

<img src="https://mc.qcloudimg.com/static/img/a320624ee8d3a82ee07feb05969e5290/A8B81CB6-DBD3-4111-9BF0-90BD02779BFC.png" width="450">

An animated effect template is a directory that contains many resource files. As animated effects have different complexity, the number of directories and file size vary by effect.
The sample code in the demo downloads the animated effect resources from the backend and extracts them all onto the SD card. You can find the download addresses of the animated effect resources in the following format in the demo code:

```
http://dldir1.qq.com/hudongzhibo/AISpecial/Android/156/(animated effect name).zip
```

>?We recommend you place the animated effect resources on your own server, so as to avoid any impacts caused by change of the demo.

After the decompression, you can call the following API to enable the animated effect:
```
/**
 * setMotionTmpl   Set the location of the animated sticker file
 * @param tmplPath
 */
public void setMotionTmpl(String tmplPath);
```

### 2. AI-based keying

#### Sample code

<img src="https://mc.qcloudimg.com/static/img/0f79b78687753f88af7685530745a8d4/98B403B8-1DEC-4130-B691-D9EB5E321162.png" width="450">

You need to download the AI-based keying resources. The API is the same as that for the animated effect.

```
/**
 * setMotionTmpl   Set the location of the animated sticker file
 * @param tmplPath
 */
public void setMotionTmpl(String tmplPath);
```

### 3. Advanced beauty filter APIs (eye enlarging, face slimming, etc.)

```
// Eye enlarging effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setEyeScaleLevel(eyeLevel);
// Face slimming effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setFaceSlimLevel(faceSlimLevel);
// Chin slimming effect level. Value range: 0–9
 mTXCameraRecord.getBeautyManager().setFaceVLevel(faceVLevel);
// Chin lengthening/shortening effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setChinLevel(chinSlimLevel);
// Face shortening effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setFaceShortLevel(faceShortLevel);
// Nose slimming effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setNoseSlimLevel(noseScaleLevel);
// Eye brightening effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setEyeLightenLevel(eyeLightenLevel);
// Teeth whitening effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setToothWhitenLevel(toothWhitenLevel);
// Wrinkle removal effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setWrinkleRemoveLevel(wrinkleRemoveLevel);
// Eye bag removal effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setPounchRemoveLevel(pounchRemoveLevel);
// Smile line removal effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setSmileLinesRemoveLevel(smileLinesRemoveLevel);
// Hairline adjustment effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setForeheadLevel(foreheadLevel);
// Eye distance adjustment effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setEyeDistanceLevel(eyeDistanceLevel);
// Eye corner adjustment effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setEyeAngleLevel(eyeAngleLevel);
// Mouth shape adjustment effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setMouthShapeLevel(mouthShapeLevel);
// Nose wing adjustment effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setNoseWingLevel(noseWingLevel);
// Nose position adjustment effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setNosePositionLevel(nosePositionLevel);
// Lip thickness adjustment effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setLipsThicknessLevel(lipsThicknessLevel);
// Face shape adjustment effect level. Value range: 0–9
mTXCameraRecord.getBeautyManager().setFaceBeautyLevel(faceBeautyLevel);
```

### 4. Green screen keying

To use green screen keying, you need to prepare a .mp4 file for playback first and then call the following API to enable green screen keying:

```
/**
 * Set the green screen keying file. It can be in formats supported by Android, such as .jpg and .png for images and .mp4 and .3gp for videos
 * The API version needs to be 18
 * @param path: green screen keying file location, which can be set in two ways:
 *             1. Place the resource file in the `assets` directory and directly set `path` to the filename
 *             2. Set `path` to the absolute path of the file
 */
@TargetApi(18)
public void setGreenScreenFile(String path);
```

## Troubleshooting              
### 1. Is the license being used normally?
After the license is successfully set (you need to wait for a period of time, subject to the network conditions), the SDK will download the license file to the phone. You can use the `getLicenceInfo()` method of `TXUGCBase` to view the license information, including the license effective time and expiration time and bound application package name.

```java
public void onCreate() {
      super.onCreate();
      String licenceURL = ""; // Obtained `licenceURL`
      String licenceKey = ""; // Obtained `licenceKey`
      TXUGCBase.getInstance().setLicence(this, licenceURL, licenceKey);// Set the license
      
      // Print the license information
      Handler handler = new Handler(Looper.getMainLooper());
      handler.postDelayed(new Runnable() {
          @Override
          public void run() {
              Log.i(TAG, "onCreate: " + TXUGCBase.getInstance().getLicenceInfo(MApplication.this));
          }
      }, 5 * 1000);// Print the license information after 5 seconds
  }

```

If you need further assistance, please save the printed license information and contact our [technical support](https://intl.cloud.tencent.com/support).

### 2. How do I fix an integration exception?
```
java.lang.UnsatisfiedLinkError: No implementation found for void com.tencent.ttpic.util.youtu.YTFaceDetectorBase.nativeSetRefine(boolean) (tried Java_com_tencent_ttpic_util_youtu_YTFaceDetectorBase_nativeSetRefine and Java_com_tencent_ttpic_util_youtu_YTFaceDetectorBase_nativeSetRefine__Z)
        at com.tencent.ttpic.util.youtu.YTFaceDetectorBase.nativeSetRefine(Native Method)
```

Please check whether the project's `build.gradle` has hierarchical module structure; for example, the `app` module imports the `ugckit` module, which imports the Tencent Cloud SDK. In this case, you need to add the following configuration to the `app` module and `ugckit` module:

```
packagingOptions {
        pickFirst '**/libc++_shared.so'
        doNotStrip "*/armeabi/libYTCommon.so"
        doNotStrip "*/armeabi-v7a/libYTCommon.so"
        doNotStrip "*/x86/libYTCommon.so"
        doNotStrip "*/arm64-v8a/libYTCommon.so"
}
```

After adding the configuration, please clean the project and built it again.

### 3. What should I do if features such as beauty filters (eye enlarging, face slimming, etc.) and animated effects do not take effect?
- Check the validity period of the UGSV license: `TXUGCBase.getInstance().getLicenceInfo(mContext)`.
- Check the validity period of the YouTu Lab license (obtained from your Tencent Cloud rep during purchase).
- Check whether the editions of the downloaded SDK and purchased SDK are the same.

Only the Enterprise Edition of UGSV supports AI-based special effects (such as eye enlarging, face slimming, chin slimming, and nose reshaping filters, animated stickers, and green screen keying).

If a called API does not take effect, please check whether the log `support EnterPrise above!!!` exists in Logcat, and if so, the downloaded SDK edition does not match the edition of the currently used license.
>!Please use the latest API `TXUGCRecord getBeautyManager()` for beauty filter effects.

The [query tool](https://mc.qcloudimg.com/static/archive/9c0f8c02466d08e5ac14c396fad21005/PituDateSearch.zip) is an Xcode project used to query the license validity period and is currently supported for macOS only. More query methods will be provided in the future.

### 4. What should I pay attention to when dynamically loading .jar and .so files?

- Check the number of dynamically distributed .so packages to confirm whether all required packages are in place. You can use `TXLiveBase.setLibraryPath(soPath);` to set the .so package address.
>!The files must be either dynamically distributed or locally integrated as a whole. You cannot store some of them locally and dynamically distribute other ones.
- Resources extracted from .jar and .so files can be categorized into `assets-static` and `assets-dynamic` resources. `assets-static` resources can only be stored locally and cannot be dynamically distributed, while `asset-dynamic` resources need to be dynamically distributed and stored in the same directory as the .so files.
- In the SDK 6.8 or above, please do not manually load .so packages in the system method, as the SDK will arrange their load sequence internally.

If the following exception occurs, please troubleshoot as detailed above:

```
YTFaceDetectorBase: (GLThread 5316)
com.tencent.ttpic.util.youtu.YTFaceDetectorBase(54)[c]: nativeInitCommon, ret = -2
YTFaceDetectorBase: (GLThread 5316)com.tencent.ttpic.util.youtu.YTFaceDetectorBase(57)[c]: nativeInitCommon failed, ret = -1001
YTFaceDetectorBase: (GLThread 5316)com.tencent.ttpic.util.youtu.YTFaceDetectorBase(26)[a]: initCommon, ret = -1001
YTFaceDetectorBase: (GLThread 5316)com.tencent.ttpic.util.youtu.YTFaceDetectorBase(28)[a]: initCommon failed, ret = -1001
```
