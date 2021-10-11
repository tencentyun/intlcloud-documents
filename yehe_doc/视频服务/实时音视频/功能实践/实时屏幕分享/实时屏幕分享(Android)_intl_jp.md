Tencent CloudのTRTCは、Androidシステムでの画面共有をサポートしており、現在のシステムの画面コンテンツは、TRTC SDKを介してルーム内の他のユーザーと共有されます。この機能については、次のような2つの注意点があります。

- TRTC Android版の画面共有は、デスクトップ版のように「サブチャネルの共有」をサポートしていません。従って、画面共有を開始するときは、あらかじめカメラのキャプチャを停止する必要があります。停止しない場合、衝突が生じます。
- Androidシステムのバックグラウンドアプリが引き続きCPUを使用すると、システムによって強制終了されやすくなり、画面共有自体が必然的にCPUを消費してしまいます。この矛盾するような衝突を解消するには、アプリで画面共有を開始するとともに、Androidシステムにフローティングウィンドウをポップアップする必要があります。AndroidはフォアグラウンドUIを含むアプリプロセスを強制終了しないため、このソリューションによって、お客様のアプリはシステムに自動回収されることなく画面を共有し続けることができます。



## サポートするプラットフォーム

| iOS | Android | Mac OS | Windows |Electron| WeChat Mini Program | Chromeブラウザ|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003; |  &#10003; |  &#10003;  |&#10003;  |   &#10003;  |   ×   |  &#10003;  |

## 画面共有を開始
Androidデバイスでの画面共有は、`TRTCCloud`の[startScreenCapture()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)インターフェースを呼び出すだけで開始することができます。ただし、明瞭で安定した共有効果を実現するには、次の3つの点に注意する必要があります。

#### Activityの追加
次のactivityをmanifestファイルに貼り付けます（項目コードに存在する場合は追加する必要はありません）。
```xml
<activity 
    android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity" 
    android:theme="@android:style/Theme.Translucent"/>
```

#### ビデオコーデックパラメータの設定
[startScreenCapture()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)で最初のパラメータ`encParams`を設定することにより、画面共有のエンコード品質を指定することができます。`encParams`をnullに指定した場合、SDKは以前に設定されたエンコードパラメータを自動的に使用します。推奨されるパラメータの設定は、次のとおりです。

| パラメータ項目 | パラメータ名 | 通常の推奨値 | テキスト教育シナリオ |
|---------|---------|---------|-----|
| 解像度 | videoResolution | 1280 × 720 | 1920 × 1080 |
| フレームレート | videoFps | 10 FPS | 8 FPS |
| 最高ビットレート | videoBitrate| 1600 kbps | 2000 kbps |
| 解像度アダプティブ | enableAdjustRes | NO | NO |

- 画面共有されるコンテンツには通常、大幅な変更がなく、FPSを高く設定するのは経済的ではないため、10FPSを推奨します。
- 共有したい画面コンテンツに大量のテキストが含まれている場合、解像度とビットレートを適宜引き上げることができます。
- 最高ビットレート(videoBitrate)とは、画面が大きく変化したときの最高出力ビットレートのことです。画面コンテンツの変化が少ない場合、実際のエンコードビットレートは低くなります。

#### フローティングウィンドウのポップアップで強制終了を回避
Android 7.0以降のシステムから、バックグラウンドで実行されている通常のアプリプロセスに切り替わりますが、CPUのアクティビティがある場合、常にシステムによって強制終了されやすくなります。従って、アプリをバックグラウンドに切り替えてサイレントで画面共有すると、フローティングウィンドウのポップアップというソリューションによって強制終了を回避することができます。また、携帯電話の画面にフローティングウィンドウを表示することは、ユーザーが今、画面共有を行っていることをユーザーに知らせ、プライバシー情報の漏えい防止につながります。

- **方法1：通常のフローティングウィンドウをポップアップする**
「VooVMeeting」のようなミニフローティングウィンドウをポップアップするには、サンプルコード[FloatingView.java](https://github.com/tencentyun/TRTCSDK/blob/master/Android/TRTC-API-Example/Basic/ScreenShare/src/main/java/com/tencent/trtc/screenshare/FloatingView.java)の実装を参照すればOKです。
```java
public void showView(View view, int width, int height) {
        mWindowManager = (WindowManager) mContext.getSystemService(Context.WINDOW_SERVICE);
        //TYPE_TOASTは、4.4以降のシステムにのみ適用できます。下位バージョンをサポートするには、TYPE_SYSTEM_ALERTを使用します（manifestで権限を宣言する必要があります）
        //7.1（7.1を含む）以降のシステムは、TYPE_TOASTに対して制限を設けています
        int type = WindowManager.LayoutParams.TYPE_TOAST;
        if (Build.VERSION.SDK_INT > Build.VERSION_CODES.N) {
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

- **方法2：カメラプレビューウィンドウをポップアップする**
TRTC Android版の画面共有は、デスクトップ版のように「サブチャネルの共有」をサポートしていません。従って、画面共有を開始するときは、カメラというチャネルのビデオデータをアップストリームすることはできません。アップストリームすると、衝突が生じます。
では、画面とカメラの画像を同時に共有するにはどうすればよいでしょうか。
答えは簡単です。画面上でカメラの画面をフローティングすればOKです。これをすると、TRTCはスクリーンの画面を収集すると同時に、カメラ画面も共有します。

## 画面共有の確認
- **Mac / Windows画面共有の確認**
  ルームにいるMac / Windowsユーザーが画面共有を起動し、サブストリームを介して共有を実行します。ルームにいるその他ユーザーはTRTCCloudDelegate中の[onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a15be39bb902bf917321b26701e961286)イベントを介してこの通知を受け取ります。
  画面共有を確認したいユーザーは[startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716)インターフェースを介してリモートユーザーのサブストリーム画面のレンダリングを起動することができます。

- **Android/iOS画面共有の確認**
  ユーザーがAndroid/iOSを介して画面共有を実行する場合は、メインストリームを介して共有を実行することができます。ルームにいるその他のユーザーは、TRTCCloudListener内の[onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05)イベントを介してこの通知を受け取ります。
  画面共有を確認したいユーザーは[startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c)インターフェースを介して、リモートユーザーのメインストリーム画面のレンダリングを起動することができます。


```java
//サンプルコード：画面共有の画面を見る
 @Override
 public void onUserSubStreamAvailable(String userId, boolean available) {
    startRemoteSubStreamView(userId);
}
```

## よくあるご質問
 **1つのルームで同時にいくつの画面を共有できますか。**
現在、1つの TRTC オーディオ・ビデオルームで共有できる画面は1つだけです。


