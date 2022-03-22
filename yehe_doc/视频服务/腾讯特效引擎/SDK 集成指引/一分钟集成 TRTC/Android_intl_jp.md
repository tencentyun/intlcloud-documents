[](id:step1)
## ステップ1：Demoプロジェクトの解凍

1. Tencent Effect TEを統合した[TRTC Demo](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/Android/2.4.1.115.vcube/TRTC-API-Example.zip)プロジェクトをダウンロードします。
2. Demoプロジェクトのxmagicモジュールを実際のプロジェクトにインポートします。

[](id:step2)

## ステップ2：appモジュールのbuild.gradleを開く
1. applicationIdを、テスト用に申請した権限と同じパッケージ名に変更します。
2. gson依存設定を追加します。
```groovy
configurations{
	all*.exclude group:'com.google.code.gson'
}
```

[](id:step3)
## ステップ3：SDKインターフェースの統合
DemoプロジェクトのThirdBeautyActivityクラスを参照できます。
1. **権限承認：**
```java
  //認証の注意事項およびエラーコードの詳細については、https://cloud.tencent.com/document/product/616/65891#.E6.AD.A5.E9.AA.A4.E4.B8.80.EF.BC.9A.E9.89.B4.E6.9D.83をご参照ください
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
TRTCVideoFrameListenerインターフェースの`onProcessVideoFrame(TRTCCloudDef.TRTCVideoFrame srcFrame, TRTCCloudDef.TRTCVideoFrame dstFrame)`メソッド内に次のコードを追加します。 
```
dstFrame.texture.textureId = mXMagic.process(srcFrame.texture.textureId, srcFrame.width, srcFrame.height);
```
5. **SDKの一時停止/停止：**
onPause()は美顔効果の一時停止に使用し、Activity/Fragmentライフサイクルメソッドにおいて実行できます。onDestroyメソッドはGLスレッドで呼び出す必要があります（onTextureDestroyedメソッドでXMagicImplオブジェクトの`onDestroy()`を呼び出すことができます）。その他の使用についてはDemoをご参照ください。
```java
mXMagic.onPause();   //一時停止。ActivityのonPauseメソッドにバインドします
mXMagic.onDestroy();  //破棄。GLスレッドで呼び出す必要があります
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

​    具体的な操作についてはDemoプロジェクトの`ThirdBeautyActivity.initXMagic();`メソッドをご参照ください。

