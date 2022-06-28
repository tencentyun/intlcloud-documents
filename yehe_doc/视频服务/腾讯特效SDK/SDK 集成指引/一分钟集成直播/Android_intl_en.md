[](id:step1)
## Step 1. Replace resources
1. Download the [MLVB demo](https://intl.cloud.tencent.com/document/product/1143/45374) which has integrated the Tencent Effect SDK. This demo is built based on the Tencent Effect SDK S1-04 edition.
2. Replace the SDK files in the demo with the files for the SDK you actually use. Specifically, follow the steps below:
   - Replace the `.aar` file in the `libs` directory of the `Xmagic` module with the `.aar` file in `libs` of your SDK.
   - Replace all the files in `../src/main/assets` of the `Xmagic` module with those in `assets/` of your SDK. If there are files in the `MotionRes` folder of your SDK package, also copy them to the `../src/main/assets` directory.
   - Replace all the `.so` files in `../src/main/jniLibs` of the `Xmagic` module with the `.so` files in `jniLibs` of your SDK package (you need to decompress the ZIP files in the `jinLibs` folder to get the `.so` files for arm64-v8a and armeabi-v7a).
3. Import the xMagic module from the demo into your actual project.

[](id:step2)

## Step 2. Open `build.gradle` in `app` and do the following:
1. Set `applicationId` to the package name bound to the trial license.
2. Add Gson dependency settings.
```groovy
configurations  {
all*.exclude  group:  'com.google.code.gson'
}
```

[](id:step3)

## Step 3. Integrate the SDK APIs
You can refer to the `ThirdBeautyActivity` class of the demo.
1. **Authorize**:
```java
 // For authentication precautions and error codes, see https://intl.cloud.tencent.com/document/product/1143/45385#step-1.-authenticate
XMagicImpl.checkAuth((errorCode, msg) -> {
            if (errorCode == TELicenseCheck.ERROR_OK) {
                showLoadResourceView();
            } else {
                TXCLog.e(TAG, "Authentication failed. Check the authentication URL and key" + errorCode + " " + msg);
            }
        });
```
2. **Initialize the material**:
```java
   private void showLoadResourceView() {
        if (XmagicLoadAssetsView.isCopyedRes) {
            XmagicResParser.parseRes(getApplicationContext());
            initXMagic();
        } else {
            XmagicLoadAssetsView loadAssetsView = new XmagicLoadAssetsView(this);
            loadAssetsView.setOnAssetsLoadFinishListener(() -> {
                XmagicResParser.parseRes(getApplicationContext());
                initXMagic();
            });
        }
    }
```
3. **Enable push settings**:
```java
String userId = String.valueOf(new Random().nextInt(10000));
String pushUrl = AddressUtils.generatePushUrl(streamId, userId, 0);
mLivePusher = new V2TXLivePusherImpl(this, V2TXLiveDef.V2TXLiveMode.TXLiveMode_RTC);
mLivePusher.enableCustomVideoProcess(true, V2TXLivePixelFormatTexture2D, V2TXLiveBufferTypeTexture);
mLivePusher.setObserver(new V2TXLivePusherObserver() {
	@Override
	public void onGLContextCreated() {
	}

	@Override
	public int onProcessVideoFrame(V2TXLiveDef.V2TXLiveVideoFrame srcFrame, V2TXLiveDef.V2TXLiveVideoFrame dstFrame) {
		if (mXMagic != null) {
			dstFrame.texture.textureId = mXMagic.process(srcFrame.texture.textureId, srcFrame.width, srcFrame.height);
		}
		return srcFrame.texture.textureId;
		}

		@Override
		public void onGLContextDestroyed() {
		if (mXMagic != null) {
			mXMagic.onDestroy();
		}
	}
});
mLivePusher.setRenderView(mPushRenderView);
mLivePusher.startCamera(true);
int ret = mLivePusher.startPush(pushUrl);
mLivePusher.startMicrophone();
```
4. **Pass the `textureId` into the SDK for rendering:**
In the `onProcessVideoFrame(V2TXLiveDef.V2TXLiveVideoFrame srcFrame, V2TXLiveDef.V2TXLiveVideoFrame dstFrame)` method of the `V2TXLivePusherObserver` API, add the following code:
```java
if (mXMagic != null) {
	dstFrame.texture.textureId = mXMagic.process(srcFrame.texture.textureId, srcFrame.width,srcFrame.height);
}
return srcFrame.texture.textureId;
```
5. **Pause/Terminate the SDK**:
`onPause()` is used to pause the beauty filter effect, which can be executed in the `Activity/Fragment` lifecycle method. The `onDestroy` method needs to be called in the GL thread (the `onDestroy()` of the `XMagicImpl` object can be called in the `onTextureDestroyed` method). For more information, see the demo.  
```java
mXMagic.onPause();   // Pause, which is bound to the `onPause` method of `Activity`
mXMagic.onDestroy();  // // Terminate, which needs to be called in the GL thread
```
6. **Add the SDK beauty filter panel to the layout:**
```xml
    <RelativeLayout
        android:id="@+id/livepusher_bp_beauty_pannel"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_above="@+id/ll_edit_info" />
```
7. **Initialize the panel:**
```java
  private void initXMagic() {
          if (mXMagic == null) {
              mXMagic = new XMagicImpl(this, mBeautyPanelView);
          }else {
              mXMagic.onResume();
          }
      }
```

See the `ThirdBeautyActivity.initXMagic();` method of the demo for details.
