[](id:step1)
## Step 1. Replace resources
1. Download and unzip the UGSV demo that is integrated with the Tencent Effect SDK. In this example, Tencent Effect SDK S1-04 is used.
2. Replace the SDK files in the demo with the files for the SDK you actually use. Specifically, follow the steps below:
   - Replace the `.aar` file in the `libs` directory of the `Xmagic` module with the `.aar` file in `libs` of your SDK.
   - Replace all the files in `../src/main/assets` of the `Xmagic` module with those in `assets/` of your SDK. If there are files in the `MotionRes` folder of your SDK package, also copy them to the `../src/main/assets` directory.
   - Replace all the `.so` files in `../src/main/jniLibs` of the `Xmagic` module with the `.so` files in `jniLibs` of your SDK package (you need to decompress the ZIP files in the `jinLibs` folder to get the `.so` files for arm64-v8a and armeabi-v7a).
3. Import the `Xmagic` module in the demo into your project.

[](id:step2)

## Step 2. Open `build.gradle` in `app` and do the following:
1. Set `applicationId` to the package name bound to the trial license.
2. Add Gson dependency settings.
```groovy
configurations{
    all*.exclude group:'com.google.code.gson'
}
```

[](id:step3)
## Step 3. Integrate the SDK APIs
You can refer to the `TCVideoRecoredActivity` class of the demo.
1. **Authorize:**
```java
 // For details about authentication and error codes, see https://cloud.tencent.com/document/product/616/65891#.E6.AD.A5.E9.AA.A4.E4.B8.80.EF.BC.9A.E9.89.B4.E6.9D.83
XMagicImpl.checkAuth((errorCode, msg) -> {
            if (errorCode == TELicenseCheck.ERROR_OK) {
                showLoadResourceView();
            } else {
                TXCLog.e(TAG, "Authentication failed. Check the authentication URL and key" + errorCode + " " + msg);
            }
        });
```
2. **Initialize the material:**
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
3. **Enable push settings:**
```java
TXUGCRecord instance = TXUGCRecord.getInstance(this);
instance.setVideoProcessListener(new TXUGCRecord.VideoCustomProcessListener() {
    @Override
    public int onTextureCustomProcess(int textureId, int width, int height) {
        if (isPause == 0 && mXMagic !=null) {
            return mXMagic.process(textureId, width, height);
        }
        return 0;
    }
    @Override
    public void onDetectFacePoints(float[] floats) {
    }
    @Override
    public void onTextureDestroyed() {
        ...
    }
});
```
4. **Pass `textureId` to the SDK for rendering:**
In the `onTextureCustomProcess(int textureId, int width, int height)` method of `VideoCustomProcessListener`, add the following code:
```java
if (isPause == 0 && mXMagic !=null) {
    return mXMagic.process(textureId, width, height);
}
return 0;
```
5. **Pause/Terminate the SDK**:
 `onPause()` is used to pause beauty filter effects, which can be implemented in the `Activity/Fragment` method. The `onDestroy` method needs to be called in the GL thread (you can call `onDestroy()` of the `XMagicImpl` object in `onTextureDestroyed`). For more information, see the demo.
```java
mXMagic.onPause();   // Pause, which is bound to the `onPause` method of `Activity`
mXMagic.onDestroy();  // Terminate, which needs to be called in the GL thread
```
6. **Add the SDK beauty filter panel to the layout:**
```xml
 <RelativeLayout
        android:id="@+id/panel_layout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:visibility="gone"/>
```
7. **Initialize the panel.**
```java
 private void initXMagic() {
        if (mXMagic == null) {
            mXMagic = new XMagicImpl(this, mBeautyPanel);
        }else{
           mXMagic.onResume();
        }
    }
```

For detailed directions, see the `TCVideoRecordActivity.initXMagic();` method in the demo.

