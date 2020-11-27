## デモンストレーション
[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)して、Demoをインストールすると、ILVBの機能の効果を体験していただくことができます。これにはマイク接続によるコラボライブ、キャスター同士のPK、低遅延の視聴、弾幕チャットなど、TRTCのインタラクティブライブストリーミングシーンにおける関連機能が含まれています。

ILVBの機能をすばやく実装する必要がある場合、当社が提供するDemoをもとに直接修正を加えてフィットさせることも、当社が提供するTRTCLiveRoom コンポーネントを使用し、カスタマイズしたUIを実現することも可能です。

<span id="DemoUI"> </span>
## Demo の UI の再利用

<span id="ui.step1"></span>
### 手順1：アプリケーションの新規作成
1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. 【今すぐスタート】をクリックし、例えば、`TestLiveRoom`などアプリケーション名を入力して、【アプリケーション作成】をクリックします。

>本機能は [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) と [IM](https://intl.cloud.tencent.com/document/product/1047) という2つの基本的な PaaS サービスを同時に使用し、TRTCをアクティブにした後、IM サービスを同期的にアクティブにすることができます。 IM は付加価値サービスであり、請求ルールの詳細については [Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。

<span id="ui.step2"></span>
### 手順2：SDKおよびDemoのソースコードをダウンロード
１．マウスを該当するカードまで移動し、【[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Android)】をクリックしてGithub（または【[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip】をクリック）にジャンプして、関連するSDK および付属のDemoのソースコードをダウンロードします。
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. ダウンロード完了後、Tencent Real-Time Communicationコンソールに戻り、【ダウンロードしました。次のステップ】をクリックすれば、SDKAppIDおよびキー情報をクエリできます。

<span id="ui.step3"></span>
### 手順3：Demoプロジェクトファイルの設定
1．[手順2](#ui.step2) でダウンロードしたソースコードパッケージを解凍します。
2.`Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`ファイルを探して開きます。
3．`GenerateTestUserSig.java`ファイルの関連するパラメータを設定します。
  <ul><li>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</li></ul> 
    <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4．Tencent Real-Time Communicationコンソールに戻り、【貼り付け完了。次のステップ】をクリックします。
5.【ガイドを閉じてコンソールへ進む】をクリックします。

≻本書で言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになり、そのため**この手法はローカルDemo実行および機能デバッグにのみ適合します**。
≻ UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

<span id="ui.step4"></span>
### 手順4：Demoの動作
Android Studio（バージョン3.5以上）を使用してソースコードの`TRTCScenesDemo`プロジェクトを開き、【実行】をクリックすれば、本Demoのデバックが開始されます。

<span id="ui.step5"></span>
### 手順5：Demo ソースコードの修正
ソースコードの trtcliveroomdemo フォルダは、 ui と modelの2つのサブフォルダを含んでいます。ui フォルダにはインターフェースコードが含まれています。以下の表にはファイルまたはフォルダ及び対応する UIをリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ | 機能説明 |
|:-------:|:--------|
| anchor | キャスター側に関するUIの実装コード。 |
| audience | 視聴者側に関するUIの実装コード。 |
| common | 一般的なUIコンポーネントの実装コード。 |
| liveroomlist | ルームリスト画面の実装コード。 |
| widget | 一般的なウィジェット。 |

<span id="model"> </span>
## UIカスタマイズの実装

[ソースコード](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCScenesDemo/trtcliveroomdemo/src/main/java/com/tencent/liteav/liveroom)  のtrtcliveroomdemo フォルダには、 ui と modelの2つのサブフォルダがあり、model フォルダには再利用できるオープンソースコンポーネント TRTCLiveRoomがあります。`TRTCLiveRoom.java`ファイルでこのコンポーネントが提供するインターフェース関数を見て、対応するインターフェースを使用して UI のカスタマイズを実現することができます。
![](https://main.qcloudimg.com/raw/710358e4e170d44304cdb9bc991ad209.jpg)

<span id="model.step1"> </span>
### 手順1： SDKへの統合
オーディオビデオ通話コンポーネントTRTCLiveRoom は、TRTC SDK と IM SDKに依存し、次の手順で2つの SDKをプロジェクトに統合することができます。

**方法一：Mavenリポジトリを介した依存**
1. dependencies に TRTCSDKと IMSDK の依存を追加します。
```
dependencies {
       complie "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       complie 'com.tencent.imsdk:imsdk:latest.release'
}
```
>2つの SDK の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK) および [IM](https://github.com/tencentyun/TIMSDK) の Github トップページで取得することができます。
>
2.  defaultConfig で App が使用する CPU アーキテクチャを指定します。
```
defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
}
```
3．【Sync Now】をクリックし、自動でSDKをダウンロードし、プロジェクトに統合します。

**方法二：ローカル AARを介した依存**
開発環境でのMavenリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。
<table>
<tr>
<th>SDK</th>
<th>ダウンロードページ</th>
<th>統合ガイド</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">統合ドキュメント</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">統合ドキュメント</a></td>
</tr>
</table>

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
-keep class com.tencent.** { *;}
```

<span id="model.step3"> </span>
### 手順3： TRTCLiveRoom  コンポーネントをインポート
次のディレクトリ内のすべてのファイルをプロジェクトにコピーします。
```
src/main/java/com/tencent/liteav/liveroom/model
```

<span id="model.step4"> </span>
### 手順4：コンポーネントの作成およびログイン
1. `sharedInstance`インターフェースをコールすると、 TRTCLiveRoom コンポーネントのインスタンスオブジェクトを作成できます。
2. 1つの`TRTCLiveRoomConfig`オブジェクトを作成したら、このオブジェクトにuseCDNFirstとCDNPlayDomainの属性を設定することができます。
 - useCDNFirstの属性：視聴者の視聴方式の設定に使用します。trueは、普通の視聴者のCDN経由での視聴を表し、費用は安価ですがディレーは高めです。falseは、普通の視聴者の低遅延による視聴を表し、費用は CDN とマイク接続の間ですが、ディレーを1s以内に抑えることができます。
 - CDNPlayDomainの属性：useCDNFirstの設定をtrueにした時に有効になり、CDN経由の視聴の再生ドメイン名の指定に利用します。ライブストリーミングコンソール >【[Domain Management](https://console.cloud.tencent.com/live/domainmanage)】の画面からログインし、設定することができます。
3. `login`関数をコールしてコンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
 <table>
<tr>
<th>パラメータ名</th>
<th>作用</th>
</tr>
<tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">Tencent Real-Time Communicationコンソール</a> で SDKAppIDを表示できます。</td>
</tr>
<tr>
<td>userId</td>
<td>現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については<a href="https://intl.cloud.tencent.com/document/product/647/35166"> UserSig</a>の計算方法をご参照ください。</td>
</tr>
<tr>
<td>config</td>
<td>グローバルコンフィギュレーション情報。ログイン時に初期化してください。ログイン後は変更できなくなります。<ul style="margin:0;">
<li>視聴者の視聴方式の設定に使用します。trueは、普通の視聴者のCDN経由での視聴を表し、費用は安価ですがディレーは高めです。falseは、普通の視聴者の低遅延による視聴を表し、費用は CDN とマイク接続の間ですが、ディレーを1s以内に抑えることができます。</li>
<li>CDNPlayDomain 属性：useCDNFirstの設定をtrueにした時に有効になり、CDN経由の視聴の再生ドメイン名の指定に利用します。ライブストリーミングコンソール >【<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>】の画面からログインして設定を行うことができます。</li>
</ul></td>
</tr>
<tr>
<td>callback</td>
<td>ログインのコールバック。成功時に code は0になります。</td>
</tr>
</table>
<pre>
TRTCLiveRoom mLiveRoom = TRTCLiveRoom.sharedInstance(this);
//useCDNFirst：trueは普通の視聴者のCDN経由の視聴、falseは普通の視聴者の低遅延による視聴を表します。
//yourCDNPlayDomain：CDN視聴時に設定する再生ドメイン名を表します。
TRTCLiveRoomDef.TRTCLiveRoomConfig config = 
    new TRTCLiveRoomDef.TRTCLiveRoomConfig(useCDNFirst, yourCDNPlayDomain);
mLiveRoom.login(SDKAPPID, userId, userSig, config, 
    new TRTCLiveRoomCallback.ActionCallback() {
            @Override
            public void onCallback(int code, String msg) {
                if (code == 0) {
                    //ログイン成功
                }
            }
});
</pre>

<span id="model.step5"> </span>
### 手順5：キャスター側の放送開始
1. キャスターは、[手順4](#model.step4)でログイン後、`setSelfProfile`をコールして自身のニックネームおよびプロファイル写真を設定することができます。
2. キャスターは、放送開始前に先に`startCameraPreview`を呼び出してカメラのプレビューを起動させ、インターフェース上に美顔調節ボタンを設置して呼び出し、`getBeautyManager`で美顔設定を行うことができます。
 >エンタープライズ版以外のSDKは変顔やスタンプの機能をサポートしていません。
 >
3. 美顔効果の変更後、キャスターは`createRoom`を呼び出して新しいライブルームを作成することができます。
4. キャスターが`startPublish`を呼び出し、プッシュを開始します。CDN視聴のサポートが必要な場合は、login 時に渡される`TRTCLiveRoomConfig`パラメータの中で`useCDNFirst`と`CDNPlayDomain`を指定し、`startPublish`時にライブストリーミングプッシュ用のstreamIDを指定してください。

![](https://main.qcloudimg.com/raw/eab281d702879ae87728d0064a090dca.jpg)

```java
// 1.キャスターは、ニックネームおよびプロファイル写真を設定します。
mLiveRoom.setSelfProfile("A", "your_face_url", null);

// 2.キャスターが放送開始前にプレビューを立ち上げ、美顔パラメータを設定します
TXCloudVideoView view = new TXCloudVideoView(context);
parentView.add(view);
mLiveRoom.startCameraPreview(true, view, null);
mLiveRoom.getBeautyManager().setBeautyStyle(1);
mLiveRoom.getBeautyManager().setBeautyLevel(6);

// 3.キャスターがルームを作成します。
TRTCLiveRoomDef.TRTCCreateRoomParam param = new TRTCLiveRoomDef.TRTCCreateRoomParam();
param.roomName = "テストルーム";
mLiveRoom.createRoom(123456789, param, new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 4.キャスターがプッシュを開始し、ストリームがCDNに配信されます。
            mLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});
```

<span id="model.step6"> </span>
### ステップ6：視聴者側の視聴
1. 視聴者側は、[手順4](#model.step4) でログイン後、`setSelfProfile`をコールして自身のニックネームおよびプロファイル写真を設定することができます。
2. 視聴者側が業務バックエンドから最新のライブルームリストを取得します。
 >Demoの中のライブルームリストはデモに使用するためだけのものです。ライブルームリストの業務ロジックは千差万別です。現在、Tencent Cloudはライブルームリスト管理のサービスを提供していません。各自でご自分のライブルームリストを管理してください。
 >
3. 視聴者側は、`getRoomInfos`をコールしてルームの詳細情報を取得します。この情報は、キャスター側が`createRoom`をコールしてライブルームを作成するときに設定する簡単な説明情報です。
 >ライブルームのリストに十分で全体的な情報がある場合は、`getRoomInfos`のコール関連の手順をスキップできます。
4. 視聴者は1つのライブルームを選択し、`enterRoom`をコールしてルームナンバーを渡すと、そのルームに入室できます。
5. `startPlay`を呼び出してキャスターのuserIdを渡し、再生を開始します。
 - ライブルームリストにキャスターのuserID 情報がすでに含まれている場合、視聴者は直接`startPlay`を呼び出してキャスターのuserIdを渡せば、再生を開始できます。
 - ルーム参加前にキャスターのuserIDが一時的に取得できない場合、視聴者はルーム参加後にキャスターの`onAnchorEnter`のイベントコールバックを受信します。このコールバックの中にキャスターのuserID 情報が含まれていますので、`startPlay`を呼び出せば再生できます。 

![](https://main.qcloudimg.com/raw/2ff8b30de38a3084c12af0513068dc6e.jpg)

```java
// 1.業務バックエンドから取得したルームリストを roomListと仮定します
List<Integer> roomList = GetRoomList();

// 2. getRoomInfos をコールすることによって、ルームの詳細情報を取得します
mLiveRoom.getRoomInfos(roomList, new TRTCLiveRoomCallback.RoomInfoCallback() {
    @Override
    public void onCallback(int code, String msg, List<TRTCLiveRoomDef.TRTCLiveRoomInfo> list) {
        if (code == 0) {
            // ルーム詳細情報の取得後、キャスターリスト画面でキャスターのニックネーム、プロファイル写真等の関連情報を表示できます。
        }
    }
})

// 3.roomidを選択しルームに参加します
mLiveRoom.enterRoom(roomid, null);

// 4.視聴者がキャスターのルーム参加の通知を受信すると、再生が開始されます。
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {  
        // 5.視聴者がキャスターの画面を再生します。
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
```

<span id="model.step7"> </span>
### 手順7：視聴者とキャスターとのマイク接続
1. 視聴者側が`requestJoinAnchor`を呼び出し、キャスター側にマイク接続のリクエストを送信します。
2. キャスター側は `TRTCLiveRoomDelegate#onRequestJoinAnchor`（視聴者があなたとのマイク接続をリクエスト）のイベント通知を受信します。
3. キャスター側は`responseJoinAnchor`を呼び出し、視聴者からのマイク接続リクエストを受け入れるかどうか決定できます。
4. 視聴者側が`TRTCLiveRoomDelegate#responseCallback`のイベント通知を受信します。この通知にはキャスターの処理結果が含まれています。
5. キャスターがマイク接続リクエストに同意したら、視聴者側は`startCameraPreview`を呼び出し、ローカルカメラを起動させます。その後`startPublish`を呼び出し、視聴者側のプッシュを開始します。
6. キャスター側は、視聴者側の起動の通知の後に、`TRTCLiveRoomDelegate#onAnchorEnter` （別のオーディオ・ビデオストリーミングが届いている）の通知を受信します。この通知には視聴者側のuserIdが含まれています。
7. キャスター側が`startPlay`を呼び出すと、マイク接続の視聴者の画面を見ることができます。

![](https://main.qcloudimg.com/raw/05a8c6af8bdc8b441f90b297e83106fc.jpg)

```java
// 1.視聴者側がマイク接続のリクエストを送信します。
mLiveRoom.requestJoinAnchor(mSelfUserId + "あなたとのマイク接続をリクエスト", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 4.キャスターが視聴者のリクエストを受け入れます。
            TXCloudVideoView view = new TXCloudVideoView(context);
            parentView.add(view);
            // 5.視聴者がプレビューを立ち上げ、プッシュを開始します。
            mLiveRoom.startCameraPreview(true, view, null);
            mLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});

// 2.キャスター側がマイク接続のリクエストを受信します。
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestJoinAnchor(final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, 
		    String reason, final int timeout) {
        // 3.相手側のマイク接続のリクエストに同意します。
        mLiveRoom.responseJoinAnchor(userInfo.userId, true, "マイク接続に同意");
    }

    @Override
    public void onAnchorEnter(final String userId) {
        // 6.キャスターがマイク接続の視聴者のマイク・オンの通知を受信します。
        TXCloudVideoView view = new TXCloudVideoView(context);
        parentView.add(view);
        // 7.キャスターが視聴者の画面を再生します。
        mLiveRoom.startPlay(userId, view, null);
    }
});
```

<span id="model.step8"> </span>
### 手順8：キャスターとキャスターのPK
1. キャスター Aが`requestRoomPK`を呼び出し、キャスター BにPKのリクエストを送信します。
2. キャスター Bが`TRTCLiveRoomDelegate onRequestRoomPK`のコールバック通知を受信します。
3. キャスター Bが`responseRoomPK`を呼び出し、キャスター A のPKのリクエストを受け入れるか決定します。
4. キャスター Bは、キャスター Aのリクエストを受け入れたら、`TRTCLiveRoomDelegate onAnchorEnter`の通知を待ってから、`startPlay`を呼び出し、キャスター Aを表示します。
5. PKのリクエストが同意されたかについて、キャスター A が`responseCallback`のコールバック通知を受信します。
6. キャスター Aのリクエストが同意されたら、`TRTCLiveRoomDelegate onAnchorEnter`の通知を待ってから、`startPlay`を呼び出し、キャスター Bを表示します。

![](https://main.qcloudimg.com/raw/5632056b6d86541db841026e9488468b.jpg)

```java
// キャスター A:
// キャスター Aがルーム12345を作成します。
mLiveRoom.createRoom(12345, param, null);

mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {
        // 6.Bのルーム参加の通知を受信します。
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});

// 1.キャスター Aがキャスター BにPKのリクエストを送信します。
mLiveRoom.requestRoomPK(54321, "B", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {  
        // 5.同意の有無のコールバックを受信します。
        if (code == 0) {
            // ユーザー受け入れ
        }else{
            // ユーザー拒否
        }
    }
});

// キャスター B：
// キャスター Bがルーム54321を作成します。
mLiveRoom.createRoom(54321, param, null);

// 2.キャスター Bがキャスター Aのメッセージを受信します。
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestRoomPK(
       final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, final int timeout) {
        // 3.キャスター Bがキャスター Aに回答し、リクエストを受け入れます。
        mLiveRoom.responseRoomPK(userInfo.userId, true, "");
    }
    @Override
    public void onAnchorEnter(final String userId) {
        // 4.キャスター Bがキャスター Aのルーム参加の通知を受信し、キャスターAの画面を再生します。
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
```

<span id="model.step9"> </span>
### 手順9：文字チャットおよび弾幕コメントの実装
- `sendRoomTextMsg`によって通常のテキストメッセージを発信できるようになり、該当するルーム内の全てのキャスターおよび視聴者が`onRecvRoomTextMsg`のコールバックを受信することができます。
 IMバックエンドは、デフォルトのNGワードフィルター規則を有し、NGワードと認識されたテキストメッセージはクラウドに転送されることはありません。
```java
// 発信側：テキストメッセージの発信
mLiveRoom.sendRoomTextMsg("Hello Word!", null);
// 受信側：テキストメッセージのモニタ
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRecvRoomTextMsg(String roomId, 
		    String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo) {
        Log.d(TAG, "が" + userInfo.userName + "から受信した情報:" + message);
    }
});
```
- `sendRoomCustomMsg`によってカスタマイズ（シグナリング）情報を発信することができます。そのルーム内の全てのキャスターおよび視聴者は`onRecvRoomCustomMsg`のコールバックを受信することができます。
カスタマイズメッセージは、カスタマイズ信号の伝送によく用いられます。例：「いいね」情報の発信および放送。
```java
// 発信側：カスタマイズ Cmd によって弾幕と「いいね」情報を区別することができます
// eg:"CMD_DANMU"は弾幕コメントを表し、"CMD_LIKE"は「いいね」情報を表します
mLiveRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mLiveRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// 受信側：カスタマイズメッセージのモニタ
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String roomId, String cmd, 
		    String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo) {
        if ("CMD_DANMU".equals(cmd)) {
            // 弾幕コメントの受信
            Log.d(TAG, "が" + userInfo.userName + "から受信した弾幕コメント:" + message);
        } else if ("CMD_LIKE".equals(cmd)) {
            // 「いいね」情報の受信
            Log.d(TAG, userInfo.userName + "いいねを付けました！");
        }
    }
});
```
