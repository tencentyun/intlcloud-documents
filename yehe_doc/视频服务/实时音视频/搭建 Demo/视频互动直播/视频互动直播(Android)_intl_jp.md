## デモンストレーション
[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)からAppをインストールすると、インタラクティブストリーミング機能の効果を体験していただくことができます。これにはマイク接続によるインタラクション、キャスターPK、低レイテンシーの視聴、弾幕チャットなど、TRTCのインタラクティブライブストリーミングシーンにおける関連機能が含まれています。

ビデオ・インタラクティブストリーミングの機能をすばやく実装する必要がある場合、当社が提供するAppをもとに直接修正を加えてフィットさせることも、当社が提供するTRTCLiveRoomコンポーネントを使用し、カスタマイズしたUIを実現することも可能です。

[](id:DemoUI)
## AppのUIの再利用

[](id:ui.step1)
### 手順1：アプリケーションの新規作成
1. TRTCコンソールにログインし、【開発支援】>【[快速跑通Demo](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. 例えば、`TestLiveRoom`などアプリケーション名を入力して、【作成】をクリックします。
3. 【ダウンロードしました。次のステップ】をクリックすると、この手順をスキップします。

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>! 本機能はTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/10479)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期してアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。


[](id:ui.step2)
### 手順2：Appソースコードのダウンロード
クリックして[TUILiveRoom](https://github.com/tencentyun/TUILiveRoom)に進み、ソースコードをCloneまたはダウンロードします。


[](id:ui.step3)
### 手順3：Appプロジェクトファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`のファイルを見つけて開きます。
3. `GenerateTestUserSig.java`ファイル内の関連パラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトはプレースホルダー(PLACEHOLDER)。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトはプレースホルダー(PLACEHOLDER)。実際のキー情報を設定してください。</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 貼り付け完了後、【貼り付けました。次へ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソールの概要ページに戻る】をクリックすればOKです。

>!ここで言及したUserSigの発行方法は、クライアントコードにSECRETKEYを設定しますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのAppクイックスタートおよび機能デバッグにのみ適しています**。
≻ UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)
### 手順4：Appの実行
Android Studio（バージョン3.5以上）を使用してソースコード`TUILiveRoom`プロジェクトを開き、【実行】をクリックすれば、このAppのデバッグが開始されます。

[](id:ui.step5)
### 手順5：Appソースコードの修正
ソースコードのSourceフォルダは、uiとmodelという2つのサブフォルダを含んでいます。uiフォルダにはインターフェースコードが含まれています。以下の表にファイルまたはフォルダおよび対応するUIをリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ | 機能の説明                             |
|:-------:|:--------|
| anchor | キャスター側に関するUIの実装コード。 |
| audience | 視聴者側に関するUIの実装コード。 |
| common | 一般的なUIコンポーネントの実装コード。 |
| widget       | 汎用ウィジェット。                           |



## 体験アプリケーション
>! 体験アプリケーションには、少なくとも2台のデバイスが必要です。

### ユーザーA
1. ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. ログイン後、【ルームの作成】をクリックします。
3. ルーム名を入力し、【ライブストリーミングを開始】をクリックします。

### ユーザーB
1. ユーザー名を入力します（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）。
2. ユーザーAが作成したルームナンバーを入力し、入室するをクリックします。<br>


>! ルームナンバーはユーザーAのルーム上部に表示されます。



## ルームのステータスの監視とPKリストへのアクセス
ルームのステータスは、次のように`LiveRoomManager`を使用して監視することができます。
<dx-codeblock>
::: java java
LiveRoomManager.getInstance().addCallback(new LiveRoomManager.RoomCallback() {
    /**
     * ルームの作成
     * @param roomId
     * @param callbackは、内部処理の結果を通知するために使用します
     */
    @Override
    public void onRoomCreate(int roomId, final LiveRoomManager.ActionCallback callback) {
        // doSomething
    }

    /**
     * ルームの破棄
     * @param roomId
     * @param callbackは、内部処理の結果を通知するために使用します
     */
    @Override
    public void onRoomDestroy(int roomId, final LiveRoomManager.ActionCallback callback) {
        // doSomething
    }
    
    /**
     * ルームリストの取得
     * @param callback
     */
    @Override
    public void onGetRoomIdList(final LiveRoomManager.GetCallback callback) {
        // ルームリストを取得します。ご自分で管理する必要があります。ユーザー間のPKに使用します
        if(callback != null) {
            if(success) {
                // コールバックに成功しました。ルームリストが渡されます
                callback.onSuccess(roomList);
            }else{
                // ルームリストの取得に失敗しました
                callback.onError(code, message);
            }
        }
    }
});
:::
</dx-codeblock>
ユーザーのアクセスを容易にするため、Callback方式が採用されています。例えば、ルームリストの取得には非同期操作が必要な場合がありますが、Callback方式を採用すればよりフレキシブルになります。


