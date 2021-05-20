## デモンストレーション

[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)してDemoをインストールし、ボイスチャット、マイクのオン・オフ、低遅延音声インタラクションなどのボイスチャットのユースケースにおけるTRTCの関連機能を含む、ボイスサロンの機能を体験できます。

ボイスサロン機能をすばやく実装する必要がある場合、当社が提供するDemoをもとにアダプタを直接修正するか、または当社が提供するTRTCChatSalonコンポーネントでUIのカスタマイズを実装することができます。

[](id:DemoUI)
## DemoのUIの再利用

[](id:ui.step1)

### 手順1：アプリケーションの新規作成
1．TRTCコンソールにログインし、【開発支援】>【[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. アプリケーション名（例：`TestChatSalon`）を入力し、【作成】をクリックします。

>!本機能はTencent Cloud[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://ntl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。



[](id:ui.step2)

### 手順2：SDKおよびDemoソースコードをダウンロード
1. 実際の業務ニーズに基づき、SDKおよび付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、【ダウンロードしました。次のステップ】をクリックします。
![](https://main.qcloudimg.com/raw/3b115019ddfd0866108ed1add30810d8.png)

[](id:ui.step3)

### 手順3：Demoプロジェクトファイルの設定

1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`のファイルを見つけて開きます。
3. `GenerateTestUserSig.java`ファイル内の関連パラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</ul>
<img src="https://main.qcloudimg.com/raw/586439966d8588888cecf80d3bb4fe46.png">
4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。


>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**のこの手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)
### 手順4：Demoの実行
Android Studio（バージョン3.5以上）を使用してソースコードプロジェクトの`TRTCScenesDemo`を開き、【実行】をクリックすると、このDemoのデバッグが開始されます。

[](id:ui.step5)
### 手順5：Demoソースコードの修正
ソースコードのtrtcchatsalondemoフォルダは、uiとmodelという2つのサブフォルダを含んでいます。uiフォルダにはインターフェースコードが含まれています。以下の表にはファイルまたはフォルダおよび対応するUIをリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ | 機能の説明                             |
| ------------ | ------------------------------------ |
| base         | UIに使用される基礎となるクラス。                    |
| list         | リストページおよびルームページの作成。                 |
| room         | メインルームページは、キャスターと視聴者という2種類のインターフェースがあります。 |
| widget       | 汎用ウィジェット。                           |

[](id:model)
## カスタマイズUIの実装
[ソースコード](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCScenesDemo/trtcchatsalondemo/src/main/java/com/tencent/liteav/trtcchatsalon)のtrtcchatsalondemoフォルダにはuiとmodelという2つのサブフォルダがあり、modelフォルダには再利用できるオープンソースコンポーネント TRTCVoiceRoomがあります。`TRTCVoiceRoom.java`ファイルでこのコンポーネントが提供するインターフェース関数を確認し、対応するインターフェースを使用してカスタマイズしたUIを実装することができます。
![](https://main.qcloudimg.com/raw/fcf694c8550664623414604d14ffcd94.png)

[](id:model.step1)
### 手順1：SDKへの統合

ボイスサロンコンポーネント trtcchatsalondemo は、TRTC SDKとIM SDKに依存し、次の手順で2つのSDKをプロジェクトに統合することができます。

[](id:model.step1_m1)
#### 方法1：Mavenリポジトリを介する依存
1. dependenciesにTRTCSDKとIMSDKの依存を追加します。
```
dependencies {
       complie "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       complie 'com.tencent.imsdk:imsdk:latest.release'
       compile 'com.google.code.gson:gson:2.3.1'
}
```
>?2つのSDKの最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK)および[IM](https://github.com/tencentyun/TIMSDK)のGithubトップページで取得することができます。
2. defaultConfigでAppが使用するCPUアーキテクチャを指定します。
```
defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
}
```
3．【Sync Now】をクリックし、自動でSDKをダウンロードし、プロジェクトに統合します。

[](id:model.step1_m2)
#### 方法2：ローカルAARを介する依存
開発環境でのMavenリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。

<table>
<tr><th>SDK</th><th>ダウンロードページ</th><th>統合ガイド</th>
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

AndroidManifest.xmlにAppの権限を設定します。SDKには次の権限が必要です（6.0以降のAndroidシステムではカメラ、読み取りストレージの権限を動的に申請する必要があります）。

```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
```

proguard-rules.proファイルでは、SDK関連を非難読化リストに追加します。

```
-keep class com.tencent.** { *; }
```

[](id:model.step3)
### 手順3：TRTCChatSalonコンポーネントのインポート
次のディレクトリ内のすべてのファイルをプロジェクトにコピーします。
```
trtcchatsalondemo/src/main/java/com/tencent/liteav/trtcchatsalon/model
```

[](id:model.step4)
### 手順4：コンポーネントの作成およびログイン
1. `sharedInstance`インターフェースを呼び出すと、TRTCChatSalonコンポーネントのインスタンスオブジェクトを作成できます。
2. `setDelegate`関数を呼び出してコンポーネントのイベント通知を登録します。
3. `login`関数を呼び出してコンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
 <table>
<tr><th>パラメータ名</th><th>作用</th></tr>
<tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a>でSDKAppIDを表示できます。</td>
</tr>
<tr>
<td>userId</td>
<td>現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、<a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSigの計算方法</a>をご参照ください。</td>
</tr>
<tr>
<td>callback</td>
<td>ログインのコールバック。成功時にcodeは0になります。</td>
</tr>
</table>
<dx-codeblock>
::: java java
TRTCChatSalon mTRTCChatSalon = TRTCChatSalon.sharedInstance(this);
mTRTCChatSalon.setDelegate(this);
mTRTCChatSalon.login(SDKAPPID, userId, userSig, new TRTCChatSalonCallback.ActionCallback() {
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
2. キャスターは、`createRoom`を呼び出して新しいボイスサロンを作成します。このとき、ルームID、マイク・オンに管理者の確認の要否、ルームタイプなどルームの属性情報を渡します。
3. キャスターは、メンバーが参加した`onAnchorEnterSeat`のイベント通知を受信します。このとき、マイク集音は自動的に開始されます。

![](https://main.qcloudimg.com/raw/0b06ef225f749caa8b1f3a16c2316890.png)
<dx-codeblock>
::: java java
// 1.キャスターは、ニックネームおよびプロフィール画像を設定します
mTRTCChatSalon.setSelfProfile("my_name", "my_face_url", null);

// 2.キャスターは、createRoomを呼び出してルームを作成します
final TRTCChatSalonDef.RoomParam roomParam = new TRTCChatSalonDef.RoomParam();
roomParam.roomName = 「ルーム名」;
roomParam.needRequest = true; // マイク・オンの管理者による確認の要否
roomParam.coverUrl = 「ルームカバー図のURL」;
mTRTCChatSalon.createRoom(mRoomId, roomParam, new TRTCChatSalonCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3.座席を占有します
            mTRTCChatSalon.enterSeat(new TRTCChatSalonCallback.ActionCallback() {
                @Override
                public void onCallback(int code, String msg) {
                    if (code == 0) {
                    }
                }
            });
        }
    }
});

// 4.席の占有成功後、onAnchorEnterSeatイベント通知を受信します
@Override
public void onAnchorEnterSeat(TRTCChatSalonDef.UserInfo userInfo) {
}
:::
</dx-codeblock>

[](id:model.step6)

### 手順6：視聴者側の視聴

1. 視聴者側は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 視聴者側は、業務バックエンドから最新のボイスサロンのルームリストを取得します。
 >?Demoのボイスサロンリストは、デモンストレーションでの使用のみです。ボイスサロンリストのビジネスロジックは様々です。Tencent Cloudでは現在、ボイスサロンリストの管理サービスを提供していませんので、ご自身でボイスサロンリストを管理してください。
3. 視聴者側は、`getRoomInfoList`を呼び出してルームの詳細情報を取得します。この情報は、キャスター側が`createRoom`を呼び出してボイスサロンを作成するときに設定する簡単な説明情報です。
>!ボイスサロンリストに十分に包括的な情報がある場合は、`getRoomInfoList`の呼び出しに関する手順をスキップできます。
4．視聴者は一つのボイスサロンを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
5. 入室後、コンポーネントの`onRoomInfoChange`というルーム属性の変更イベント通知を受信します。このとき、ルーム属性を記録し、UIに表示されるルーム名、マイク・オンにキャスターへの同意のリクエストの要否の記録など、対応する変更を行うことができます。
6. 入室後にマイクリストにキャスターが参加した`onAnchorEnterSeat`のイベント通知も受信します。

![](https://main.qcloudimg.com/raw/b08253d1835ca6e571378af76c84e275.png)
<dx-codeblock>
::: java java
// 1.視聴者は、ニックネームおよびプロフィール画像を設定します
mTRTCChatSalon.setSelfProfile("my_name", "my_face_url", null);

// 2.業務バックエンドから取得したルームリストをroomListと仮定します
List<Integer> roomList = GetRoomList();

// 3.getRoomInfoListを呼び出すことによって、ルームの詳細情報を取得します
mTRTCChatSalon.getRoomInfoList(roomList, new TRTCChatSalonCallback.RoomInfoCallback() {

    @Override
    public void onCallback(int code, String msg, List<TRTCChatSalonDef.RoomInfo> list) {
        if (code == 0) {
            // この時、自分のUIルームリストを更新することができます
        }
    }

});

// 4.roomidを渡してルームに参加します
mTRTCChatSalon.enterRoom(roomId, new TRTCChatSalonCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
                //入室に成功
            }
        }
});

// 5.入室に成功後、onRoomInfoChangeイベント通知を受信します
@Override
public void onRoomInfoChange(TRTCChatSalonDef.RoomInfo roomInfo) {
    mNeedRequest = roomInfo.needRequest;
    mRoomName = roomInfo.roomName;
    // UIはタイトルなどを表示することができます
}

// 6. onAnchorEnterSeatイベント通知を受信します
@Override
public void onAnchorEnterSeat(TRTCChatSalonDef.UserInfo userInfo) {
}
:::
</dx-codeblock>

[](id:model.step7)

### 手順7：マイクのオン・オフ

<dx-tabs>
::: キャスター側
1. `pickSeat`は、視聴者のuserIdを渡し、ピックしてマイク・オンにできます。ルーム内の全メンバーは`onAnchorEnterSeat`のイベント通知を受信します。
2. `kickSeat`は、対応するユーザーのuserIdを渡し、キックアウトしてマイク・オフできます。ルーム内の全メンバーは`onAnchorEnterSeat`のイベント通知を受信します。

![](https://main.qcloudimg.com/raw/5a590df748b3cedd6eccd7d8e3027168.png)
マイク操作後のイベント通知の順番は次のとおりです。callback > onAnchorEnterSeatなど独立したイベント。
<dx-codeblock>
::: java java
// 1.キャスターがピックしてマイク・オンにします
mTRTCChatSalon.pickSeat("123", new TRTCChatSalonCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. callbackコールバックを受信します
        if (code == 0) {
        }
    }
});

// 3.キャスターはマイク通知に進むと、ここで視聴者が適切な処理を行っているかどうかを判断することができます
public void onAnchorEnterSeat(TRTCChatSalonDef.UserInfo user) {
}
:::
</dx-codeblock>
:::
::: 視聴者側
1. `enterSeat`はマイク・オンにし、ルーム内の全メンバーは`onAnchorEnterSeat`のイベント通知を受信します。
2. `leaveSeat`は自主的にマイク・オフにし、ルーム内の全メンバーは`onAnchorLeaveSeat`のイベント通知を受信します。

![](https://main.qcloudimg.com/raw/08f7bf725fa05e1d97a69aacdbd3986a.png)
マイク操作後のイベント通知の順番は次のとおりです。callback > onAnchorEnterSeatなど独立したイベント。
<dx-codeblock>
::: java java
// 1.視聴者が自主的にマイク・オンにします
mTRTCChatSalon.enterSeat(new TRTCChatSalonCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. callbackコールバックを受信します
        if (code == 0) {
        }
    }
});

// 3.キャスターはマイク通知に進むと、ここで自分が適切な処理を行っているかどうかを判断することができます
public void onAnchorEnterSeat(int index, TRTCChatSalonDef.UserInfo user) {
}
:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step8)
### 手順8：招待シグナリングの使用
Appが次の操作の業務フローを実施するために、相手の同意を必要とする場合、招待シグナリングによって対応するサポートを提供することができます。

<dx-tabs>
::: 視聴者からの自主的なマイク申請
1. 視聴者側は、`sendInvitation`を呼び出してキャスターのuserIdおよび業務のカスタムコマンドワードなどを渡します。この時、関数は1個のinviteIdを返しこのinviteIdを記録します。
2. キャスター側は、`onReceiveNewInvitation`のイベント通知を受信します。この時、UIはウィンドウをポップアップして、キャスターに同意するかどうか照会することができます。
3. キャスターが同意を選択後、`acceptInvitation`を呼び出してinviteIdを渡します。
4. 視聴者側は、`onInviteeAccepted`のイベント通知を受信し、`enterSeat`を呼び出してマイク・オンにします。

![](https://main.qcloudimg.com/raw/76f13e8118c49136fcfd99942e56a65e.png)

<dx-codeblock>
::: java java
// 視聴者側の視点
// 1. sendInvitationを呼び出し、マイク・オンをリクエストします
String inviteId = mTRTCChatSalon.sendInvitation("ENTER_SEAT", ownerUserId, "123", null);

// 2.招待の同意リクエストを受信して、正式にマイク・オンにします
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCChatSalon.enterSeat(null);
    }
}

// キャスター側の視点
// 1.キャスターがリクエストを受信します
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("ENTER_SEAT")) {
        // 2.キャスターが視聴者のリクエストに同意します
         mTRTCChatSalon.acceptInvitation(id, null);
    }
}
:::
</dx-codeblock>
:::
::: キャスターから視聴者を招待してマイク・オン

1. キャスター側は、`sendInvitation`を呼び出して視聴者のuserIdおよび業務のカスタマイズコマンドワードなどを渡します。この時、関数は1個のinviteIdを返しこのinviteIdを記録します。
2. 視聴者側は、`onReceiveNewInvitation`のイベント通知を受信します。この時、UIはウィンドウをポップアップして、視聴者がマイク・オンに同意するかどうかを照会することができます。
3. 視聴者が同意を選択後、`acceptInvitation`を呼び出してinviteIdを渡します。
4. キャスター側は、`onInviteeAccepted`のイベント通知を受信し、`pickSeat`を呼び出し視聴者をピックしてマイク・オンにします。

![](https://main.qcloudimg.com/raw/3193dd17c510ca5a6583747c0bde0114.png)

<dx-codeblock>
::: java java
// キャスター側の視点
// 1.キャスターはsendInvitationを呼び出して、視聴者123をピックしてマイク・オンをリクエストします
String inviteId = mTRTCChatSalon.sendInvitation("PICK_SEAT", ownerUserId, "123", null);

// 2.招待の同意リクエストを受信して、正式にマイク・オンにします
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCChatSalon.pickSeat(null);
    }
}

// 視聴者側の視点
// 1.視聴者がリクエストを受信します
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("PICK_SEAT")) {
        // 2.視聴者がキャスターのリクエストに同意します
         mTRTCChatSalon.acceptInvitation(id, null);
    }
}
:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step9)
### 手順9：文字チャットおよび弾幕コメントの実装
- `sendRoomTextMsg`によって通常のテキストメッセージを送信できるようになり、該当するルーム内の全てのキャスターおよび視聴者が`onRecvRoomTextMsg`のコールバックを受信することができます。
  IMバックエンドは、デフォルトのセンシティブワードフィルタルールを備えており、センシティブワードと認識されたテキストメッセージはクラウドに転送されることはありません。
  <dx-codeblock>
  ::: java java
  // 送信側：テキストメッセージの送信
  mTRTCChatSalon.sendRoomTextMsg("Hello Word!", null);
  // 受信側：テキストメッセージの監視
  mTRTCChatSalon.setDelegate(new TRTCChatSalonDelegate() {
   @Override
   public void onRecvRoomTextMsg(String message, TRTCChatSalonDef.UserInfo userInfo) {
       Log.d(TAG、「が」 + userInfo.userName + 「から受信したメッセージ:」 + message);
   }
  });
  :::
  </dx-codeblock>
- `sendRoomCustomMsg`によってカスタマイズ（シグナリング）情報を送信することができます。そのルーム内のすべてのキャスターおよび視聴者は`onRecvRoomCustomMsg`のコールバックを受信することができます。
  カスタムメッセージは、カスタマイズ信号の送信によく用いられます。例えば、「いいね」情報の発信やブロードキャストに使用します。
  <dx-codeblock>
  ::: java java
  // 送信側：カスタマイズCmdによって弾幕と「いいね」情報を区別することができます
  // eg:「CMD_DANMU」は弾幕コメントを表し、「CMD_LIKE」は「いいね」情報を表します
  mTRTCChatSalon.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
  mTRTCChatSalon.sendRoomCustomMsg("CMD_LIKE", "", null);
  // 受信側：カスタムメッセージの監視
  mTRTCChatSalon.setDelegate(new TRTCChatSalonDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, String message, TRTCChatSalonDef.UserInfo userInfo) {
        if ("CMD_DANMU".equals(cmd)) {
            // 弾幕コメントの受信
            Log.d(TAG、「が」 + userInfo.userName + 「から受信した弾幕コメント:」 + message);
        } else if ("CMD_LIKE".equals(cmd)) {
            // 「いいね」情報の受信
            Log.d(TAG、 userInfo.userName + 「いいねを付けました！」);
        }
    }
  });
  :::
  </dx-codeblock>
