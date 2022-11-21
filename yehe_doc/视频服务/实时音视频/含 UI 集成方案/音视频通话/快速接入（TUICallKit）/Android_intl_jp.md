ここでは、最短の時間でTUICallKitコンポーネントの統合を完了する方法についてご説明します。このドキュメントに沿って操作することで、1時間以内に次の重要手順を完了し、最終的にUIインターフェースを完備したビデオ通話機能を手にすることができます。

## 環境の準備

互換性のある最低バージョンはAndroid 4.1（SDK API Level 16）です。Android 5.0（SDK API Level 21）およびそれ以降のバージョンの使用を推奨します。

Android Studio 3.5およびそれ以降のバージョン（Gradle 3.5.4およびそれ以降のバージョン）。

Android 4.1およびそれ以降のスマートフォンデバイス。

[](id:step1)
##  ステップ1：サービスのアクティブ化

TUICallKitはTencent Cloudの[IM](https://www.tencentcloud.com/document/product/1047)と、[TRTC](https://www.tencentcloud.com/document/product/647)という2つの有料PaaSサービスをベースに構築したオーディオビデオ通信コンポーネントです。以下の手順で関連のサービスをアクティブ化し、7日間の無料トライアルサービスを体験することができます。

1. [IMコンソール](https://console.tencentcloud.com/im)にログインし、**新しいアプリケーションの作成**をクリックし、ポップアップしたダイアログボックスにアプリケーション名を入力して**OK**をクリックします。
![img](https://qcloudimg.tencent-cloud.cn/raw/571d5bed98a46752933169fbf4136271.png)

2. 作成したアプリケーションをクリックし、基本設定ページに進み、ページ右下隅のTRTCサービスのアクティブ化機能エリアで無料体験をクリックすると、TUICallKitの7日間無料トライアルサービスをアクティブ化することができます。正式アプリケーションのリリースが必要な場合は、追加購入をクリックすると購入ページに進むことができます。
![img](https://qcloudimg.tencent-cloud.cn/raw/0860fe4f282d2d918d3911127d85120a.png)

>! IMのオーディオビデオ通話機能は業務ニーズに応じて差別化した有料バージョンをご提供しています。含まれる機能をIM購入ページでご確認の上、ご自身に合ったバージョンを選択してご購入いただけます。

3. 同じページで**SDKAppID**と**キー(SecretKey)**を見つけて記録します。この2つはその後の[ステップ4：TUIコンポーネントへのログイン](#step4)で使用します。
![img](https://qcloudimg.tencent-cloud.cn/raw/5c1b56dc1972d836c85579dd16b0634d.png)


>? お知らせ：**無料体験**をクリックすると、それまでに[TRTC](https://www.tencentcloud.com/document/product/647/35078)サービスを使用したことがある一部のユーザーには、次のような内容が表示されることがあります。

```java
[-100013]:TRTC service is  suspended. Please check if the package balance is 0 or the Tencent Cloud accountis in arrears
```
新しいIMオーディオビデオ通話機能は、Tencent Cloudの[TRTC](https://www.tencentcloud.com/document/product/647/35078)と[IM](https://www.tencentcloud.com/document/product/1047)という2つの基本PaaSサービスを統合したもののため、[TRTC](https://www.tencentcloud.com/document/product/647/35078)の無料利用枠（10000分）が期限切れまたは使用済みの場合、このサービスをアクティブ化しようとすると失敗します。その場合は、[TRTCコンソール](https://console.tencentcloud.com/trtc/app)をクリックし、SDKAppIDに対応するアプリケーション管理ページを見つけ、図のように後払い機能をアクティブ化してから**アプリケーションを有効にする**ことで、オーディオビデオ通話機能を正常に体験することができるようになります。

[](id:step2)
## ステップ2：コンポーネントのダウンロードとインポート

[Github](https://github.com/tencentyun/TUICalling)でコードをクローン/ダウンロードした後、下図のように、Androidディレクトリ下のtuicallkitサブディレクトリを現在のプロジェクトのappの同階層のディレクトリにコピーします。

![img](https://qcloudimg.tencent-cloud.cn/raw/4b6a74f2ee2f5d8eab00061b9fc1f112.png)

[](id:step3)
## ステップ3：プロジェクト設定の完了
1. プロジェクトのルートディレクトリ下で`setting.gradle`ファイルを見つけ、その中に次のコードを追加します。その役割は、[ステップ2](#step2)でダウンロードしたtuicallkitコンポーネントを現在のプロジェクトにインポートするものです。

```java
include ':tuicallkit'
```

2. appディレクトリ下で`build.gradle`ファイルを見つけ、その中に次のコードを追加します。その役割は、現在のappの新たに追加したtuicallkitコンポーネントへの依存を明確に述べるものです。
```java
api project(':tuicallkit')
```
>? TUICallKitプロジェクトの内部はデフォルトで`TRTC SDK`、`IM SDK`、`tuicallengine`およびパブリックコーパスの`tuicore`に依存しており、開発者が単独で設定する必要はありません。バージョンアップが必要な場合は、`tuicallkit/build.gradle`ファイルを変更するだけで済みます。

3. SDKの内部ではJavaのリフレクション機能を使用しているため、 SDK内の一部のクラスに非難読化リストを追加する必要があります。このため、`proguard-rules.pro`ファイルに次のコードを追加する必要があります。
```bash
-keep class com.tencent.** { *; }
```
>! TUICallKitは内部で、カメラ、マイク、ストレージ読み取り権限などの動的申請を補助します。業務上、削減が必要な場合は`tuicallkit/src/main/AndroidManifest.xml`を変更することができます。

[](id:step4)
## ステップ4：TUIコンポーネントへのログイン

プロジェクトに次のコードを追加します。この役割は、TUICore内の関連インターフェースを呼び出して、TUIコンポーネントへのログインを完了することです。ログインに成功しなければTUICallKitの各機能を正常に使用できないため、この手順に異常がないことが重要です。関連のパラメータが正しく設定されているかどうかを注意深く確認してください。
```java
//ログイン結果に対するリスナーを設定します
private final TUILoginListener mLoginListener = new TUILoginListener() {    
    @Override    
    public void onKickedOffline() {        
        super.onKickedOffline();        
        Log.i(TAG, "You have been kicked off the line. Please login again!"); 
        //logout();
    }    
    @Override    
    public void onUserSigExpired() {        
        super.onUserSigExpired();       
        Log.i(TAG, "Your user signature information has expired");        
        //logout();    
    }
};
TUILogin.addLoginListener(mLoginListener);

//ログイン
TUILogin.login(context, 
    1400000001,     // ステップ1で取得したSDKAppIDに置き換えてください
    "denny",        // ご自身のUserIDに置き換えてください
    "xxxxxxxxxxx",  // コンソールでUserSigを計算し、この位置に入力することができます
    new TUICallback() {
    @Override
    public void onSuccess() {
        Log.i(TAG, "login success");
    }

    @Override
    public void onError(int errorCode, String errorMessage) {
        Log.e(TAG, "login failed, errorCode: " + errorCode + " msg:" + errorMessage);
    }
});
```

**パラメータの説明** ここではlogin関数内で使用するいくつかの重要パラメータについて詳しくご説明します。

- **SDKAppID**：ステップ1の最後の段階で取得済みです。ここでは説明を省略します。
- **UserID**：現在のユーザーIDです。文字列タイプでは、アルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。
- **UserSig**：[ステップ1](#step1)の第3段階で取得したSecretKeyを使用してSDKAppID、userIDなどの情報を暗号化し、UserSigを取得します。これは認証用の証明書であり、現在のユーザーがTRTCサービスを使用できるかどうかをTencent Cloudが識別するために用いられます。コンソールの[**支援ツール**](https://console.cloud.tencent.com/im/tool-usersig)で一時的に使用可能なUserSigを生成することができます。

その他の情報については、[UserSigの計算、使用方法](https://www.tencentcloud.com/document/product/647/35166)をご参照ください。

>? **この手順は、現在開発者から最も多くのフィードバックが寄せられる手順でもあります。よくみられる問題には次のようなものがあります。**
- SDKAppIDの設定に誤りがある。国内サイトのSDKAppIDは一般的に140で始まる10桁の整数です。
- UserSigを誤って暗号化鍵（SecretKey）に設定している。UserSigはSecretKeyを使用して、SDKAppID、UserIDおよび有効期限などの情報を暗号化するためのものであり、SecretKeyは直接UserSigに設定するものではありません。
- UserIDが「1」、「123」、「111」などの簡単な文字列で設定されている。**TRTCは同一のUserIDによる複数端末へのログインをサポートしていない**ため、複数人によるコラボレーション開発の場合、「1」、「123」、「111」のようなUserIDは同僚に占有されていることが多く、ログイン失敗につながりやすいです。このため、デバッグの際に、識別度の高いUserIDを設定することをお勧めします。

>! GithubのサンプルコードでgenTestUserSig関数を使用してローカルでUserSigを計算すると、現在のアクセスフローをさらに速くスタートさせることができますが、この方法ではSecretKeyがAppのコード内で開示されてしまい、その後のアップグレードおよびSecretKeyの保護にとって不利益になります。そのため、UserSigの計算ロジックはサーバーに置いて実行し、またAppがTUICallKitコンポーネントを使用するたびに、リアルタイムに計算したUserSigをサーバーにリクエストするようにすることを強く推奨します。

[](id:step5)
## ステップ5：通話する

### 1対1ビデオ通話

TUICallKitのcall関数を呼び出し、 通話タイプと着呼者のuserIdを指定すると、音声またはビデオ通話を開始することができます。
```java
// 1対1ビデオ通話を開始します(UserIDはmikeとします)
TUICallKit.createInstance(context).call("mike", TUICallDefine.MediaType.Video); 
```

| パラメータ          | タイプ                    | 意味                                                  |
| ------------- | ----------------------- | ----------------------------------------------------- |
| userId        | String                  | ターゲットユーザーのUserID：`"mike"`                           |
| callMediaType | TUICallDefine.MediaType | 通話のメディアタイプ。例：`TUICallDefine.MediaType.Video` |

### グループ内ビデオ通話

TUICallKitのgroupCall関数を呼び出し、 通話タイプと着呼者のUserIDリストを指定すると、グループ内で音声またはビデオ通話を開始することができます。
```java
TUICallKit.createInstance(context).groupCall("12345678", Arrays.asList("jane", "mike", "tommy"),TUICallDefine.MediaType.Video);
```

| パラメータ          | タイプ                    | 意味                                                      |
| ------------- | ----------------------- | --------------------------------------------------------- |
| groupId       | String                  | グループID。例：`"12345678"`                               |
| userIdList    | List                    | ターゲットユーザーのUserIDリスト。例：`{"jane", "mike", "tommy"}` |
| callMediaType | TUICallDefine.MediaType | 通話のメディアタイプ。例：`TUICallDefine.MediaType.Video`     |

>? グループの作成の詳細については[IMグループ管理](https://www.tencentcloud.com/document/product/1047/48466)をご参照ください。もしくは[IM TUIKit](https://intl.cloud.tencent.com/document/product/1047/34286)を直接使用し、チャット、通話などのシナリオをワンストップで統合することもできます。

TUICallKitでは現在、グループ以外の多人数ビデオ通話はサポートしていません。もし必要な場合は、colleenyu@tencent.comまでお問い合わせください。

[](id:step6)
## ステップ6：通話に応答する

通話リクエストを受信した後、TUICallKitコンポーネントは着信を通知する応答画面を自動的に呼び出しますが、Androidシステムの権限上の理由により、状況は次のいくつかに分かれます。

- Appがフロントエンドにある場合は、招待を受信した際に呼び出し画面が自動的にポップアップし、着信音が再生されます。
- Appがバックエンドにあっても、`フローティングウィンドウ権限`または`バックエンドポップアップアプリケーション`などの権限が承認されている場合は、呼び出し画面が自動的にポップアップし、着信音が再生されます。
- Appがバックエンドにあり、なおかつ`フローティングウィンドウ権限`または`バックエンドポップアップアプリケーション`などの権限が承認されていない場合は、TUICallKitが着信音を再生し、ユーザーに応答または終了を促します。
- Appのプロセスがすでに破棄されている場合は、[オフライン通知（Android）](https://www.tencentcloud.com/document/product/647/50991)にアクセスし、通知欄のメッセージによってユーザーに応答または終了を促すのみとなります。

[](id:step7)
## ステップ7：その他の特徴

### 1、ニックネーム&プロフィール画像の設定

カスタムニックネームまたはプロフィール画像を設定したい場合は、次のインターフェースを使用して更新できます。
```java
TUICallKit.createInstance(context).setSelfInfo("jack", "https:/****/user_avatar.png", callback);
```

>! ユーザーのプライバシー上の制限により、フレンド以外との通話では、呼ばれるニックネームとプロフィール画像の更新が遅れる可能性があります。一度通話が成功するとスムーズに更新されるようになります。

### 2、オフライン通知

上記の手順が完了すると、オーディオビデオ通話の発信と接続が実現できますが、業務上「アプリケーションのプロセスが強制終了された後」または「アプリケーションがバックエンドに戻った後」もオーディオビデオ通話リクエストを正常に受信できる必要がある場合は、オフライン通知機能を追加する必要があります。詳細については[オフライン通知（Android）](https://www.tencentcloud.com/document/product/647/50991)をご参照ください。

### 3、フローティングウィンドウ機能

業務上、フローティングウィンドウ機能を有効にする必要がある場合は、TUICallKitコンポーネントの初期化の際に次のインターフェースを呼び出してこの機能を有効化することができます。
```java
TUICallKit.createInstance(context).enableFloatWindow(true);
```

### 4、通話ステータスの監視

業務上、通話の開始、終了、通話中のネットワーク品質などの**通話ステータスの監視**が必要な場合は、次のイベントを監視することができます。
```java
TUICallEngine.createInstance(context).addObserver(new TUICallObserver() {
    @Override
    public void onCallBegin(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType, TUICallDefine.Role callRole) {
    }
    public void onCallEnd(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType,TUICallDefine.Role callRole, long totalTime) {
    }
    public void onUserNetworkQualityChanged(List<TUICommonDefine.NetworkQualityInfo> networkQualityList) {
    }
});
```

### 5、カスタム着信音

着信音をカスタマイズしたい場合は、次のインターフェースによって設定できます。

```java
TUICallKit.createInstance(context).setCallingBell(filePath);
```

## よくあるご質問

### 1、「The package you purchased does not support this ability」というエラーが表示されました。

上記のエラーが表示された場合は、現在のアプリケーションのオーディオビデオ通話機能パッケージが期限切れまたはアクティブ化されていないことを表します。[ステップ1：サービスのアクティブ化](#step1)を参照してオーディオビデオ通話機能を取得またはアクティブ化し、引き続きTUICallKitコンポーネントをご利用ください。

### 2、パッケージを購入するにはどうすればよいですか。

購入リンク[オーディオビデオ通話SDK価格一覧](https://www.tencentcloud.com/document/product/647/50553)をご参照ください。その他にご質問がありましたらページ右側をクリックし、パッケージのご購入前にお問い合わせください。もしくはQQグループ：**592465424**に参加し、問い合わせとフィードバックを行うことができます。

### 3、TUICallKitがクラッシュし、クラッシュログが"No implementation found for xxxx"となっています。

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

**TUICallkitは仮想マシンをサポートしていませんので、実機でご体験ください**。実機で上記の異常が生じる原因は、TUICallKitの依存するTRTCなどのSDKの一部インターフェースにJNIを使用しているため、Android Studioがいくつかの条件でAPKコンパイルを行う際にNativeの.soライブラリをパッケージ化できず、このようなエラーが発生します。再Cleanを行ってください。

>? その他のヘルプ情報についての詳細は、[Androidについてのよくあるご質問](https://www.tencentcloud.com/document/product/647/51022)をご参照ください。

## ご意見とフィードバック

ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。