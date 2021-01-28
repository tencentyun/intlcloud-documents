
## Overview

To ensure better effects for user videos, Tencent Cloud UGSV worked with YouTu and Pitu to integrate special effects including eye enlarging, face slimming, animated stickers, and green screen into the image processing logic of the RTMP SDK. These are additional features developed for the Enterprise Edition SDK based on the face recognition technology of YouTu Lab and retouching technology of Pitu.

## Accessing the Features
To apply for an Enterprise Edition license, please contact Tencent Cloud sales.

## Downloading the SDK
You can download a compressed package of the Enterprise Edition SDK at [SDK Download](https://intl.cloud.tencent.com/document/product/1069/37914). The package is encrypted. The password for decompression is offered to you along with the license. Decompress the package and you will find `Demo` and `SDK` in the folder. Special effect resources are in `SDK/Resource`.

## Configuring the Xcode Project

For detailed instructions, see [SDK Integration (Xcode)](https://intl.cloud.tencent.com/document/product/1069/38012). 

### Step 1. Add frameworks.

You must add the following frameworks to the Enterprise Edition SDK.
> - AssetsLibrary.framwork
> - CoreMedia.framework
> - Accelerate.framework
> - Metal.framework 

### Step 2. Add linker flag.

1. Go to **Build Setting** > **Other Link Flags**, and add `-ObjC`.
2. If you want to use the AI keying feature, set **Metal API Validation** to `Disabled` in **Product** > **Edit Scheme** > **Run** > **Options**.

### Step 3. Add special effect resources.

Check if animated effect resources have already been added, and add the files in `SDK/Resource` as groups to the project. Below is a list of the files.

> - AECore.metallib
> - FilterEngine.bundle
> - RPNSegmenter.bundle
> - YTHandDetector.bundle
> - detector.bundle
> - e1
> - o1
> - poseest.bundle
> - u1
> - ufa.bundle
> - v1

### Step 4. Import the license file.
You can enable the features in the Enterprise Edition SDK only after license verification. You can apply for a 30-day free license for debugging from Tencent Cloud sales.
Once you have a license, name it **YTFaceSDK.licence** and add it to your project.
>?
>- Each license is bound with a Bundle Identifier. Modifying the Bundle Identifier of your app will result in verification failure.
>- Make sure that the license is named “YTFaceSDK.licence” and do not modify it.
> You do not need to apply for separate licenses for iOS and Android. A license can authorize a bundleid for iOS and Android at the same time.


** Since version 4.9, the SDK has used two-in-one licenses, and `YTFaceSDK.licence` is no longer needed. Just configure the license and corresponding key and URL you obtain from sales in the same way as you configure a license for the Basic Edition.**

## Enabling the Features

### Animated Stickers

#### Example

Each animated effect template is represented by a directory that contains multiple resource files, whose number and size vary with the complexity of the animated effect.

In the sample code, animated effect resources are downloaded and then decompressed to the `Resource` directory. You can find the download links of animated effect resources and their thumbnails in the UGSV code, as shown below.
- `https://st1.xiangji.qq.com/yunmaterials/{name of animated effect}.zip`
- `https://st1.xiangji.qq.com/yunmaterials/{name of animated effect}.png`

>?You are strongly recommended to store animated effect resources on your own servers so that they won’t be affected by changes on the UGSV side.

After decompressing the downloaded files, you can enable the animated effects via the following API.
```objective-c
/**
 * Select an animated effect
 *
 * @param tmplName: name of the animated effect
 * @param tmplDir: directory of the animated effect
 */
- (void)selectMotionTmpl:(NSString *)tmplName inDir:(NSString *)tmplDir;
```

### AI keying

#### Example

You need to download the AI keying resources and enable it using the same API as that for animated effects.
```objective-c
/**
 * Select a keying effect
 *
 * @param tmplName: name of the effect
 * @param tmplDir: directory of the effect
 */
- (void)selectMotionTmpl:(NSString *)tmplName inDir:(NSString *)tmplDir;
```

### APIs for advanced beauty filters (eye enlarging, face slimming, etc)

You can set different beauty filter parameters by obtaining the `TXBeautyManager` object via `getBeautyManager` of `TXUGCRecord`.
<dx-codeblock>
::: objective-c objective-c
/**
 * Select the algorithm used for the skin smoothing filter
 *
 * The SDK has two built-in skin smoothing algorithms. One is "smooth", which features more obvious smoothing effect and is designed for shows.
 The other is "natural", which retains more facial details and is more natural.
 *
 * @param beautyStyle Skin smoothing mode: `smooth` or `natural`. `Smooth` features more obvious smoothing effect and is suitable for shows.
 */
- (void)setBeautyStyle:(TXBeautyStyle)beautyStyle;

/**
 * Set the intensity of the skin smoothing filter.
 * @param level Intensity of the skin smoothing filter. Value range: 0-9. 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
 */
- (void)setBeautyLevel:(float)level;

/**
 * Set the intensity of the skin lightening filter.
 *
 * @param level Intensity of the skin lightening filter. Value range: 0-9. 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
 */
- (void)setWhitenessLevel:(float)level;

/**
 * Set the intensity of the rosy complexion filter.
 *
 * @param level Intensity of the rosy complexion filter. Value range: 0-9. 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
 */
- (void)setRuddyLevel:(float)level;

/**
 Set the intensity of the eye enlarging filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the eye enlarging filter. Value range: 0-9. 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
 */
- (void)setEyeScaleLevel:(float)level;

/**
 * Set the intensity of the face slimming filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the face slimming filter. Value range: 0-9. 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
 */
- (void)setFaceSlimLevel:(float)level

/**
 * Set the intensity of the chin slimming filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the chin slimming filter. Value range: 0-9. 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
 */
- (void)setFaceVLevel:(float)level

/**
 * Set the intensity of the jaw shrinking/expanding filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the jaw shrinking/expanding filter. Value range: -9-9. 0 indicates that the filter is disabled. Values smaller than 0 mean shrinking the jaw, and values larger than 0 mean expanding the jaw.
 */
- (void)setChinLevel:(float)level
/**
 * Set the intensity of the face shortening filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the face shortening filter. Value range: 0-9. 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
 */
- (void)setFaceShortLevel:(float)level

/**
 * Set the intensity of the nose slimming filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the nose slimming filter. Value range: 0-9. 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
 */
- (void)setNoseSlimLevel:(float)level;

/**
 * Set the intensity of the eye brightening filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the eye brightening filter. Value range: 0-9. 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
 */
- (void)setEyeLightenLevel:(float)level

/**
 * Set the intensity of the teeth whitening filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the teeth whitening filter. Value range: 0-9. 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
 */
- (void)setToothWhitenLevel:(float)level

/**
 * Set the intensity of the wrinkle removing filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the wrinkle removing filter. Value range: 0-9. 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
 */
- (void)setWrinkleRemoveLevel:(float)level

/**
 * Set the intensity of the eye bag removing filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the eye bag removing filter. Value range: 0-9. 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
 */
- (void)setPounchRemoveLevel:(float)level

/**
 * Set the intensity of the nasolabial fold removing filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the nasolabial fold removing filter. Value range: 0-9. 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
 */
- (void)setSmileLinesRemoveLevel:(float)level

/**
 * Set the intensity of the hairline filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the hairline filter. Value range: -9-9. 0 indicates that the filter is disabled. Values smaller than 0 mean moving the hairline back, and values larger than 0 mean moving the hairline forward.
 */
- (void)setForeheadLevel:(float)level

/**
 * Set the intensity of the eye distance filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the eye distance filter. Value range: -9-9. 0 indicates that the filter is disabled. Values smaller than 0 mean stretching the distance, and values larger than 0 mean shrinking the distance.
 */
- (void)setEyeDistanceLevel:(float)level

/**
 * Set the intensity of the eye slant filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the eye slant filter. Value range: -9-9. 0 indicates that the filter is disabled. Values smaller than 0 mean lowering the outer corner of the eye, and values larger than mean lifting the corner.
 */
- (void)setEyeAngleLevel:(float)level

/**
 * Set the intensity of the lip contour filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the lip contour filter. Value range: -9-9. 0 indicates that the filter is disabled. Values smaller than 0 mean augmenting the lip, and values larger than mean shrinking the contour.
 */
- (void)setMouthShapeLevel:(float)level

/**
 * Set the intensity of the nose shape filter (valid only in the Enterprise Edition).
 *
 * @param level Intensity of the nose shape filter. Value range: -9-9. 0 indicates that the filter is disabled. Values smaller than 0 mean widening the nose, and values larger than mean narrowing the nose.
 */
- (void)setNoseWingLevel:(float)level

/**
 * Set the intensity of the nose position filter (valid only in the Enterprise Edition).
 * @param level Intensity of the nose position filter. Value range: -9-9. 0 indicates that the filter is disabled. Values smaller than 0 mean moving the nose up, and values larger than 0 mean moving the nose down.
 */
- (void)setNosePositionLevel:(float)level

/**
 * Set the intensity of the lip thickness filter (valid only in the Enterprise Edition).
 * @param level Intensity of the lip thickness filter. Value range: -9-9. 0 indicates that the filter is disabled. Values smaller than 0 mean thickening the lip, and values larger than 0 mean thinning the lip.
 */
- (void)setLipsThicknessLevel:(float)level

/**
 * Set the intensity of the face shape enhancing filter (valid only in the Enterprise Edition).
 * @param level Intensity of the face shape enhancing filter. Value range: 0-9. 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
 */
- (void)setFaceBeautyLevel:(float)level
:::
</dx-codeblock>

### Green Screen

Make sure you have an MP4 file for playback before using the green screen feature. Call the API below to enable the green screen feature.

```objective-c
/**
 * Configure the green screen file.
 * 
 @param file: path of the green screen file (in the MP4 format). nil: disables the green screen feature.
 */
- (void)setGreenScreenFile:(NSURL *)file
```


## Troubleshooting
### 1. What should I do if I fail to compile my project?
Make sure you have added dependent libraries AssetsLibrary.framwork, CoreMedia.framework, Accelerate.framework, and Metal.framework.
                 
### 2. What should I do if the project crashes when I run it?  
1. Make sure that `-ObjC` is configured in your project.  
2. Make sure that `Metal API Validation` is set to `Disabled`.
   
### 3. Why are the animated effects not working?  
1. Check whether you have called the `+[TXUGCBase setLicenceURL:key:]` method and whether the parameters are correct.
2. Call the `getLicenseInfo` method of `TXUGCBase`. Licenses with animated effects enabled should contain the field `pituLicense`.
3. Check whether Pitu resources are added correctly. Note that handdetect, handtrack, and res18_3M must be added as folder references. A simple method to check this is comparing the animated effect files added to your project against those in our demo and see if they are the same.  
4. The SDK downloads licenses to the “Documents” folder of the sandbox. During your development process, you can go to Window > Devices and Simulators to export the license and use this [Query Tool](https://mc.qcloudimg.com/static/archive/9c0f8c02466d08e5ac14c396fad21005/PituDateSearch.zip) to check its validity period.
 The [Query Tool](https://mc.qcloudimg.com/static/archive/9c0f8c02466d08e5ac14c396fad21005/PituDateSearch.zip) is an Xcode project and is only supported on macOS currently. Other query methods will be made available soon.
