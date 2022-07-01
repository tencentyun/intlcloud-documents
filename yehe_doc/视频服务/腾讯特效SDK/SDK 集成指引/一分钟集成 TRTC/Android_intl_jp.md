[](id:step1)
## 手順1：Demoプロジェクトの解凍

1. Tencent Effect TEを統合した[TRTC Demo](https://intl.cloud.tencent.com/document/product/1143/45374)プロジェクトをダウンロードします。このDemoは、Tencent Effect SDK S1-04パッケージに基づいて作成されています。
2. リソースを置き換えます。このDemoプロジェクトで使用されるSDKパッケージは実際のパッケージと同じではない可能性があるため、このDemoの関連SDKファイルを実際に使用するパッケージのSDKファイルに置き換えてください。具体的な操作は以下のとおりです：
   - xmagicモジュールのlibsディレクトリにある`.aar`ファイルを削除し、SDKのlibsディレクトリにある.aar`ファイルをxmagicモジュールのlibsディレクトリにコピーします。
   - xmagicモジュールのassetsディレクトリにあるすべてのファイルを削除し、SDKの`assets/`ディレクトリにあるすべてのリソースをxmagicモジュールの`../src/main/assets`ディレクトリにコピーします。SDKパッケージのMotionResフォルダにリソースがある場合は、このフォルダを`../src/main/assets`ディレクトリにコピーします。
   - xmagicモジュールのjniLibsディレクトリにあるすべての.soファイルを削除し、SDKパッケージのjniLibsで対応する.soファイルを見つけて（SDKのjinLibsフォルダにあるarm64-v8aおよびarmeabi-v7aの.soファイルが圧縮パッケージに存在しているため、先に解凍する必要がある）、xmagicモジュールの`../src/main/jniLibs`ディレクトリにコピーします。
3. Demoプロジェクトのxmagicモジュールを実際のプロジェクトにインポートします。

[](id:step2)

## 手順2：appモジュールのbuild.gradleを開く
1. applicationIdを、テスト用に申請した権限と同じパッケージ名に変更します。
2. gson依存設定を追加します。
```groovy
configurations{
    all*.exclude group:'com.google.code.gson'
}
```

[](id:step3)
## 手順3：SDKインターフェースの統合
DemoプロジェクトのThirdBeautyActivityクラスを参照できます。
1. **権限承認：**
```java
  //認証に関する注意事項とエラーコードの詳細については、https://intl.cloud.tencent.com/document/product/1143/45385#step-1.-authenticateを参照してください。
XMagicImpl.checkAuth((errorCode, msg) -> {
                if (errorCode == TELicenseCheck.ERROR_OK) {
                    showLoadResourceView();
                }else{
                    TXCLog.e(TAG, "認証に失敗しました。認証urlおよびkeyをご確認ください" + errorCode + " " + msg);
                }
            });
```
2. **素材の初期化：**
```java
private void showLoadResourceView() {
        if (XmagicLoadAssetsView.isCopyedRes) {
            XmagicResParser.parseRes(getApplicationContext());
            initXMagic();
        }else{
            loadAssetsView = new XmagicLoadAssetsView(this);
            loadAssetsView.setOnAssetsLoadFinishListener(() -> {
                XmagicResParser.parseRes(getApplicationContext());
                initXMagic();
            });
        }
    }
```
3. **プッシュ設定の有効化：**
```java
mTRTCCloud.setLocalVideoProcessListener(TRTCCloudDef.TRTC_VIDEO_PIXEL_FORMAT_Texture_2D, TRTCCloudDef.TRTC_VIDEO_BUFFER_TYPE_TEXTURE, new TRTCCloudListener.TRTCVideoFrameListener() {
    @Override
    public void onGLContextCreated() {
    }
    @Override
    public int onProcessVideoFrame(TRTCCloudDef.TRTCVideoFrame srcFrame, TRTCCloudDef.TRTCVideoFrame dstFrame) {
    }
    @Override
    public void onGLContextDestory() {
    }
});
```
4. **textureIdをSDKに渡し、レンダリング処理を実施：**
TRTCVideoFrameListenerインターフェースの`onProcessVideoFrame(TRTCCloudDef.TRTCVideoFrame srcFrame, TRTCCloudDef.TRTCVideoFrame dstFrame)`メソッド内に次のコードを追加します： 
```
dstFrame.texture.textureId = mXMagic.process(srcFrame.texture.textureId, srcFrame.width, srcFrame.height);
```
5. **SDKの一時停止/停止：**
onPause()は美顔効果の一時停止に使用し、Activity/Fragmentライフサイクルメソッドにおいて実行できます。onDestroyメソッドはGLスレッドで呼び出してください（onTextureDestroyedメソッドでXMagicImplオブジェクトの`onDestroy()`を呼び出すことができます）。その他の使用についてはDemoをご参照ください。
```java
mXMagic.onPause();   //一時停止。ActivityのonPauseメソッドにバインドします
mXMagic.onDestroy();  //破棄。GLスレッドで呼び出してください
```
6. **レイアウトにSDK美顔パネルを追加**：
```xml
    <RelativeLayout
        android:layout_above="@+id/ll_edit_info"
        android:id="@+id/livepusher_bp_beauty_pannel"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
```
7. **パネルの初期化：**
```java
      private void initXMagic() {
          if (mXMagic == null) {
              mXMagic = new XMagicImpl(this, mBeautyPanelView);
          }else{
              mXMagic.onResume();
          }
      }
```

​具体的な操作についてはDemoプロジェクトの`ThirdBeautyActivity.initXMagic();`メソッドをご参照ください。

