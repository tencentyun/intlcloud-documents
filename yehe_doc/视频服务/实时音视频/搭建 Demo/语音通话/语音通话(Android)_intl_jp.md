## デモンストレーション
Appを[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)してインストールすると、TRTC通話の効果を体験できます。
<table>
<tr>
   <th>発呼側</th>
   <th>着呼側</th>
 </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/7b03f80d5ad33bd33b6fb551e392b4d3.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/60581f007dda722e06af6333b13afbd4.jpeg"/></td>
</tr>
</table>



>! オーディオビデオ通話機能を素早く実装できるように、当社はTUICallingコンポーネントをリモデルし、通話UIをTUICallingコンポーネントの内部に実装しました。お客様がUIに気をつかう必要はありません。

[](id:ui)

## Appの実行と体験

[](id:ui.step1)

### 手順1：アプリケーションの新規作成
1. TRTCコンソールにログインし、**開発支援>[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)**を選択します。
2．アプリケーション名（例：`TestVideoCall`）を入力して、**作成**をクリックします。
3. **ダウンロードしました。次のステップ**をクリックすると、この手順をスキップします。

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>! 本機能はTencent Cloud[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。


[](id:ui.step2)
### 手順2：Appソースコードのダウンロード
クリックして[TUICalling](https://github.com/tencentyun/TUICalling)に進み、ソースコードをCloneまたはダウンロードします。

[](id:ui.step3)
### 手順3：Appプロジェクトファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`のファイルを見つけて開きます。
3. `GenerateTestUserSig.java`ファイル内の関連パラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトはプレースホルダー(PLACEHOLDER)。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトはプレースホルダー(PLACEHOLDER)。実際のキー情報を設定してください。</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 貼り付け完了後、**貼り付けました。次のステップ**をクリックすれば、作成が完了します。
5. コンパイル完了後、 **コンソール概要に戻る** をクリックすれば終了です。

>!
>- ここで言及するUserSigの発行方法は、クライアントコードの中でのSECRETKEY設定となりますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのAppクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)
### 手順4：Appの実行

Android Studio（バージョン3.5以降）を使用してソースコードプロジェクト`TUICalling`を開き、**実行**をクリックすれば、このAppのデバッグが開始されます。



## 体験アプリケーション
>! 体験アプリケーションには、少なくとも2台のデバイスが必要です。

### ユーザーA
1. ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. 電話をかけたいuserIdを入力し、検索をクリックします。
3. **呼出**をクリックし、**ビデオ通話**を選択して電話をかけます（**着呼者がアプリケーション内にいることを保証してください。保証できない場合、電話をかけても失敗する可能性があります**）。<br>

### ユーザーB
1. ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. メインページに進み、通話応答を待ちます。



[](id:model)
## 具体的な接続フロー

[ソースコード](https://github.com/tencentyun/TUICalling/tree/master/Android/Source/src/main/java/com/tencent/liteav/trtccalling)の`Source`フォルダの中にはuiとmodelの2つのサブフォルダが含まれています。そのうち、modelフォルダには外部に公開しているオープンソースコンポーネントTUICallingManagerが含まれています。`TUICalling.java`ファイルの中でこのコンポーネントが提供するインターフェース関数を見つけることができます。
![](https://qcloudimg.tencent-cloud.cn/raw/0de26d679e6e0dc1d9aeadb6dbf6f8aa.png)


オープンソースコンポーネントTUICallingのTUICallingManagerをそのまま使用し、オーディオビデオ通話機能を手軽に実装することができます。もう複雑な通話UIやロジックの実装をご自身で行う必要はありません。

[](id:model.step1)
### 手順1：SDKの統合 

オーディオビデオ通話コンポーネントTUICallingは、TRTC SDKとIM SDKに依存しています。次の手順で2つのSDKをプロジェクトに統合することができます。

#### 方法1：MavenCentralリポジトリを介する依存

1. dependenciesにTRTCSDKとIMSDKの依存を追加します。
<dx-codeblock>
::: java java
dependencies {
    compile "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    compile 'com.tencent.imsdk:imsdk:latest.release'

    // 当社はgson解析を使用していますので、さらにgoogle のGsonに依存する必要はありません。
    compile 'com.google.code.gson:gson:latest.release'
}
:::
</dx-codeblock>
>?2つのSDK製品の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK)と[IM](https://github.com/tencentyun/TIMSDK) のGithubトップページで取得することができます。
2. defaultConfigでAppが使用するCPUアーキテクチャを指定します。
<dx-codeblock>
::: java java
defaultConfig {
      ndk {
            abiFilters "armeabi-v7a"
      }
}
:::
</dx-codeblock>
3. **Sync Now**をクリックし、SDKを同期します。
>? mavenCentralへのネットワーク接続に問題がない場合、SDKは自動的にダウンロードされ、プロジェクトに統合されます。


#### 方法2：ローカルAARを介する依存
開発環境でのmavenCentralリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。

| SDK      | ダウンロードページ                                                     | 統合ガイド                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK   | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/1047/34306) |

[](id:model.step2)

### 手順2：権限の設定および難読化ルール

AndroidManifest.xmlにAppの権限を設定します。SDKには次の権限が必要です（6.0以上のAndroidシステムではカメラ、読み取りストレージの権限を動的に申請する必要があります）。

```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```

proguard-rules.proファイルでは、SDK関連を非難読化リストに追加します。

```
-keep class com.tencent.** { *; }
```

[](id:model.step3)

### 手順3：TUICallingコンポーネントをインポート

Sourceディレクトリをプロジェクトにコピーし、 `setting.gradle`へのインポートを完了します。以下をご参照ください。

```
include ':Source'
```

[](id:model.step4)

### 手順4：コンポーネントの初期化およびログイン

1. `TUICallingManager.sharedInstance()`を呼び出し、コンポーネントを初期化します。
2. `TUILogin.init(context, SDKAppID, config, listener)`を呼び出し、ログインを初期化します。
3. `TUILogin.login(userId, userSig, callback)`を呼び出し、コンポーネントのログインを完了します。このうちの重要なパラメータの入力については、下表をご参照ください。
 <table>
<tr><th>パラメータ名</th><th>作用</th></tr>
<tr>
<td>SDKAppID</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> で SDKAppIDを表示できます。</td>
</tr><tr>
<td>userId</td>
<td>現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。業務の実際のアカウントシステムと組み合わせてご自身で設定することをお勧めします。</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。計算方法については<a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSigの計算方法</a>をご参照ください。</td>
</tr>
</tr><tr>
<td>config</td>
<td>SDKの設定。ログレベルおよびログコールバック（nullを渡すことも可能）の設定に使用します。詳細については、下記サンプルコードをご参照ください。</td>
</tr><tr>
</tr><tr>
<td>listener</td>
<td>IMリスナー。いくつかの必要なシステムコールバック通知の受信に使用します。例：キックアウトによるオフライン、userSig期限切れなど。詳細については、下記サンプルコードをご参照ください。</td>
</tr><tr>
</tr><tr>
<td>callback</td>
<td>ログイン結果リスナー。ログイン成功の有無を通知します。詳細については、下記サンプルコードをご参照ください。</td>
</tr><tr>
</table>
<dx-codeblock>
::: java java
     // コンポーネントの初期化
     TUICallingManager manager = TUICallingManager.sharedInstance();
  // ログイン
  V2TIMSDKConfig config = new V2TIMSDKConfig();
  config.setLogLevel(V2TIMSDKConfig.V2TIM_LOG_DEBUG);
  config.setLogListener(new V2TIMLogListener() {
        @Override
        public void onLog(int logLevel, String logContent) {
                
        }
  });
  TUILogin.init(this, ${あなたのSDKAPPID}, config, new V2TIMSDKListener() {

            @Override
            public void onKickedOffline() {  //  ログインがキックアウトされたオフライン通知
                mIsKickedOffline = true;
                checkUserStatus();
            }
    
            @Override
            public void onUserSigExpired() { // suerSig期限切れ通知
                mIsUserSigExpired = true;
                checkUserStatus();
            }
  });
  TUILogin.login("${あなたのuserId}", "${あなたのuserSig}", new V2TIMCallback() {
            @Override
            public void onError(int code, String msg) {
                Log.d(TAG, "code: " + code + " msg:" + msg);
            }

            @Override
            public void onSuccess() {
                Log.d(TAG, "onSuccess");
            }
  });

:::
</dx-codeblock>

[](id:model.step5)

### 手順5：オーディオビデオ通話の実装

1. 発信側：TUICallingManagerの`call();`メソッドを呼び出して通話リクエストを送信し、ユーザーIDの配列（userids）と通話タイプ（type）を渡します。通話タイプパラメータは`TUICalling.Type.AUDIO`（オーディオ通話）または`TUICalling.Type.VIDEO`（ビデオ通話）を渡します。ユーザーID配列（userids）のuserIdが1つのみの時は、シングル通話と見なされ、ユーザーID配列（userids）のuserIdが複数（>=2）の時は多人数通話と見なされます。
2. 受信側：受信側がログイン状態の場合は、対応するインターフェースが自動的に起動します。受信側がログインしていない状態でも通話リクエストを受け取りたい場合は、[オフライン応答](#model.offline)をご参照ください。


<dx-codeblock>
::: java java
// 1. コンポーネントの初期化
TUICallingManager manager = TUICallingManager.sharedInstance();
// 2. リスナーの登録
manager.setCallingListener(new TUICalling.TUICallingListener() {
            @Override
            public boolean shouldShowOnCallView() {
                return true;
            }

            @Override
            public void onCallStart(String[] userIDs, TUICalling.Type type, TUICalling.Role role, final View tuiCallingView) {
                if (!shouldShowOnCallView() || null == tuiCallingView) {
                    return;
                }
                runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        FrameLayout.LayoutParams params = new FrameLayout.LayoutParams(FrameLayout.LayoutParams.MATCH_PARENT, FrameLayout.LayoutParams.MATCH_PARENT);
                        mCallingView = tuiCallingView;
                        addContentView(tuiCallingView, params);
                    }
                });
            }
    
            @Override
            public void onCallEnd(String[] userIDs, TUICalling.Type type, TUICalling.Role role, long totalTime) {
                removeView();
            }
    
            @Override
            public void onCallEvent(TUICalling.Event event, TUICalling.Type type, TUICalling.Role role, String message) {
                if (TUICalling.Event.CALL_FAILED == event) {
                    removeView();
                }
            }
});
// 3.電話をかけます
manager.call(userIDs, TUICalling.Type.VIDEO);
:::
</dx-codeblock>

