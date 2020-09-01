
## Feature Description

Special effects such as eye enlarging, face slimming, animated stickers, and green screen keying are privileged features developed based on the face recognition technology of YouTu Lab and makeup effect technology of Pitu. By collaborating with YouTu and Pitu teams, the UGSV team deeply integrated such special effects into the video image processing process of the UGSV SDK to deliver better video special effects.

## Connection Process
Contact your sales rep to apply for an enterprise license.

## Download
Download the Enterprise Edition SDK package at the bottom of the [SDK Download](https://intl.cloud.tencent.com/document/product/1069/37914) page. The package is encrypted, and you can get the decryption password and license file in the applicable connection step. After the package is successfully decompressed, `Demo` and `SDK` folders will be extracted, and the special effect resources are stored in `SDK/Resource`.

## Xcode Project Settings

For more information, please see [Project Configuration](https://intl.cloud.tencent.com/document/product/1069/38012). 

### 1. Add frameworks

The Enterprise Edition needs to link to the following frameworks:
> - AssetsLibrary.framwork
> - CoreMedia.framework
> - Accelerate.framework
> - Metal.framework 

### 2. Add link parameters

> 1. In "Build Settings" > "Other Link Flags" of the project, add the `-ObjC` option.
> 2. If you use the AI-based keying feature, you need to select "Product" > "Edit Scheme" > "Run" > "Options" and set "Metal API Validation" to "Disabled".

### 3. Add animated effect resources

Please check whether the animated effect resources are added: add files in `SDK/Resource` to the project as groups. The following is the list of files:

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

### 4. Import the license file
The features of Enterprise Edition can take effect only after the license is successfully verified. You can apply for a debugging license with 30-day validity free of charge to your Tencent Cloud rep.
After getting the license, you need to name it **`YTFaceSDK.licence`** and add it to the project as shown above.
>?
>- Each license has been bound to a specific `Bundle Identifier`. If you modify the application's `Bundle Identifier`, the verification will fail.
>- The filename of `YTFaceSDK.licence` is fixed and should not be modified.
>- You do not need to apply for two licenses for iOS and Android respectively. A license can authorize both an iOS `bundleid` and an Android `packageName`.


**From v4.9 on, the SDK supports two-in-one license. In this way, `YTFaceSDK.licence` is no longer needed; instead, you can get the corresponding `key` and `url` of the license from your Tencent Cloud rep and set the license information in the same way as for Basic Edition.**

## Feature Call

### 1. Animated sticker

#### Sample code

<img src="https://mc.qcloudimg.com/static/img/a320624ee8d3a82ee07feb05969e5290/A8B81CB6-DBD3-4111-9BF0-90BD02779BFC.png" width="450">

An animated effect template is a directory that contains many resource files. As animated effects have different complexity, the number of directories and file size vary by effect.

The sample code in the UGSV application demo downloads the animated effect resources from the backend and extracts them all into the `Resource` directory. You can find the download addresses of the animated effect resources and animated effect thumbnails in the following format in the UGSV application demo code:

> `https://st1.xiangji.qq.com/yunmaterials/{animated effect name}.zip`
> `https://st1.xiangji.qq.com/yunmaterials/{animated effect name}.png`

>?We recommend you place the animated effect resources on your own server, so as to avoid any impacts caused by change of the UGSV application demo.

After the decompression, you can call the following API to enable the animated effect:

```objective-c
/**
 * Select an animated effect
 *
 * @param tmplName: animated effect name
 * @param tmplDir: animated effect directory
 */
- (void)selectMotionTmpl:(NSString *)tmplName inDir:(NSString *)tmplDir;
```
### 2. AI-based keying

#### Sample code

<img src="https://mc.qcloudimg.com/static/img/0f79b78687753f88af7685530745a8d4/98B403B8-1DEC-4130-B691-D9EB5E321162.png" width="450">

You need to download the AI-based keying resources. The API is the same as that for the animated effect.

```objective-c
/**
 * Select the keying special effect
 *
 * @param tmplName: animated effect name
 * @param tmplDir: animated effect directory
 */
- (void)selectMotionTmpl:(NSString *)tmplName inDir:(NSString *)tmplDir;
```

### 3. Advanced beauty filter APIs (eye enlarging, face slimming, etc.)

You can use the `getBeautyManager` method of `TXUGCRecord` to get the `TXBeautyManager` object and set beauty filter parameters as follows:

```objective-c
/**
 * Set the beauty (skin smoothing) filter algorithm
 *
 * The SDK is integrated with two skin smoothing algorithms of different styles. One is called "smooth" and is suitable for shows as its effect is more obvious.
 * The other is called "natural", which retains more facial details and seems more natural subjectively.
 *
 * @param beautyStyle   Beauty filter style: smooth or natural. The smooth style has more obvious skin smoothing effect and is suitable for entertaining scenarios.
 */
- (void)setBeautyStyle:(TXBeautyStyle)beautyStyle;

/**
 * Set the effect level of the beauty filter
 * @param level   Effect level of the beauty filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
 */
- (void)setBeautyLevel:(float)level;

/**
 * Set the effect level of the brightening filter
 *
 * @param level   Effect level of the brightening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
 */
- (void)setWhitenessLevel:(float)level;

/**
 * Set the effect level of the rosy skin filter
 *
 * @param level   Effect level of the rosy skin filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
 */
- (void)setRuddyLevel:(float)level;

/**
 * Set the effect level of the eye enlarging filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the eye enlarging filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
 */
- (void)setEyeScaleLevel:(float)level;

/**
 * Set the effect level of the face slimming filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the face slimming filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
 */
- (void)setFaceSlimLevel:(float)level;

/**
 * Set the effect level of the chin slimming filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the chin slimming filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
 */
- (void)setFaceVLevel:(float)level;

/**
 * Set the effect level of the chin lengthening/shortening filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the chin lengthening/shortening filter. Value range: -9–9; 0 indicates that the filter is disabled, a value smaller than 0 indicates that the chin is shortened, while a value greater than 0 indicates that the chin is lengthened.
 */
- (void)setChinLevel:(float)level;
/**
 * Set the effect level of the face shortening filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the face shortening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
 */
- (void)setFaceShortLevel:(float)level;

/**
 * Set the effect level of the nose slimming filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the nose slimming filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
 */
- (void)setNoseSlimLevel:(float)level;

/**
 * Set the effect level of the eye brightening filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the eye brightening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
 */
- (void)setEyeLightenLevel:(float)level;

/**
 * Set the effect level of the teeth whitening filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the teeth whitening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
 */
- (void)setToothWhitenLevel:(float)level;

/**
 * Set the effect level of the wrinkle removal filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the wrinkle removal filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
 */
- (void)setWrinkleRemoveLevel:(float)level;

/**
 * Set the effect level of the eye bag removal filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the eye bag removal filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
 */
- (void)setPounchRemoveLevel:(float)level;

/**
 * Set the effect level of the smile line removal filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the smile line removal filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
 */
- (void)setSmileLinesRemoveLevel:(float)level;

/**
 * Set the effect level of the hairline adjustment filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the hairline adjustment filter. Value range: -9–9; 0 indicates that the filter is disabled, a value smaller than 0 indicates to lift, while a value greater than 0 indicates to lower.
 */
- (void)setForeheadLevel:(float)level;

/**
 * Set the effect level of the eye distance adjustment filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the eye distance adjustment filter. Value range: -9–9; 0 indicates that the filter is disabled, a value smaller than 0 indicates to widen, while a value greater than 0 indicates to narrow.
 */
- (void)setEyeDistanceLevel:(float)level;

/**
 * Set the effect level of the eye corner adjustment filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the eye corner adjustment filter. Value range: -9–9; 0 indicates that the filter is disabled, a value smaller than 0 indicates to lower, while a value greater than 0 indicates to lift.
 */
- (void)setEyeAngleLevel:(float)level;

/**
 * Set the effect level of the mouth shape adjustment filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the mouth shape adjustment filter. Value range: -9–9; 0 indicates that the filter is disabled, a value smaller than 0 indicates to widen, while a value greater than 0 indicates to narrow.
 */
- (void)setMouthShapeLevel:(float)level;

/**
 * Set the effect level of the nose wing adjustment filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 *
 * @param level   Effect level of the nose wing adjustment filter. Value range: -9–9; 0 indicates that the filter is disabled, a value smaller than 0 indicates to widen, while a value greater than 0 indicates to narrow.
 */
- (void)setNoseWingLevel:(float)level;

/**
 * Set the effect level of the nose position adjustment filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 * @param level   Effect level of the nose position adjustment filter. Value range: -9–9; 0 indicates that the filter is disabled, a value smaller than 0 indicates to lift, while a value greater than 0 indicates to lower.
 */
- (void)setNosePositionLevel:(float)level;

/**
 * Set the effect level of the lip thickness adjustment filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 * @param level   Effect level of the lip thickness adjustment filter. Value range: -9–9; 0 indicates that the filter is disabled, a value smaller than 0 indicates to thicken, while a value greater than 0 indicates to thin.
 */
- (void)setLipsThicknessLevel:(float)level;

/**
 * Set the effect level of the face shape adjustment filter (it takes effect only in Enterprise Edition and is invalid in other editions)
 * @param level   Effect level of the face shape adjustment filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
 */
- (void)setFaceBeautyLevel:(float)level;
```

### 4. Green screen keying

To use green screen keying, you need to prepare a .mp4 file for playback first and then call the following API to enable green screen keying:

```objective-c
/**
 * Set the green screen keying file
 * 
 * @param file: path of green screen keying file. .mp4 files are supported. `nil` indicates to disable green screen keying
 */
-(void)setGreenScreenFile:(NSURL *)file;
```
## Troubleshooting
### 1. Why does the project fail to be compiled?
 1. Check whether the `AssetsLibrary.framwork`, `CoreMedia.framework`, `Accelerate.framework`, and `Metal.frameworkdependent` dependent libraries have been added.
                 
### 2. What should I do if the project crashed during execution?  
 > 1. Check whether the project is configured with `-ObjC`.  
 > 2. Check whether "Metal API Validation" is set to "Disabled".
     
### 3. Why doesn't the special effect take effect in the project?  
 > 1. Check whether the `+[TXUGCBase setLicenceURL:key:]` method is called and the parameters are correct.
 > 2. Call the `getLicenseInfo` method of `TXUGCBase`. If a license contains animated effects, you will find the `pituLicense` field.
 > 3. Check whether the Pitu resources are properly added. Especially, the `handdetect`, `handtrack`, and `res18_3M` files should be added as folder references. The simplest way to check is to check whether the animated effect files added in your project are the same as those added in the demo.  
 > 4. The SDK will download the license into the `Documents` directory of the sandbox. During development, you can select "Window" > "Devices and Simulators" in the Xcode menu, export the license, and use the query tool (available [here](https://mc.qcloudimg.com/static/archive/9c0f8c02466d08e5ac14c396fad21005/PituDateSearch.zip)) to view the validity period.
 The [query tool](https://mc.qcloudimg.com/static/archive/9c0f8c02466d08e5ac14c396fad21005/PituDateSearch.zip) is an Xcode project and is currently supported for macOS only. More query methods will be provided in the future.
