### TUICallKitでIM SDKをインポートせず、TRTCだけを使用することはできますか。

**できません**。TUIKit全シリーズのコンポーネントはすべて、通信の基本サービス、例えば通話発信シグナル、通話中シグナルなどのコアロジックにTencent Cloud IM SDKを使用しています。他のIM製品をご購入済みの場合は、TUICallKitロジックを参照して適合させることも可能です。

### 「The package you purchased does not support this ability」というエラーが表示されました。

上記のエラーが表示された場合は、現在のアプリケーションのオーディオビデオ通話機能パッケージが期限切れまたはアクティブ化されていないことを表します。[ステップ1：サービスのアクティブ化](https://www.tencentcloud.com/document/product/647/50991#step1)を参照してオーディオビデオ通話機能を取得またはアクティブ化し、引き続きTUICallKitコンポーネントをご利用ください。

### TUICallKitがクラッシュし、クラッシュログが"No implementation found for xxxx"となっています。

スタック情報は次のとおりです。

```java
java.lang.UnsatisfiedLinkError: No implementation found for void com.tencent.liteav.base.Log.nativeWriteLogToNative(int, java.lang.String, java.lang.String) (tried Java_com_tencent_liteav_base_Log_nativeWriteLogToNative and Java_com_tencent_liteav_base_Log_nativeWriteLogToNative__ILjava_lang_String_2Ljava_lang_String_2)
       at com.tencent.liteav.base.Log.nativeWriteLogToNative(Native Method)
       at com.tencent.liteav.base.Log.i(SourceFile:177)
       at com.tencent.liteav.basic.log.TXCLog.i(SourceFile:36)
       at com.tencent.liteav.trtccalling.model.impl.base.TRTCLogger.i(TRTCLogger.java:15)
       at com.tencent.liteav.trtccalling.model.impl.ServiceInitializer.init(ServiceInitializer.java:36)
       at com.tencent.liteav.trtccalling.model.impl.ServiceInitializer.onCreate(ServiceInitializer.java:101)
       at android.content.ContentProvider.attachInfo(ContentProvider.java:2097)
       at android.content.ContentProvider.attachInfo(ContentProvider.java:2070)
       at android.app.ActivityThread.installProvider(ActivityThread.java:8168)
       at android.app.ActivityThread.installContentProviders(ActivityThread.java:7709)
       at android.app.ActivityThread.handleBindApplication(ActivityThread.java:7573)
       at android.app.ActivityThread.access$2600(ActivityThread.java:260)
       at android.app.ActivityThread$H.handleMessage(ActivityThread.java:2435)
       at android.os.Handler.dispatchMessage(Handler.java:110)
       at android.os.Looper.loop(Looper.java:219)
       at android.app.ActivityThread.main(ActivityThread.java:8668)
       at java.lang.reflect.Method.invoke(Native Method)
       at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:513)
       at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1109)
```

>! **TUICallkitは仮想マシンをサポートしていませんので、実機でご体験ください**。実機で上記の異常が生じる原因は、TUICallKitの依存するTRTCなどのSDKの一部インターフェースにJNIを使用しているため、Android Studioがいくつかの条件でAPKコンパイルを行う際にNativeの.soライブラリをパッケージ化できず、このようなエラーが発生します。再Cleanを行ってください。

### allowBackupの異常が発生しました。

**エラーメッセージ**：`Manifest merger failed : Attribute application@allowBackup value=(true) from AndroidManifest.xml`

**問題の原因**：TUICallKitが依存するIM SDKではデフォルトのallowBackupの値はfalseであり、これはアプリケーションのバックアップと復元機能が無効になっていることを意味します。

**対処方法**：プロジェクトの`AndroidManifest.xml`ファイルからallowBackup属性を削除するか、またはこの属性をfalseに変更し、バックアップと復元機能が無効にすることができます。また、`AndroidManifest.xml`ファイルのapplicationノードに`tools:replace="android:allowBackup"`を追加することもでき、これはIM SDKの設定を上書きし、ご自身の設定を使用することを意味します。

### TUICallKitはオフラインプッシュをサポートしていますか。

**サポートしています**。AndroidのオフラインプッシュはTencent CloudのTUIOfflinePushコンポーネントを使用しています。詳細については、[TUIOfflinePush](https://www.tencentcloud.com/document/product/1047/39156)をご参照ください。[TUICallKit](https://github.com/tencentyun/TUICalling/tree/main/Android)コンポーネントにもこのコンポーネントが接続されています。

### 通話招待のタイムアウト時間内に、被招待者がオフラインから再びオンラインとなった場合、通話画面をポップアップさせることはできますか。

Appの起動タイプによって状況がそれぞれ異なります。

![img](https://qcloudimg.tencent-cloud.cn/image/document/f4b8ab415785fb5274e2f6cc709254fc.png)

オフラインから再びオンラインとなった際に通話画面がポップアップしなかった場合は、`onReceiveNewInvitation`ログをフィルタリングし、メッセージ履歴にプルしていないかどうかを確認してください。このログプリントがない場合は、[お問い合わせ](https://intl.cloud.tencent.com/contact-us)ください。

### アプリケーションがバックエンドにあるとき、通話画面をフロントエンドに自動的にプルできません

**アプリケーションをバックエンドからフロントエンドに自動的にプルする場合、Appが「バックエンド自動起動」または「フローティングウィンドウ」権限を有効にしているかどうかを確認する必要があります。**

メーカーが異なる場合や、同じメーカーであってもAndroidのバージョンが異なる場合は、アプリケーションに許可する権限や権限名が一致しないことがありますのでご注意ください。例えば、Xiaomi 6ではバックエンドの画面ポップアップ権限を有効にすればよいだけですが、Redmiではバックエンド画面ポップアップとフローティングウィンドウの権限を同時に有効にする必要があります。

>? テスト中に手動ですべての権限を有効化しても、通話画面のフロントエンドへの自動プルができない場合は、メーカー間の互換性の問題がある可能性があります。
