## Step 1. Download and integrate effect resources
[Download](https://intl.cloud.tencent.com/document/product/1143/45377) the corresponding SDK for the package you purchased and add the resource files to your own project:
<dx-tabs>
::: Android
1. Open `build.gradle` in `app` and add the Maven address for your package. For example, if you purchased S1 - 04, add the following:
```groovy
dependencies {
			implementation 'com.tencent.mediacloud:TencentEffect_S1-04:latest.release'
	 }
```
**You can find the Maven addresses of different packages on [this page](https://intl.cloud.tencent.com/document/product/1143/45385).**
2. Find the `src/main/assets` folder in `app` (if there isn’t this folder, create one). Check if there is a `MotionRes` folder. Copy it to `../src/main/assets`.
3. Open `AndroidManifest.xml` in `app` and add the following tag to `application`.
```xml
 <uses-native-library
					 android:name="libOpenCL.so"
					 android:required="true" />
```
It will look like this:
![](https://qcloudimg.tencent-cloud.cn/raw/adca155b8fa60600465bdfc6e78ebb2b.png)
:::
::: iOS
1. **Add effect resources to your project** (your resources may differ from those in the screenshot):
![](https://qcloudimg.tencent-cloud.cn/raw/e5cb4984aa2bfa14fd4f837acf465cfa.png)
2. Copy the four classes in `demo/lib/producer` – `BeautyDataManager`, `BeautyPropertyProducer`, `BeautyPropertyProducerAndroid`, and `BeautyPropertyProducerIOS` – to your Flutter project. They are used to configure effect resources and display effect options in the effect panel.
:::
</dx-tabs>

## Step 2. Reference the Flutter SDK
Add the following reference to the `pubspec.yaml` file of your project:
```json
 tencent_effect_flutter:
	 git:
		 url: https://github.com/TencentCloud/tencenteffect-sdk-flutter
```

## Step 3. Bind MLVB and Tencent Effect
<dx-tabs>
::: Android
Add the following code to `oncreate` of the `application` class (or `onCreate` of `FlutterActivity`):
```java
TXLivePluginManager.register(new XmagicProcesserFactory());
```
:::
::: iOS
Add the following code to `didFinishLaunchingWithOptions` of the `AppDelegate` class:
```objective-c
XmagicProcesserFactory *instance = [[XmagicProcesserFactory alloc] init];
[TXLivePluginManager registerWithCustomBeautyProcesserFactory:instance];
```
It will look like this:
![](https://qcloudimg.tencent-cloud.cn/raw/3f2de0a60696f18daedde2228d65076a.png)
:::
</dx-tabs>

## Step 4. Call the resource initialization API
```dart
String dir =  await BeautyDataManager.getInstance().getResDir();
 TXLog.printlog('The file path: $dir');
 TencentEffectApi.getApi()?.initXmagic(dir,(reslut) {
	 _isInitResource = reslut;
	 callBack.call(reslut);
	 if (!reslut) {
		 Fluttertoast.showToast(msg: "Failed to initialize the resources");
	 }
 }); TencentEffectApi.getApi()?.initXmagic((reslut) {
	 if (!reslut) {
		 Fluttertoast.showToast(msg: "Failed to initialize the resources");
	 }
 });
```

## Step 5. Set the license
```dart
TencentEffectApi.getApi()?.setLicense(licenseKey, licenseUrl,
									(errorCode, msg) {
											TXLog.printlog("Print the authentication result errorCode = $errorCode   msg = $msg");
											if (errorCode == 0) {
												// Authentication succeeded
											}
	});
```

## Step 6. Enable effects
```dart
/// Enable effects
var enableCustomVideo = await _livePusher?.enableCustomVideoProcess(true);
```

## Step 7. Set effect properties
```dart
TencentEffectApi.getApi()?.updateProperty(_xmagicProperty!);
/// You can call `BeautyDataManager.getInstance().getAllPannelData()` to get all the properties and call `updateProperty` to set properties.
```

## Step 8. Set other properties
- **Pause audio effects**
```dart
 TencentEffectApi.getApi()?.onPause();  
```
- **Resume audio effects**
```dart
TencentEffectApi.getApi()?.onResume();
```
- **Listen for effect events**
```dart
TencentEffectApi.getApi()
			 ?.setOnCreateXmagicApiErrorListener((errorMsg, code) {
				 TXLog.printlog("Error creating an effect object errorMsg = $errorMsg , code = $code");
	 });   ///You need to set the listener before creating an effect object
```
- **Configure the callback of face, gesture, and body detection results**
```dart
TencentEffectApi.getApi()?.setAIDataListener(XmagicAIDataListenerImp());
```
- **Configure the callback for animated effect tips**
```dart
TencentEffectApi.getApi()?.setTipsListener(XmagicTipsListenerImp());
```
- **Configure the callback of facial keypoints and other data (only available in S1 - 05 and S1 - 06)**
```dart
TencentEffectApi.getApi()?.setYTDataListener((data) {
		 TXLog.printlog("setYTDataListener  $data");
	 });
```
- **Remove all callbacks**
You need to remove all callbacks when terminating the page:
```dart
 TencentEffectApi.getApi()?.setOnCreateXmagicApiErrorListener(null);
 TencentEffectApi.getApi()?.setAIDataListener(null);
 TencentEffectApi.getApi()?.setYTDataListener(null);
 TencentEffectApi.getApi()?.setTipsListener(null);
```
>? For more information on the APIs, see the API documentation. For others, refer to the demo project.

## Step 9. Add data to and remove data from the effect panel
You can customize effect panel data in the `BeautyDataManager`, `BeautyPropertyProducer`, `BeautyPropertyProducerAndroid`, and `BeautyPropertyProducerIOS` classes.
- **Add effect resources**:
	1. Add your resource file to the corresponding folder as described in step 1. For example, to add a 2D animated effect, you need to put the resource in `android/xmagic/src.mian/assets/MotionRes/2dMotionRes` of your project.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7e91b97099e3d337de31c4893686759b.png" style="zoom:50%;" />
	2. Also add the resource to `ios/Runner/xmagic/2dMotionRes.bundle`.
<img src="https://qcloudimg.tencent-cloud.cn/raw/8c806cb1c77d9c49b787ab17f77a2f0d.png" style="zoom:50%;" />
- **Delete effect resources**:
Your license may not support some beautification or body retouch effects, which you can delete from the panel. For example, to delete lipstick effects, do the following:
Delete the code below from `getBeautyData` of `BeautyPropertyProducerAndroid` and `BeautyPropertyProducerIOS`.
<img src="https://qcloudimg.tencent-cloud.cn/raw/774aa1367fce726b17e34319d1b08bc2.png" style="zoom:50%;" />
