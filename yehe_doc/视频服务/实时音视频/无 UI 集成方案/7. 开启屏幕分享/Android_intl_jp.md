このドキュメントでは、主に画面共有の使用方法を紹介します。現在、TRTCオーディオビデオルームで使用できる画面共有は1つだけです。

## 呼び出しガイド
### 画面共有の有効化

[](id:step1)
#### 手順1：Activityの追加
次のactivityをmanifestファイルに貼り付けます（項目コードに存在する場合は追加する必要はありません）。
```xml
<activity 
    android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity" 
    android:theme="@android:style/Theme.Translucent"/>
```

[](id:step2)
#### 手順2：画面共有の有効化
Android側での画面共有は、`TRTCCloud`の[startScreenCapture()](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)インターフェースを呼び出すだけで開始することができます。

[startScreenCapture()](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)で最初のパラメータ`encParams`を設定することにより、画面共有のエンコード品質を指定することができます。`encParams`をnullに指定した場合、SDKは以前に設定されたエンコードパラメータを自動的に使用します。推奨されるパラメータの設定は、次のとおりです：

| パラメータ項目 | パラメータ名 | 通常の推奨値 | テキスト教育シナリオ |
|---------|---------|---------|-----|
| 解像度 | videoResolution | 1280 × 720 | 1920 × 1080 |
| フレームレート | videoFps | 10 FPS | 8 FPS |
| 最高ビットレート | videoBitrate| 1600 kbps | 2000 kbps |
| 解像度アダプティブ | enableAdjustRes | NO | NO |

- 画面共有されるコンテンツには通常、大幅な変更がなく、FPSを高く設定するのは経済的ではないため、10FPSを推奨します。
- 共有したい画面コンテンツに大量のテキストが含まれている場合、解像度とビットレートを適宜引き上げることができます。
- 最高ビットレート(videoBitrate)とは、画面が大きく変化したときの最高出力ビットレートのことです。画面コンテンツの変化が少ない場合、実際のエンコードビットレートは低くなります。

[](id:step3)
#### 手順3：フローティングウィンドウをポップアップして、アプリケーションが強制終了されないようにします（オプション）
Android 7.0以降のシステムから、バックグラウンドで実行されている通常のアプリプロセスに切り替わりますが、CPUのアクティビティがある場合、常にシステムによって強制終了されやすくなります。従って、アプリをバックグラウンドに切り替えてサイレントで画面共有すると、フローティングウィンドウのポップアップというソリューションによって強制終了を回避することができます。また、携帯電話の画面にフローティングウィンドウを表示することは、ユーザーが今、画面共有を行っていることをユーザーに知らせ、プライバシー情報の漏えい防止につながります。

フローティングウィンドウをポップアップするには、[FloatingView.java](https://github.com/LiteAVSDK/TRTC_Android/tree/main/TRTC-API-Example/Basic/ScreenShare/src/main/java/com/tencent/trtc/screenshare/FloatingView.java)の実装を参照してください：
```java
public void showView(View view, int width, int height) {
        mWindowManager = (WindowManager) mContext.getSystemService(Context.WINDOW_SERVICE);
        int type = WindowManager.LayoutParams.TYPE_TOAST;
        //TYPE_TOASTは、4.4以降のシステムにのみ適用できます。下位バージョンをサポートするには、TYPE_SYSTEM_ALERTを使用します（manifestで権限を宣言してください）
        //7.1（7.1を含む）以降のシステムは、TYPE_TOASTに対して制限を設けています
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            type = WindowManager.LayoutParams.TYPE_APPLICATION_OVERLAY;
        } else if (Build.VERSION.SDK_INT > Build.VERSION_CODES.N) {
            type = WindowManager.LayoutParams.TYPE_PHONE;
        }
        mLayoutParams = new WindowManager.LayoutParams(type);
        mLayoutParams.flags = WindowManager.LayoutParams.FLAG_NOT_FOCUSABLE;
        mLayoutParams.flags |= WindowManager.LayoutParams.FLAG_WATCH_OUTSIDE_TOUCH;
        mLayoutParams.width = width;
        mLayoutParams.height = height;
        mLayoutParams.format = PixelFormat.TRANSLUCENT;
        mWindowManager.addView(view, mLayoutParams);
}
```

### 画面共有の確認
- ** Mac / Windows画面共有の確認**
  ルームにいるMac / Windowsユーザーが画面共有を開始する場合、サブストリームを介して共有を実行します。ルームにいるその他のユーザーは、TRTCCloudListener内の[onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a80bcaac82e5372245746a4bc63656390)イベントを介してこの通知を受け取ります。

- **Android / iOS画面共有の確認**
  ユーザーがAndroid / iOSを介して画面共有を開始する場合、ビッグストリームを介して共有を実行します。ルームにいるその他のユーザーは、TRTCCloudListener内の[onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05)イベントを介してこの通知を受け取ります。
  

画面共有を確認したいユーザーは[startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c)インターフェースを介してリモートユーザーのビッグストリーム画面のレンダリングを開始することができます。