[](id:model.offline)

### 手順6：オフライン応答の実装

>?ビジネスの位置付けがオンラインカスタマーサービスなどのオフライン応答機能を必要としないシーンである場合は、上記[手順1]（＃model.step1）-[手順5]（＃model.step5）の対応で問題ありません。 しかし、ビジネスの位置付けがソーシャルシーンである場合は、オフライン応答を実装することをお勧めします。

IM SDKはオフラインプッシュをサポートしていますが、Androidの各スマートフォンメーカーは各自のオフラインプッシュサービスを備えていることから、iOSプラットフォームよりアクセスが複雑となり、利用基準を満たすためには、相応の設定を行う必要があります。

1. 対応するメーカーのプッシュチャネルに必要な証明書などを申請の上、IMコンソール内に設定し、プッシュ要件に従って証明書とIDなどを追加します。詳細な操作手順については、[IM > オフラインプッシュ（Android） ](https://intl.cloud.tencent.com/document/product/1047/39156)をご参照ください。
2. 現在、TRTCCallingImplのsendModelシグナリング送信関数にオフライン送信関数が統合されており、Appのオフラインプッシュを設定した後、メッセージのオフラインプッシュを実装することができます。

[](id:api)

## コンポーネントAPIリスト

TUICallingコンポーネントのAPIインターフェースリストは次のとおりです。

| インターフェース関数        | インターフェースの機能                                                 |
| --------------- | --------------------------------------------------------- |
| call            | C2C通話に招待します         |
| receiveAPNSCalled          | 被招待者として着信に応答します                                      |
| setCallingListener          | リスナーを設定します                                     |
| setCallingBell          | 着信音の設定(30s以内を推奨)                                                 |
| enableMuteMode | ミュートモードをオンにします    |
| enableCustomViewRoute      | カスタムビューをオンにします。オンにすると、呼び出し/被呼び出し開始コールバックの中で、CallingViewのインスタンスを受信します。開発者自身が表示方式を決定します。注意：フルスクリーンまたはスクリーンと同じ比率で表示する必要があります。そうしない場合、表示に異常が生じます            |

