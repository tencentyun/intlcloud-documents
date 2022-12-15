[](id:step1)
## 手順1：Demoプロジェクトの解凍
1. Tencent Effect TEを統合した[UGSV Demo](https://intl.cloud.tencent.com/document/product/1143/45374)プロジェクトをダウンロードします。このDemoは、Tencent Effect SDK S1-04パッケージに基づいて作成されています。
2. リソースの置き換え：このDemoプロジェクトで使用するSDKパッケージが実際のパッケージと一致するとは限らないため、このDemoの関連SDKファイルを実際に使用されるパッケージのSDKファイルに置き換える必要があります。具体的な操作は次のとおりです。
   - `xmagickit module`の`build.gradle`ファイルで下記を見つけます。
```groovy
api 'com.tencent.mediacloud:TencentEffect_S1-04:latest.release'
```
購入した[依存パッケージ](https://intl.cloud.tencent.com/document/product/1143/45385)に置き換えます。
   - パッケージに動的エフェクトおよびフィルター機能が含まれる場合は、Tencent Effect [SDKダウンロードページ](https://intl.cloud.tencent.com/document/product/1143/45377)で対応するリソースをダウンロードし、動的エフェクトおよびフィルター素材を`xmagickit module`下の以下のディレクトリに配置する必要があります。
	- 動的エフェクト：`../assets/MotionRes`
	- フィルター：`../assets/lut`
3. Demoプロジェクトのxmagickitモジュールを実際のプロジェクトにインポートします。

[](id:step2)

## 手順2：appモジュールのbuild.gradleを開く
applicationIdを、申請したテスト権限と同じパッケージ名に変更します。

[](id:step3)
## 手順3：SDKインターフェースの統合
DemoプロジェクトのUGCKitVideoRecordタイプを参照できます。
1. **権限承認：**
```java
 //認証の注意事項およびエラーコードの詳細については、https://intl.cloud.tencent.com/document/product/1143/45385#.E6.AD.A5.E9.AA.A4.E4.B8.80.EF.BC.9A.E9.89.B4.E6.9D.83をご参照ください
 XMagicImpl.checkAuth(new TELicenseCheck.TELicenseCheckListener() {
            @Override
            public void onLicenseCheckFinish(int errorCode, String msg) {
                if (errorCode == TELicenseCheck.ERROR_OK) {
                    loadXmagicRes();
                }else{
                    Log.e("TAG", "auth fail ,please check auth url and key" + errorCode + " " + msg);
                }
            }
        });
```
2. **素材の初期化：**
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
3. **UGSVと美顔のバインド：**
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
                if (Looper.getMainLooper() != Looper.myLooper()) {  //メインスレッドではない
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
4. **SDKの一時停止/破棄：**
 `onPause()`は美顔効果の一時停止に使用し、Activity/Fragmentライフサイクルメソッドにおいて実行できます。onDestroyメソッドはGLスレッドで呼び出す必要があります（onTextureDestroyedメソッドでXMagicImplオブジェクトの`onDestroy()`を呼び出すことができます）。その他の使用については事例にあるonTextureDestroyedメソッドをご参照ください。
```java
            @Override
            public void onTextureDestroyed() {
                if (Looper.getMainLooper() != Looper.myLooper()) {  //メインスレッドではない
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
5. **レイアウトに美顔パネルをロードしたレイアウトを追加：**
```xml
 <RelativeLayout
        android:id="@+id/panel_layout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:visibility="gone"/>
```
6. **美顔オブジェクトを作成して美顔パネルを追加**
```java
   private void initXMagic() {
       if (mXMagic == null) {
           mXMagic = new XMagicImpl(mActivity, getBeautyPanel());
       }else{
           mXMagic.onResume();
       }
   }
```

具体的な操作についてはDemoプロジェクトのUGCKitVideoRecordタイプをご参照ください。

