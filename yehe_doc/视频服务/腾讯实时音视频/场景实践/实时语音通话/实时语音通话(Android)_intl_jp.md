## デモンストレーション












音声通話機能をすばやく実装する必要がある場合、当社が提供するDemoをもとにアダプターを修正するか、または当社が提供するTRTCCalling コンポーネントでUIのカスタマイズを実装することができます。

>! 当社は TRTCAudioCall コンポーネントを過去に提供していましたが、旧バージョンのコンポーネントは [コンポーネントリポジトリ](https://github.com/tencentyun/LiteAVClassic) に移動済みです。TRTCCalling コンポーネントはIM シグナリングのインターフェースを使用するため、旧コンポーネントとの互換性がなくなります。

<span id="ui"> </span>

## Demo の UI を再利用

<span id="ui.step1"></span>

### 手順1：アプリケーションの新規作成

1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2．【今すぐ開始】をクリックし、例えば、`TestVideoCall`などアプリケーション名を入力して、【アプリケーションの作成】をクリックします。

>! 本機能はTencent Cloud [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) と [IM](https://intl.cloud.tencent.com/document/product/1047) という2つの基本的な PaaS サービスを同時に使用し、TRTCをアクティブにした後、IM サービスを同期的にアクティブにすることができます。 IM は付加価値サービスであり、請求ルールの詳細については [Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。

<span id="ui.step2"></span>

### 手順2：SDKおよびDemoのソースコードをダウンロード

１．マウスを該当するカードまで移動し、【[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Android)】をクリックしてGithub（または【[ZIP](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip)】をクリック）にジャンプして、関連するSDK および付属のDemoのソースコードをダウンロードします。
   ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. ダウンロード完了後、Tencent Real-Time Communicationコンソールに戻り、【ダウンロードしました。次のステップ】をクリックすれば、SDKAppIDおよびキー情報をクエリできます。

<span id="ui.step3"></span>

### 手順3：Demoプロジェクトファイルの設定

1．[手順2](#ui.step2) でダウンロードしたソースコードパッケージを解凍します。
2.`Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`ファイルを探して開きます。
3．`GenerateTestUserSig.java`ファイルの関連するパラメータを設定します。
   - SDKAPPID：デフォルトは0、実際のSDKAppIDを設定してください。
   - SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。

![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)

4．Tencent Real-Time Communicationコンソールに戻り、【貼り付け完了。次のステップ】をクリックします。
5.【ガイドを閉じてコンソールへ進む】をクリックします。

>!
>-本書で言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになり、そのため**のこの手法はローカルDemo実行および機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166#Server)をご参照ください。

<span id="ui.step4"></span>

### 手順4：Demoの動作

Android Studio（バージョン3.5以上）を使用してソースコードプロジェクトの`TRTCDemo`を開き、【実行】をクリックします。

<span id="ui.step5"></span>

### 手順5：Demo ソースコードの修正

ソースコードフォルダ `trtccallingdemo` には2つのサブファイルui と modelが含まれ、その内、ui フォルダに含まれるのはすべてインターフェースコードです。

| ドキュメントまたはファイル                     | 機能の説明                                                     |
| -------------------------------- | ------------------------------------------------------------ |
| TRTCAudioCallActivity.java       | 音声通話のメインインターフェースを表示し、通話の応答や拒否はこのインターフェースで完了します。 |
| TRTCCallingEntranceActivity.java | 連絡先を選択するためのインターフェースを表示するために使用され、このインターフェースを介して登録済みユーザーを検索し、通話を開始できます。 |
| audiolayout                      | 通話中のユーザー画面のレンダリングと配列ロジックのために使用されます。                     |

<span id="model"> </span>

## UIカスタマイズの実装

[ソースコード] フォルダ `trtccallingdemo` 中には2つのサブフォルダ ui と modelが含まれ、その内、 model フォルダには当社が実装した再利用可能なオープンソースコンポーネント TRTCCallingが含まれています。 このコンポーネントが提供するインターフェース関数は`TRTCCalling.java`  ファイルで確認できます。
![](https://main.qcloudimg.com/raw/78cc06cd53538243bc52abc381350c55.jpg)

オープンソースコンポーネント TRTCCalling を使用して自身の UIを実装することができます。つまり model パーツを再利用するだけで、自身で UI パーツを実装できます。

<span id="model.step1"> </span>

### 手順1： SDKへの統合

オーディオビデオ通話コンポーネント TRTCCallingは、TRTC SDK と IM SDKに依存し、次の手順で2つの SDKをプロジェクトに統合することができます。

**方法一：Mavenリポジトリを介した依存**

1. dependencies にTRTC SDK と IM SDK の依存を追加します。
```
dependencies {
	complie "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    complie 'com.tencent.imsdk:imsdk:latest.release'

	// 当社は gson 解析を使用していますので、さらにgoogle の Gsonに依存する必要はありません。
    complie 'com.google.code.gson:gson:latest.release'
}
```
>?2つの SDK 製品の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK) と [IM](https://github.com/tencentyun/TIMSDK) の Github トップページで取得することができます。

2.  defaultConfig で App が使用する CPU アーキテクチャを指定します。
```
defaultConfig {
    ndk {
        abiFilters "armeabi-v7a"
    }
}
```
3. 【Sync Now】をクリックし、 SDKを同期します。
>?jcenterへのネットワーク接続に問題がない場合、SDKは自動的にダウンロードされ、プロジェクトに統合されます。


**方法二：ローカル AARを介した依存**
開発環境でのMavenリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。

| SDK      | ダウンロードページ                                                     | 統合ガイド                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK   | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/1047/34306) |

<span id="model.step2"> </span>

### 手順2：権限の設定および難読化ルール

AndroidManifest.xml にAppの権限を設定します。SDKには次の権限が必要です（6.0以上の Android システムではカメラ、読み取りストレージの権限を動的に申請する必要があります）。

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

 proguard-rules.pro ファイルでは、 SDK 関連を非難読化リストに追加します。

```
-keep class com.tencent.** { *; }
```

<span id="model.step3"> </span>

### 手順3：TRTCCalling コンポーネントをインポート

次のディレクトリ内のすべてのファイルをプロジェクトにコピーします。

```
trtccallingdemo/src/main/java/com/tencent/liteav/trtccalling/model 
```

<span id="model.step4"> </span>

### 手順4：コンポーネントの初期化およびログイン

1.  `TRTCCallingImpl.sharedInstance(context)`をコールしコンポーネントインスタンスを取得します。
2.  `login(SDKAppID, userId, userSig, callback)`をコールし コンポーネントのログインを完了します。なおいくつかの重要パラメータの入力については下表をご参照ください。
 <table>
<tr>
<th>パラメータ名</th>
<th>作用</th>
</tr>
<tr>
<td>SDKAppID</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">Tencent Real-Time Communicationコンソール</a> で SDKAppIDを表示できます。</td>
</tr>
<tr>
<td>userId</td>
<td>現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。計算方法については<a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSigの計算方法</a>をご参照ください。</td>
</tr>
</table>
<pre>
// 初期化
sCall = TRTCCallingImpl.sharedInstance(context);
sCall.login(1400000123, "userA", "xxxx", new ActionCallback());
</pre>


<span id="model.step5"> </span>

### 手順5： 1v1 音声通話の実現

1. 発信者： `TRTCCalling` の `call()` メソッドをコールして通話リクエストを開始し、ユーザーID（userid）と通話タイプ（type）を渡して、通話タイプパラメータを`TYPE_AUDIO_CALL`に渡します。
2. 受信者：受信者がログイン状態の場合は、 `onInvited()` という名称のイベント通知を受け取ります。受信者がログインしていない状態でも通話リクエストを受け取りたい場合は、[オフライン応答](#model.offline)をご参照ください。
3. 受信者：通話に応答したい場合、受信者は `accept()`関数をコールします。また `reject()`をコールし、この通話を拒否することもできます。
4. 双方の音声およびビデオチャネルが確立した後、通話する双方はいずれも `onUserEnter()` という名称のイベント通知を受け取ります。このことは、双方が通話に参加したことを意味します。

```
//1. コンポーネントの初期化
TRTCCalling sCall =  TRTCCallingImpl.sharedInstance(context);
//2. 監視装置の登録
sCall.addDelegate(new TRTCCallingDelegate() {
    //...一部の監視コードを省略
    public void onInvited(String sponsor, final List<String> userIdList, boolean isFromGroup, int callType) {
        // sponsorからの通話リクエストを受け取り、ここのコードで応答を選択します。 reject()をコールして通話を拒否することもできます。
        sCall.accept();
    } 
});
//3. コンポーネントのログイン完了。ログイン成功後にコンポーネントの他の機能関数をコールすることができます
sCall.login(sdkappid, "aaa", usersig, new ActionCallback() {
    public void onSuccess() {
        //4. インスタンスコード：コンポーネントでログインに成功した後、ユーザー“aaa”を呼び出し、タイプをTYPE_AUDIO_CALLと入力します
        sCall.call("aaa"，TRTCCalling.TYPE_AUDIO_CALL);
    }
});
```

<span id="model.step6"> </span>

### 手順6：多人数音声通話を実装

1. 発信者：多人数のビデオ通話では、`TRTCCalling` の `groupCall()` 関数をコールし 、ユーザーリスト（userIdList）、通話タイプ（type）、 IM 群组 ID（groupId）を入力する必要があります。なお userIdList は入力必須パラメータ、通話タイプは`TYPE_AUDIO_CALL`に渡す入力必須パラメータで、groupId はオプションパラメータです。
2. 受信者：`onInvited()`というイベント通知を介して呼び出しリクエストを受け取ることができます。
3. 受信者：イベント通知を受け取った後、`accept()` メソッドをコールし、この通話に応答することができます。`reject()` メソッドをコールして通話の拒否を選択することもできます。
4. 一定時間（デフォルトは30s）を超えて応答しなかった場合、受信者は `onCallingTimeOut()` のイベント通知を受け取り、発信者は`onNoResp(String userId)` というイベント通知を受け取ります。通話発信者が複数の着信に応答しない場合は `hangup()`のイベント通知を受け取り 、各受信者は `onCallingCancel()`という イベント通知を受け取ります。
5. 現在の多人数の通話から退出したい場合は、`hangup()` 方法をコールします。
6. 通話中にユーザーが途中参加し、または退出する場合、他のユーザーは `onUserEnter()` または  `onUserLeave()` というイベント通知を受け取ります。

>?インターフェース `groupCall()` における `groupID` パラメータは IM SDKにおけるグループ IDです。このパラメータを設定すると、通話リクエストメッセージがグループメッセージシステムを介してブロードキャストされます。このメッセージブロードキャスト方式は簡単で信頼性の高い方法です。設定しない場合は、`TRTCCalling` コンポーネントが単発メッセージで1人1人に通知を行います。

```
// 前記省略...
// ダイヤルするユーザーリストをまとめます
List<String> callList = new ArrayList();
callList.add("bbb");
callList.add("ccc");
callList.add("ddd");
// あるIM グループ内で開始されていない場合は、groupIdを空文字列とすることができます。
sCall.groupCall(callList, TRTCCalling.TYPE_AUDIO_CALL, "");
```

<span id="model.offline"> </span>

### 手順7：オフライン応答の実装

>?ビジネスの位置付けがオンラインカスタマーサービスなどのオフライン応答機能を必要としないシーンである場合は、上記[手順1]（＃model.step1）-[手順6]（＃model.step6）の対応で問題ありません。 しかし、ビジネスの位置付けがソーシャルシーンである場合は、オフライン応答を実装することをお勧めします。

IM SDK はオフラインプッシュをサポートしていますが、Android の各スマートフォンメーカーは各自のオフラインプッシュサービスを備えていることから、iOS プラットフォームよりアクセスが複雑となり、利用基準を満たすためには、相応の設定を行う必要があります。

1. 対応するメーカーのプッシュチャネルに必要な証明書などを申請の上、 IM コンソール内に設定し、プッシュ要件に従って証明書とIDなどを追加します。詳細な操作手順については [IM > オフラインプッシュ（Android） ](https://intl.cloud.tencent.com/document/product/1047/34336)をご参照ください。
2. 現在 TRTCCallingImpl の sendModel シグナリング送信関数にオフライン送信関数が統合されており、App のオフラインプッシュを設定した後、メッセージのオフラインプッシュを実装することができます。

<span id="api"> </span>

## コンポーネント API リスト

TRTCCalling コンポーネントの API インターフェースリストは次のとおりです。

| インターフェース関数        | インターフェースの機能                                                  |
| --------------- | --------------------------------------------------------- |
| addDelegate     | TRTCCalling 監視装置を追加します。ユーザーはこの監視装置を介して状態通知を取得します |
| removeDelegate  | 監視装置を削除します                                                |
| destroy         | インスタンスを廃棄します                                                  |
| login           | IMにログインします。すべての機能を使用するためには、まずログインする必要があります                |
| logout          | IMからログアウトします。ログアウト後はダイヤル操作ができません                         |
| call            | C2C の通話に招待します、被招待者は onInvited のイベント通知を受け取ります         |
|groupCall       | IM グループの通話に招待します、被招待者は onInvited のイベント通知を受け取ります     |
| accept          | 被招待者として通話に応答します                                      |
| reject          | 被招待者として通話を拒否します                                      |
| hangup          | 通話を終了します                                                  |
| startRemoteView | リモートユーザーのカメラデータを指定の TXCloudVideoView にレンダリングします    |
| stopRemoteView  | 任意のリモートユーザーのカメラデータ のレンダリングを停止します                         |
|openCamera      | カメラを起動し、指定の TXCloudVideoView にレンダリングします            |
| closeCamera     | カメラを終了します                                               |
| switchCamera    | 前後カメラを切り替えます                                            |
| setMicMute      | micをミュート/非ミュートに設定します                                              |
| setHandsFree    | ハンズフリーを起動するかどうかを設定します                                              |
