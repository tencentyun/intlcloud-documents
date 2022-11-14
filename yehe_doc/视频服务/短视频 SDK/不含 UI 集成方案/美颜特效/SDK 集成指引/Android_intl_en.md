[](id:step1)
## Step 1. Replace resources
1. Download the [UGSV demo](https://intl.cloud.tencent.com/document/product/1143/45374) which has been integrated with the Tencent Effect SDK. This demo is built based on the Tencent Effect SDK S1-04 edition.
2. Replace resources: As the SDK edition used by the demo project may be different from the SDK edition you actually use, you need to replace the different SDK files in the demo with the files in the SDK edition you actually use as follows:
   - In the `build.gradle` file of the `xmagickit` module, find the following:
```groovy
api 'com.tencent.mediacloud:TencentEffect_S1-04:latest.release'
```
Replace it with the SDK edition you purchased as described in [Integrating the Tencent Effect SDK (Android)](https://intl.cloud.tencent.com/document/product/1143/45385).
  - If your edition contains animated effects and filters, you need to download the corresponding resources on the [Tencent Effect SDK download](https://intl.cloud.tencent.com/document/product/1143/45377) page and put them in the following directories of the `xmagickit` module respectively:
	- Animated effects: `../assets/MotionRes`.
	- Filters: `../assets/lut`.
3. Import the `xmagickit` module from the demo into your actual project.

[](id:step2)
## Step 2. Open `build.gradle` in `app` and do the following:
Replace the `applicationId` with the package name under the obtained trial license.

[](id:step3)
## Step 3. Integrate the SDK APIs
You can refer to the `UGCKitVideoRecord` class of the demo.
1. **Authorize:**
```java
 // For details about authentication and error codes, see https://intl.cloud.tencent.com/document/product/1143/45385#.E6.AD.A5.E9.AA.A4.E4.B8.80.EF.BC.9A.E9.89.B4.E6.9D.83
 XMagicImpl.checkAuth(new TELicenseCheck.TELicenseCheckListener() {
            @Override
            public void onLicenseCheckFinish(int errorCode, String msg) {
                if (errorCode == TELicenseCheck.ERROR_OK) {
                    loadXmagicRes();
                } else {
                    Log.e("TAG", "auth fail, please check auth url and key" + errorCode + " " + msg);
                }
            }
        });
```
2. **Initialize the material:**
```java
 private void loadXmagicRes() {
        if (XMagicImpl.isLoadedRes) {
            XmagicResParser.parseRes(mActivity.getApplicationContext());
            initXMagic();
            return;
        }
        new Thread(new Runnable() {
            @Override
            public void run() {
                XmagicResParser.copyRes(mActivity.getApplicationContext());
                XmagicResParser.parseRes(mActivity.getApplicationContext());
                XMagicImpl.isLoadedRes = true;
                new Handler(Looper.getMainLooper()).post(new Runnable() {
                    @Override
                    public void run() {
                        initXMagic();
                    }
                });
            }
        }).start();
    }
```
3. **Bind beauty filters to UGSV:**
```java
 private void initBeauty() {
        TXUGCRecord instance = TXUGCRecord.getInstance(UGCKit.getAppContext());
        instance.setVideoProcessListener(new TXUGCRecord.VideoCustomProcessListener() {
            @Override
            public int onTextureCustomProcess(int textureId, int width, int height) {
                if (xmagicState == XMagicImpl.XmagicState.STARTED && mXMagic != null) {
                    return mXMagic.process(textureId, width, height);
                }
                return textureId;
            }

            @Override
            public void onDetectFacePoints(float[] floats) {
            }

            @Override
            public void onTextureDestroyed() {
                if (Looper.getMainLooper() != Looper.myLooper()) {  // Not the main thread
                    boolean stopped = xmagicState == XMagicImpl.XmagicState.STOPPED;
                    if (stopped || xmagicState == XMagicImpl.XmagicState.DESTROYED) {
                        if (mXMagic != null) {
                            mXMagic.onDestroy();
                        }
                    }
                    if (xmagicState == XMagicImpl.XmagicState.DESTROYED) {
                        TXUGCRecord.getInstance(UGCKit.getAppContext()).setVideoProcessListener(null);
                    }
                }
            }
        });
    }
```
4. **Pause/Terminate the SDK**:
 `onPause()` is used to pause the beauty filter effect, which can be executed in the `Activity/Fragment` lifecycle method. The `onDestroy` method needs to be called in the GL thread (the `onDestroy()` of the `XMagicImpl` object can be called in the `onTextureDestroyed` method). For more information, see the `onTextureDestroyed` method in the sample code.
```java
            @Override
            public void onTextureDestroyed() {
                if (Looper.getMainLooper() != Looper.myLooper()) {  // Not the main thread
                    boolean stopped = xmagicState == XMagicImpl.XmagicState.STOPPED;
                    if (stopped || xmagicState == XMagicImpl.XmagicState.DESTROYED) {
                        if (mXMagic != null) {
                            mXMagic.onDestroy();
                        }
                    }
                    if (xmagicState == XMagicImpl.XmagicState.DESTROYED) {
                        TXUGCRecord.getInstance(UGCKit.getAppContext()).setVideoProcessListener(null);
                    }
                }
            }
```
5. **Add the beauty filter panel to the layout:**
```xml
 <RelativeLayout
        android:id="@+id/panel_layout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:visibility="gone"/>
```
6. **Create a beauty filter object and add the beauty filter panel.**
```java
   private void initXMagic() {
       if (mXMagic == null) {
           mXMagic = new XMagicImpl(mActivity, getBeautyPanel());
       } else {
           mXMagic.onResume();
       }
   }
```

For detailed directions, see the `UGCKitVideoRecord` class of the demo.

