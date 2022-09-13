[](id:step1)
## 手順1：Demoプロジェクトの解凍
1. Tencent Effect TEを統合した[UGSV Demo](https://intl.cloud.tencent.com/document/product/1143/45374)プロジェクトをダウンロードします。このDemoは、Tencent Effect SDK S1-04パッケージに基づいて作成されています。
2. リソースを置き換えます。このDemoプロジェクトで使用されるSDKパッケージは実際のパッケージと同じではない可能性があるため、このDemoの関連SDKファイルを実際に使用するパッケージのSDKファイルに置き換えてください。具体的な操作は以下のとおりです：
   - xmagicモジュールのlibsディレクトリにある`.aar`ファイルを削除し、SDKのlibsディレクトリにある.aar`ファイルをxmagicモジュールのlibsディレクトリにコピーします。
   - xmagicモジュールのassetsディレクトリにあるすべてのファイルを削除し、SDKの`assets/`ディレクトリにあるすべてのリソースをxmagicモジュールの`../src/main/assets`ディレクトリにコピーします。SDKパッケージのMotionResフォルダにリソースがある場合は、このフォルダを`../src/main/assets`ディレクトリにコピーします。
   - xmagicモジュールのjniLibsディレクトリにあるすべての.soファイルを削除し、SDKパッケージのjniLibsで対応する.soファイルを見つけて（SDKのjinLibsフォルダにあるarm64-v8aおよびarmeabi-v7aの.soファイルが圧縮パッケージに存在しているため、先に解凍してください）、xmagicモジュールの`../src/main/jniLibs`ディレクトリにコピーします。
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
DemoプロジェクトのTCVideoRecoredActivityクラスを参照できます。
1. **権限承認：**
```java
 //認証に関する注意事項とエラーコードの詳細については、https://intl.cloud.tencent.com/document/product/1143/45385を参照してください。
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
mXMagic.onDestroy();  //破棄。GLスレッドで呼び出してください
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

