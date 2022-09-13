UGSV Enterprise Edition has been discontinued, and its beauty filter module has been decoupled to form Tencent Effect SDK. Tencent Effect SDK has more natural beautification effects, more powerful features, and more flexible integration methods. This document describes how to migrate from UGSV Enterprise Edition to Tencent Effect SDK.

## Notes
1. Modify the version number of the `glide` library in the `xmagic` module to make it the same as the actual version number.
2. Modify the earliest version number in the `xmagic` module to make it the same as the actual version number.


## Integration steps
### Step 1. Decompress the demo project
1. Download the [UGSV demo](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/Android/2.4.1.115.vcube/UGSV_Demo.zip) which has integrated the Tencent Effect SDK. This demo is built based on the Tencent Effect SDK S1-04 edition.
2. Replace the SDK files in the demo with the files for the SDK you actually use. Specifically, follow the steps below:
   - Replace the `.aar` file in the `libs` directory of the `Xmagic` module with the `.aar` file in `libs` of your SDK.
   - Replace all the files in `../src/main/assets` of the `Xmagic` module with those in `assets/` of your SDK. If there are files in the `MotionRes` folder of your SDK package, also copy them to the `../src/main/assets` directory.
   - Replace all the `.so` files in `../src/main/jniLibs` of the `Xmagic` module with the `.so` files in `jniLibs` of your SDK package (you need to decompress the ZIP files in the `jinLibs` folder to get the `.so` files for arm64-v8a and armeabi-v7a).
3. Import the `Xmagic` module in the demo into your project.

### Step 2. Upgrade the SDK edition
Upgrade the SDK from Enterprise Edition to Pro Edition.
- **Before replacement:** `implementation 'com.tencent.liteav:LiteAVSDK_Enterprise:latest.release'`
- **After replacement:** `implementation 'com.tencent.liteav:LiteAVSDK_Professional:latest.release'`

### Step 3. Set the beauty filter license
1. Call the `oncreate` method in `application` in the project as follows:
```java
XMagicImpl.init(this);
XMagicImpl.checkAuth(null);
```
2. Replace the content in the `XMagicImpl` class with your obtained Tencent Effect SDK **license URL and key**.

### Step 4. Implement the code
Take the UGSV recording page `TCVideoRecordActivity.java` as an example:

1. Add the following variable code to the `TCVideoRecordActivity.java` class:
```java
private XMagicImpl mXMagic;
private int isPause = 0;// 0: not paused; 1: paused; 2: pausing; 3: to be terminated
```
2. Add the following code after the `onCreate` method in the `TCVideoRecordActivity.java` class:
```java
TXUGCRecord instance = TXUGCRecord.getInstance(this);
instance.setVideoProcessListener(new TXUGCRecord.VideoCustomProcessListener() {
	 @Override
	 public int onTextureCustomProcess(int textureId, int width, int height) {
			 if (isPause == 0 && mXMagic != null) {
					 return mXMagic.process(textureId, width, height);
			 }
			 return 0;
	 }

	 @Override
	 public void onDetectFacePoints(float[] floats) {
	 }

	 @Override
	 public void onTextureDestroyed() {
			 if (Looper.getMainLooper() != Looper.myLooper()) {  // Not the main thread
					 if (isPause == 1) {
							 isPause = 2;
							 if (mXMagic != null) {
									 mXMagic.onDestroy();
							 }
							 initXMagic();
							 isPause = 0;
					 } else if (isPause == 3) {
							 if (mXMagic != null) {
									 mXMagic.onDestroy();
							 }
					 }
			 }
	 }
});
XMagicImpl.checkAuth((errorCode, msg) -> {
	 if (errorCode == TELicenseCheck.ERROR_OK) {
			 loadXmagicRes();
	 } else {
			 TXCLog.e("TAG", "Authentication failed. Check the authentication URL and key" + errorCode + " " + msg);
	 }
});
```
3. Add the following code to the `onStop` method:
```java
isPause = 1;
if (mXMagic != null) {
	 mXMagic.onPause();
}
```
4. Add the following code to the `onDestroy` method:
```java
isPause = 3;
XmagicPanelDataManager.getInstance().clearData();
```
5. Add the following code at the beginning of the `onActivityResult` method:
```java
if (mXMagic != null) {
	 mXMagic.onActivityResult(requestCode, resultCode, data);
}
```
6. Add the following two methods to the end of this class:
```java
private void loadXmagicRes() {
	 if (XMagicImpl.isLoadedRes) {
			 XmagicResParser.parseRes(getApplicationContext());
			 initXMagic();
			 return;
	 }
	 new Thread(() -> {
			 XmagicResParser.setResPath(new File(getFilesDir(), "xmagic").getAbsolutePath());
			 XmagicResParser.copyRes(getApplicationContext());
			 XmagicResParser.parseRes(getApplicationContext());
			 XMagicImpl.isLoadedRes = true;
			 new Handler(Looper.getMainLooper()).post(() -> {
					 initXMagic();
			 });
	 }).start();

}
/**
* Initialize the beauty filter SDK
*/
private void initXMagic() {
	 if (mXMagic == null) {
			 mXMagic = new XMagicImpl(this, mUGCKitVideoRecord.getBeautyPanel());
	 }else {
			 mXMagic.onResume();
	 }
}
```

### Step 5. Modify other classes

1. Change the `mBeautyPanel` type in the `AbsVideoRecordUI` class to the `RelativeLayout` type and the response type of the `getBeautyPanel()` method to `RelativeLayout`. You also need to modify the corresponding XML configuration to comment out the code that reports errors.
2. Comment out the code that reports errors in the `UGCKitVideoRecord` class.
3. Modify the code in the `ScrollFilterView` class to delete the `mBeautyPanel` variable and comment out the code that reports errors.

### Step 6. Delete the dependencies on the `beautysettingkit` module
Delete the dependencies on the `beautysettingkit` module in the `build.gradle` file in the `ugckit` module and compile the project to comment out the code that report errors.

