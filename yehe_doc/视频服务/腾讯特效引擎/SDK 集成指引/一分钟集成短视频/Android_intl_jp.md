[](id:step1)
## ステップ1：Demoプロジェクトの解凍
1. Tencent Effect TEを統合した[UGSV Demo](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/Android/2.4.1.115.vcube/UGSV_Demo.zip)プロジェクトをダウンロードします。
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
DemoプロジェクトのTCVideoRecoredActivityクラスを参照できます。
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
            XmagicLoadAssetsView loadAssetsView = new XmagicLoadAssetsView(this);
            loadAssetsView.setOnAssetsLoadFinishListener(() -> {
                XmagicResParser.parseRes(getApplicationContext());
                initXMagic();
            });
        }
    }
```
3. **プッシュ設定の有効化：**
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
4. **textureIdをSDKに渡し、レンダリング処理を実施：**
VideoCustomProcessListenerインターフェースの`onTextureCustomProcess(int textureId, int width, int height)`メソッド内に次のコードを追加します。
```java
if (isPause == 0 && mXMagic !=null) {
    return mXMagic.process(textureId, width, height);
}
return 0;
```
5. **SDKの一時停止/破棄：**
 onPause()は美顔効果の一時停止に使用し、Activity/Fragmentライフサイクルメソッドにおいて実行できます。onDestroyメソッドはGLスレッドで呼び出す必要があります（onTextureDestroyedメソッドでXMagicImplオブジェクトの`onDestroy()`を呼び出すことができます）。その他の使用についてはDemoをご参照ください。
```java
mXMagic.onPause();   //一時停止。ActivityのonPauseメソッドにバインドします
mXMagic.onDestroy();  //破棄。GLスレッドで呼び出す必要があります
```
6. **レイアウトにSDK美顔パネルをロードしたレイアウトを追加：**
```xml
 <RelativeLayout
        android:id="@+id/panel_layout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:visibility="gone"/>
```
7. **パネルの初期化**
```java
 private void initXMagic() {
        if (mXMagic == null) {
            mXMagic = new XMagicImpl(this, mBeautyPanel);
        }else{
           mXMagic.onResume();
        }
    }
```

具体的な操作についてはDemoプロジェクトの`TCVideoRecordActivity.initXMagic();`メソッドをご参照ください。