[](id:model)
## UIカスタマイズの実装

[ソースコード](https://github.com/tencentyun/TUILiveRoom/tree/master/Android/Source/src/main/java/com/tencent/liteav/liveroom)のSourceフォルダには、uiとmodelという2つのサブフォルダがあり、modelフォルダには再利用できるオープンソースコンポーネントTRTCLiveRoomがあります。`TRTCLiveRoom.java`ファイルでこのコンポーネントが提供するインターフェース関数を確認し、対応するインターフェースを使用してカスタマイズしたUIを実装することができます。
![](https://main.qcloudimg.com/raw/710358e4e170d44304cdb9bc991ad209.jpg)

[](id:model.step1)
### 手順1：SDKの統合 
ビデオ・インタラクティブストリーミングコンポーネントTRTCLiveRoomは、TRTC SDKとIM SDKに依存し、次の手順で2つのSDKをプロジェクトに統合することができます。

**方法1：Mavenリポジトリを介する依存**
1. dependenciesにTRTCSDKとIMSDKの依存を追加します。
<dx-codeblock>
::: java java
dependencies {
       compile "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       compile 'com.tencent.imsdk:imsdk:latest.release'
}
:::
</dx-codeblock>
>?2つのSDKの最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK) および[IM](https://github.com/tencentyun/TIMSDK) のGithubトップページで取得することができます。
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
3．【Sync Now】をクリックし、自動でSDKをダウンロードし、プロジェクトに統合します。

**方法2：ローカルAARを介する依存**
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

[](id:model.step2)
### 手順2：権限の設定および難読化ルール
AndroidManifest.xmlにAppの権限を設定します。SDKには次の権限が必要です（6.0以上のAndroidシステムではカメラ、ストレージ読み取りの権限を動的に申請する必要があります）。
<dx-codeblock>
::: java java
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
:::
</dx-codeblock>

proguard-rules.proファイルでは、SDK関連を非難読化リストに追加します。
<dx-codeblock>
::: java java
-keep class com.tencent.** { *; }
:::
</dx-codeblock>

[](id:model.step3)
### 手順3：TRTCLiveRoomコンポーネントをインポート
次のディレクトリ内のすべてのファイルをプロジェクトにコピーします。
<dx-codeblock>
::: java java
src/main/java/com/tencent/liteav/liveroom/model
:::
</dx-codeblock>

[](id:model.step4)
### 手順4：コンポーネントの作成およびログイン
1. sharedInstance インターフェースを呼び出すと、TRTCLiveRoomコンポーネントのインスタンスオブジェクトを作成できます。
2. 1つの TRTCLiveRoomConfig オブジェクトを作成したら、このオブジェクトにuseCDNFirstとCDNPlayDomainの属性を設定することができます。
 - useCDNFirstの属性：視聴者の視聴方式の設定に使用します。trueは、一般視聴者のCDN経由での視聴を表し、料金は安価ですがレイテンシーは高めです。falseは、一般視聴者の低レイテンシーによる視聴を表し、料金はCDN とマイク接続の間ですが、遅延を1s以内に抑えることができます。
 - CDNPlayDomainの属性：useCDNFirstの設定をtrueにした時に有効になり、CDN経由の視聴の再生ドメイン名の指定に利用します。CSSコンソール >【[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)】ページからログインし、設定することができます。
3. `login`関数を呼び出してコンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
 <table>
<tr>
<th>パラメータ名</th>
<th>作用</th>
</tr>
<tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> で SDKAppIDを表示できます。</td>
</tr>
<tr>
<td>userId</td>
<td>現在のユーザーID。文字列タイプでは、英語のアルファベット（a-z、A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。業務の実際のアカウントシステムと組み合わせてご自身で設定することをお勧めします。</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、<a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSigの計算方法</a>をご参照ください。</td>
</tr>
<tr>
<td>config</td>
<td>グローバルコンフィギュレーション情報。ログイン時に初期化してください。ログイン後は変更できなくなります。<ul style="margin:0;">
<li>useCDNFirstの属性：視聴者の視聴方式の設定に使用します。trueは、一般視聴者のCDN経由での視聴を表し、料金は安価ですがレイテンシーは高めです。falseは、一般視聴者の低レイテンシーによる視聴を表し、料金は CDN とマイク接続の間ですが、遅延を1s以内に抑えることができます。</li>
<li>CDNPlayDomainの属性：useCDNFirstの設定をtrueにした時に有効になり、CDN経由の視聴の再生ドメイン名の指定に利用します。CSSコンソール>【<a href="https://console.cloud.tencent.com/live/domainmanage">ドメイン名管理</a>】ページからログインして設定を行うことができます。</li>
</ul></td>
</tr>
<tr>
<td>callback</td>
<td>ログインのコールバック。成功時にcodeは0になります。</td>
</tr>
</table>
<dx-codeblock>
::: java java
TRTCLiveRoom mLiveRoom = TRTCLiveRoom.sharedInstance(this);
//useCDNFirst：trueは一般視聴者のCDN経由の視聴、falseは一般視聴者の低レイテンシーによる視聴を表します
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
:::
</dx-codeblock>

[](id:model.step5)
### 手順5：キャスター側での配信開始
1. キャスターは、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. キャスターは、配信開始前に先に`startCameraPreview`を呼び出してカメラのプレビューを起動させ、インターフェース上に美顔調節ボタンを設置して呼び出し、`getBeautyManager`で美顔設定を行うことができます。
>?エンタープライズ版以外のSDKは美顔やスタンプなどの高度な美顔機能をサポートしていません。
3. 美顔効果の変更後、キャスターは `createRoom` を呼び出して新しいライブストリーミングルームを作成することができます。
4. キャスターが`startPublish`を呼び出し、プッシュを開始します。CDN視聴のサポートが必要な場合は、login時に渡される`TRTCLiveRoomConfig`パラメータ内で`useCDNFirst`と`CDNPlayDomain`を指定し、`startPublish`時にライブストリーミング・プルストリーム用のstreamIDを指定してください。

![](https://main.qcloudimg.com/raw/eab281d702879ae87728d0064a090dca.jpg)

<dx-codeblock>
::: java java
// 1.キャスターは、ニックネームおよびプロフィール画像を設定します
mLiveRoom.setSelfProfile("A", "your_face_url", null);

// 2.キャスターが配信開始前にプレビューを立ち上げ、美顔パラメータを設定します
TXCloudVideoView view = new TXCloudVideoView(context);
parentView.add(view);
mLiveRoom.startCameraPreview(true, view, null);
mLiveRoom.getBeautyManager().setBeautyStyle(1);
mLiveRoom.getBeautyManager().setBeautyLevel(6);

// 3.キャスターがルームを作成します
TRTCLiveRoomDef.TRTCCreateRoomParam param = new TRTCLiveRoomDef.TRTCCreateRoomParam();
param.roomName = 「テストルーム」;
mLiveRoom.createRoom(123456789, param, new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 4.キャスターがプッシュを開始し、ストリームがCDNに配信されます。
            mLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});
:::
</dx-codeblock>

[](id:model.step6)
### 手順6：視聴者側での視聴
1. 視聴者側は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 視聴者側が業務バックエンドから最新のライブストリーミングルームリストを取得します。
>?App内のライブストリーミングルームリストはデモに使用するためだけのものです。ライブストリーミングルームリストの業務ロジックは千差万別です。現在、Tencent Cloudはライブストリーミングルームリスト管理のサービスを提供していません。各自でご自分のライブストリーミングルームリストを管理してください。
3. 視聴者側は、`getRoomInfos`を呼び出してルームの詳細情報を取得します。この情報は、キャスター側が`createRoom`を呼び出してライブストリーミングルームを作成するときに設定する簡単な説明情報です。
>!ライブストリーミングルームのリストに十分に包括的な情報がある場合は、`getRoomInfos`の呼び出しに関する手順をスキップできます。
4. 視聴者は1つのライブストリーミングルームを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
5. `startPlay`を呼び出してキャスターのuserIdを渡し、再生を開始します。
 - ライブストリーミングルームリストにキャスターのuserID情報がすでに含まれている場合、視聴者は直接`startPlay`を呼び出してキャスターのuserIdを渡せば、再生を開始できます。
 - ルーム参加前にキャスターのuserIDが一時的に取得できない場合、視聴者側はルーム参加後にキャスターの`onAnchorEnter`のイベントコールバックを受信します。このコールバックの中にキャスターのuserID情報が含まれていますので、`startPlay`を呼び出せば再生できます。 

![](https://main.qcloudimg.com/raw/2ff8b30de38a3084c12af0513068dc6e.jpg)

<dx-codeblock>
::: java java
// 1.業務バックエンドから取得したルームリストをroomListと仮定します
List<Integer> roomList = GetRoomList();

// 2. getRoomInfosを呼び出すことによって、ルームの詳細情報を取得します
mLiveRoom.getRoomInfos(roomList, new TRTCLiveRoomCallback.RoomInfoCallback() {
    @Override
    public void onCallback(int code, String msg, List<TRTCLiveRoomDef.TRTCLiveRoomInfo> list) {
        if (code == 0) {
            // ルーム詳細情報の取得後、キャスターリストページでキャスターのニックネーム、プロフィール画像等の関連情報を表示できます
        }
    }
})

// 3.roomidを選択しルームに参加します
mLiveRoom.enterRoom(roomid, null);

// 4.視聴者がキャスターのルーム参加の通知を受信すると、再生が開始されます
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {  
        // 5.視聴者がキャスターの画面を再生します
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
:::
</dx-codeblock>

[](id:model.step7)
### 手順7：視聴者とキャスターとのマイク接続
1. 視聴者側が requestJoinAnchor を呼び出し、キャスター側にマイク接続のリクエストを送信します。
2. キャスター側は TRTCLiveRoomDelegate#onRequestJoinAnchor（視聴者からのマイク接続のリクエストがあります）のイベント通知を受信します。
3. キャスター側は responseJoinAnchor を呼び出し、視聴者からのマイク接続リクエストを受け入れるかどうか決定できます。
4. 視聴者側が`TRTCLiveRoomDelegate#responseCallback`のイベント通知を受信します。この通知にはキャスターの処理結果が含まれています。
5. キャスターがマイク接続リクエストに同意したら、視聴者側は`startCameraPreview`を呼び出し、ローカルカメラを起動させます。その後 startPublish を呼び出し、視聴者側のプッシュを開始します。
6. キャスター側は、視聴者側の起動の通知の後に、`TRTCLiveRoomDelegate#onAnchorEnter`（別のオーディオ・ビデオストリーミングが届いています）の通知を受信します。この通知には視聴者側のuserIdが含まれています。
7. キャスター側が startPlay を呼び出すと、マイク接続の視聴者の画面を見ることができます。

![](https://main.qcloudimg.com/raw/05a8c6af8bdc8b441f90b297e83106fc.jpg)

<dx-codeblock>
::: java java
// 1.視聴者側がマイク接続のリクエストを送信します
mLiveRoom.requestJoinAnchor(mSelfUserId + "あなたとのマイク接続をリクエスト", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 4.キャスターが視聴者のリクエストを受け入れます
            TXCloudVideoView view = new TXCloudVideoView(context);
            parentView.add(view);
            // 5.視聴者がプレビューを起動し、プッシュを開始します
            mLiveRoom.startCameraPreview(true, view, null);
            mLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});

// 2.キャスター側がマイク接続のリクエストを受信します
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestJoinAnchor(final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, 
        String reason, final int timeout) {
        // 3.相手側のマイク接続のリクエストに同意します
        mLiveRoom.responseJoinAnchor(userInfo.userId, true, "マイク接続に同意");
    }

    @Override
    public void onAnchorEnter(final String userId) {
        // 6.キャスターがマイク接続の視聴者のマイク・オンの通知を受信します
        TXCloudVideoView view = new TXCloudVideoView(context);
        parentView.add(view);
        // 7.キャスターが視聴者の画面を再生します
        mLiveRoom.startPlay(userId, view, null);
    }
});
:::
</dx-codeblock>

[](id:model.step8)
### 手順8：キャスターとキャスターPK
1. キャスターAが requestRoomPK を呼び出し、キャスターBにPKのリクエストを送信します。
2. キャスターBが `TRTCLiveRoomDelegate onRequestRoomPK`のコールバック通知を受信します。
3. キャスターBが `responseRoomPK` を呼び出し、キャスターA のPKのリクエストを受け入れるか決定します。
4. キャスターBは、キャスターAのリクエストを受け入れたら、 `TRTCLiveRoomDelegate onAnchorEnter`の通知を待ってから、`startPlay`を呼び出し、キャスターAを表示します。
5. PKのリクエストが同意されたかについて、キャスターAが`responseCallback`のコールバック通知を受信します。
6. キャスターAのリクエストが同意されたら、`TRTCLiveRoomDelegate onAnchorEnter`の通知を待ってから、`startPlay`を呼び出し、キャスターBを表示します 。

![](https://main.qcloudimg.com/raw/5632056b6d86541db841026e9488468b.jpg)

<dx-codeblock>
::: java java
// キャスターA:
// キャスターAがルーム12345を作成します
mLiveRoom.createRoom(12345, param, null);

mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {
        // 6.Bのルーム参加の通知を受信します
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});

// 1.キャスターAがキャスターBにPKのリクエストを送信します
mLiveRoom.requestRoomPK(54321, "B", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {  
        // 5.同意の有無のコールバックを受信します
        if (code == 0) {
            // ユーザー受け入れ
        }else{
            // ユーザー拒否
        }
    }
});

// キャスターB：
// キャスターBがルーム54321を作成します
mLiveRoom.createRoom(54321, param, null);

// 2.キャスターBがキャスターAのメッセージを受信します
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestRoomPK(
       final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, final int timeout) {
        // 3.キャスターBがキャスターAに回答し、リクエストを受け入れます
        mLiveRoom.responseRoomPK(userInfo.userId, true, "");
    }
    @Override
    public void onAnchorEnter(final String userId) {
        // 4.キャスターBがキャスターAのルーム参加の通知を受信し、キャスターAの画面を再生します
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
:::
</dx-codeblock>

[](id:model.step9)
### 手順9：文字チャットおよび弾幕コメントの実装
- `sendRoomTextMsg`によって通常のテキストメッセージを送信できるようになり、該当するルーム内の全てのキャスターおよび視聴者が`onRecvRoomTextMsg`のコールバックを受信することができます。
 IMバックエンドは、デフォルトでNGワードフィルター規則を有し、NGワードと認識されたテキストメッセージはクラウドに転送されることはありません。
  <dx-codeblock>
  ::: java java
  // 送信側：テキストメッセージの送信
  mLiveRoom.sendRoomTextMsg("Hello Word!", null);
  // 受信側：テキストメッセージのモニタリング
  mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRecvRoomTextMsg(String roomId, 
        String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo) {
        Log.d(TAG、 + userInfo.userName + 「からのメッセージを受信:」 + message);
    }
  });
  :::
  </dx-codeblock>
- `sendRoomCustomMsg`によって、カスタム（シグナル）メッセージを送信できます。当該ルーム内のすべてのキャスターと視聴者が`onRecvRoomCustomMsg` コールバックを受信できます。
カスタムメッセージは、カスタマイズ信号の送信によく用いられます。例えば、「いいね」情報の発信やブロードキャストに使用します。
<dx-codeblock>
::: java java// 送信側：カスタマイズCmdによって弾幕と「いいね」情報を区別することができます
// eg:「CMD_DANMU」は弾幕コメントを表し、「CMD_LIKE」は「いいね」情報を表します
mLiveRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mLiveRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// 受信側：カスタムメッセージのモニタリング
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String roomId, String cmd, 
        String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo) {
        if ("CMD_DANMU".equals(cmd)) {
            // 弾幕コメントの受信
            Log.d(TAG、 + userInfo.userName + 「からの弾幕コメントを受信:」 + message);
        } else if ("CMD_LIKE".equals(cmd)) {
            // 「いいね」情報の受信
            Log.d(TAG、 userInfo.userName + 「いいねを付けました！」);
        }
    }
});
:::
</dx-codeblock>
