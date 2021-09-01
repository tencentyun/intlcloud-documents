## デモンストレーション
[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)からDemoをインストールして、マイク管理、低レイテンシー音声インタラクション、文字チャットなどのボイスチャットのユースケースにおけるTRTCの関連機能を含む、ボイスチャットルームの機能を体験できます。

ボイスチャットルーム機能をすばやく実装する必要がある場合は、当社が提供するDemoをもとに直接適応に変更を加えることも、当社が提供するTRTCVoiceRoomコンポーネントでUIのカスタマイズを実装することも可能です。

[](id:DemoUI)
## DemoのUIの再利用

[](id:ui.step1)
### 手順1：アプリケーションの新規作成
1．TRTCコンソールにログインし、【開発支援】>【[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. 例えば、`TestLiveRoom`などアプリケーション名を入力して、【作成】をクリックします。

>!本機能はTencent Cloud[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。



[](id:ui.step2)
### 手順2：SDKおよびDemoソースコードをダウンロード
1. 実際の業務ニーズに基づき、SDKおよび付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、【ダウンロードしました。次のステップ】をクリックします。

[](id:ui.step3)
### 手順3：Demoプロジェクトファイルの設定
1. 設定変更画面に入り、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`のファイルを見つけて開きます。
3. `GenerateTestUserSig.java`ファイル内の関連パラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。


>!ここで言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適しています**。
≻ UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)
### 手順4：Demoの実行
Android Studio（バージョン3.5以上）を使用してソースコードプロジェクトの`TRTCScenesDemo`を開き、【実行】をクリックすると、このDemoのデバッグが開始されます。

[](id:ui.step5)
### 手順5：Demoソースコードの修正
ソースコードのtrtcvoiceroomdemoフォルダは、uiとmodelという2つのサブフォルダを含んでいます。uiフォルダにはインターフェースコードが含まれています。以下の表にはファイルまたはフォルダ及び対応するUIをリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ | 機能説明 |
|-------|--------|
| base | UIに使用される基礎となるクラス。 |
| list | リストページおよびルームページの作成。 |
| room | メインルームページ。キャスターと視聴者の2種類のインターフェースがあります。 |
| widget | 汎用ウィジェット。 |

[](id:model)
## UIカスタマイズの実現

[ソースコード](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCScenesDemo/trtcvoiceroomdemo/src/main/java/com/tencent/liteav/trtcvoiceroom)のtrtcvoiceroomdemoフォルダにはuiとmodelという2つのサブフォルダがあり、modelフォルダには再利用できるオープンソースコンポーネント TRTCVoiceRoomがあります。`TRTCVoiceRoom.java`ファイルでこのコンポーネントが提供するインターフェース関数を見て、対応するインターフェースを使用してUIのカスタマイズを実現することができます。
![](https://main.qcloudimg.com/raw/319beb14d72a43120e102380278aa1da.png)

[](id:model.step1)
### 手順1：SDKへの統合
ボイスチャットコンポーネントTRTCVoiceRoomは、TRTC SDKとIM SDKに依存し、次の手順で2つのSDKをプロジェクトに統合することができます。

**方法1：Mavenリポジトリを介する依存**
1. dependenciesにTRTCSDKとIMSDKの依存を追加します。
```
dependencies {
       complie "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       complie 'com.tencent.imsdk:imsdk:latest.release'
       compile 'com.google.code.gson:gson:2.3.1'
}
```
>?2つのSDKの最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK)および[IM](https://github.com/tencentyun/TIMSDK)のGithubトップページで取得することができます。
>
2. defaultConfigでAppが使用するCPUアーキテクチャを指定します。
```
defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
}
```
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
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
```

proguard-rules.proファイルでは、SDK関連を非難読化リストに追加します。
```
-keep class com.tencent.** { *; }
```

[](id:model.step3)
### 手順3：TRTCVoiceRoomコンポーネントをインポート
次のディレクトリ内のすべてのファイルをプロジェクトにコピーします。
```
trtcvoiceroomdemo/src/main/java/com/tencent/liteav/trtcvoiceroom/model
```

<span id="model.step4"></span>
### 手順4：コンポーネントの作成およびログイン
1. `sharedInstance`インターフェースを呼び出すと、TRTCVoiceRoomコンポーネントのインスタンスオブジェクトを作成できます。
2. `setDelegate`関数を呼び出してコンポーネントのイベント通知を登録します。
3. `login`関数を呼び出してコンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
 <table>
<tr>
<th>パラメータ名</th>
<th>作用</th>
</tr>
<tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> でSDKAppIDを表示できます。</td>
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

```
TRTCVoiceRoom mTRTCVoiceRoom = TRTCVoiceRoom.sharedInstance(this);
mTRTCVoiceRoom.setDelegate(this);
mTRTCVoiceRoom.login(SDKAPPID, userId, userSig, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            //ログイン成功
        }
    }
});
```

[](id:model.step5)
### 手順5：キャスター側での配信開始
1. キャスターは、[手順4](#model.step4) でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. キャスターは、`createRoom`を呼び出して新しいボイスチャットルームを作成します。この時にルームID、マイク・オンに管理者の確認の要否、マイク数などルームの属性情報を伝達します。
3. キャスターは、ルームの作成成功後、`enterSeat`を呼び出して参加します。
4. キャスターは、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時、マイクリストの変更をUI上に更新することができます。
5. キャスターは、マイクリストのメンバーが参加した`onAnchorEnterSeat`のイベント通知も受信します。この時はマイク集音は自動的に開始されます。

![](https://main.qcloudimg.com/raw/256ebe5ce1426b3f175c8c8b68095d5b.png)

```
// 1.キャスターは、ニックネームおよびプロフィール画像を設定します。
mTRTCVoiceRoom.setSelfProfile("my_name", "my_face_url", null);

// 2.キャスターは、createRoomを呼び出してルームを作成します
final TRTCVoiceRoomDef.RoomParam roomParam = new TRTCVoiceRoomDef.RoomParam();
roomParam.roomName = "ルーム名";
roomParam.needRequest = false; // マイク・オンの管理者による確認の要否
roomParam.seatCount = 7; // ルームの座席数。ここは計7席あり、管理者が1席を占有した後、残り6席は視聴者が占有します
roomParam.coverUrl = "ルームカバー図のURL ";
mTRTCVoiceRoom.createRoom(mRoomId, roomParam, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            //3. 0号の席を占有
            mTRTCVoiceRoom.enterSeat(0, new TRTCVoiceRoomCallback.ActionCallback() {
                @Override
                public void onCallback(int code, String msg) {
                    if (code == 0) {
                    }
                }
            });
        }
    }
});

// 4.席の占有に成功した後、onSeatListChangeイベント通知を受信します
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
    // マイクリストの表示
}

// 5. onAnchorEnterSeatイベント通知を受信
@Override
public void onAnchorEnterSeat(TRTCVoiceRoomDef.UserInfo userInfo) {
}
```

[](id:model.step6)
### 手順6：視聴者側の視聴
1. 視聴者側は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 視聴者側は、業務バックエンドに最新のボイスチャットルームのルームリストを取得します。
 >?Demoのボイスチャットルームリストは、デモンストレーションでの使用のみです。ボイスチャットルームリストのビジネスロジックは様々です。Tencent Cloudは、ボイスチャットのルームリスト管理サービスを一時的に提供しませんので、自身でボイスチャットのルームリストを管理してください。
 >
3. 視聴者側は、`getRoomInfoList`を呼び出してルームの詳細情報を取得します。この情報は、キャスター側が`createRoom`を呼び出してボイスチャットルームを作成するときに設定する簡単な説明情報です。
 >!ボイスチャットルームのリストに十分で全体的な情報がある場合は、`getRoomInfoList`の呼び出しに関する手順をスキップできます。
4．視聴者は一つのボイスチャットルームを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに入室できます。
5. 入室後、コンポーネントの`onRoomInfoChange`ルーム属性の変更イベント通知を受信します。この時、ルーム属性を記録し、それに応じた修正を行うことができます。例：UIに表示されるルーム名、マイク・オンにキャスターへの同意をリクエストする要否の記録などを表示します。
6. 入室後は、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時、マイクリストの変更をUI上に更新することができます。
7. 入室後に、マイクリストにキャスターが参加した`onAnchorEnterSeat`というイベント通知も受信することがあります。

![](https://main.qcloudimg.com/raw/33432f97eb632fbb9710a59cba9e4469.png)
```
// 1.視聴者は、ニックネームおよびプロフィール画像を設定します。
mTRTCVoiceRoom.setSelfProfile("my_name", "my_face_url", null);

// 2.業務バックエンドから取得したルームリストをroomListと仮定します
List<Integer> roomList = GetRoomList();

// 3. getRoomInfoListを呼び出すことによって、ルームの詳細情報を取得します
mTRTCVoiceRoom.getRoomInfoList(roomList, new TRTCVoiceRoomCallback.RoomInfoCallback() {
    @Override
    public void onCallback(int code, String msg, List<TRTCVoiceRoomDef.RoomInfo> list) {
        if (code == 0) {
            // この時、自分のUIルームリストを更新することができます
        }
    }
});

// 4.ボイスチャットルームを選択後、roomidを渡して入室します
mTRTCVoiceRoom.enterRoom(roomId, new TRTCVoiceRoomCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
                //入室に成功
            }
        }
});

// 5.入室に成功後、onRoomInfoChangeイベント通知を受信します
@Override
public void onRoomInfoChange(TRTCVoiceRoomDef.RoomInfo roomInfo) {
    mNeedRequest = roomInfo.needRequest;
    mRoomName = roomInfo.roomName;
    // UIはタイトルなどを表示することができます
}

// 6.入室に成功後、onSeatListChangeイベント通知を受信します
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
    // マイクリストの表示
}

// 7. onAnchorEnterSeatイベント通知を受信します
@Override
public void onAnchorEnterSeat(TRTCVoiceRoomDef.UserInfo userInfo) {
}
```

<span id="model.step7"></span>
### 手順7：マイク管理

#### キャスター側
1. `pickSeat`は、対応するマイクおよび視聴者のuserIdを渡し、発言権を付与してマイク・オンできます。ルーム内の全参加者は`onSeatListChange`および`onAnchorEnterSeat`のイベント通知を受信します。
2. `kickSeat`は、対応するマイクを渡した後、キックアウトしてマイク・オフにすることができます。ルーム内の全参加者は`onSeatListChange`および`onAnchorLeaveSeat`のイベント通知を受信します。
3. `muteSeat`は、対応するマイクを渡した後、ミュート/ミュート解除をすることができます。ルーム内の全参加者は`onSeatListChange`および`onSeatMute`のイベント通知を受信します。
4．`closeSeat`は、対応するマイクを送信後、任意のマイクのクローズ/解除をすることができます。クローズ後は、視聴者側はこれ以上マイクを使用することはできません。ルーム内の全参加者は`onSeatListChange`および`onSeatClose`のイベント通知を受信します。

![](https://main.qcloudimg.com/raw/367a0c670d2f9899d0b311ed1f322ea3.png)
#### 視聴者側：

1. `enterSeat`は、対応するマイクを渡した後、マイク・オンにすることができます。ルーム内の全参加者は`onSeatListChange`および`onAnchorEnterSeat`のイベント通知を受信します。
2. `leaveSeat`は、自主的にマイク・オフにします。ルーム内の全参加者は`onSeatListChange`および`onAnchorLeaveSeat`のイベント通知を受信します。

![](https://main.qcloudimg.com/raw/8d385dd387b6255b8512dbff5829e88a.png)

マイク操作後のイベント通知の順番は次のとおりです。callback > onSeatListChange > onAnchorEnterSeatなど独立したイベント。

```
// case1: キャスターによる1号マイクの発言権の付与
mTRTCVoiceRoom.pickSeat(1, "123", new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. callbackコールバックを受信します
        if (code == 0) {
        }
    }
});

// 3. onSeatListChangeコールバックを受信し、マイクリストを更新します
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
}

// 4.単一のマイク変更の通知によって、ここで視聴者が適切な処理を行っているか判断することができます
public void onAnchorEnterSeat(int index, TRTCVoiceRoomDef.UserInfo user) {
}
```

```
// case2: 視聴者による自主的な2号マイクのマイク・オン
mTRTCVoiceRoom.enterSeat(2, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. callbackコールバックを受信します
        if (code == 0) {
        }
    }
});

// 3. onSeatListChangeコールバックを受信し、マイクリストを更新します
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
}

// 4.単一のマイク変更の通知によって、ここでご自身が適切な処理を行っているか判断することができます
public void onAnchorEnterSeat(int index, TRTCVoiceRoomDef.UserInfo user) {
}
```


[](id:model.step8)
### 手順8：招待シグナリングの使用
[マイク管理](#model.step7)では、視聴者がマイク・オン/オフにする場合やキャスターが発言権を付与してマイク・オンにする場合は、相手の同意を必要とせずに直接操作することができます。
Appにおいて相手の同意がなければ、次の操作の業務フローを実施できない場合は、招待シグナリングによって相応のサポートを行うことができます。

#### 視聴者からの自主的なマイク申請：
1. 視聴者側は、`sendInvitation`を呼び出してキャスターのuserIdおよび業務のカスタムコマンドワードなどを渡します。この時、関数は1個のinviteIdを返しこのinviteIdを記録します。
2. キャスター側は、`onReceiveNewInvitation`のイベント通知を受信します。この時、UIはウィンドウをポップアップして、キャスターに同意するかどうか照会することができます。
3. キャスターが同意を選択後、`acceptInvitation`を呼び出してinviteIdを渡します。
4. 視聴者側は、`onInviteeAccepted`のイベント通知を受信し、`enterSeat`を呼び出してマイク・オンにします。

![](https://main.qcloudimg.com/raw/5ccdb15f63efa127aa883ca6a7bcd80d.png)

```
// 視聴者側の視点
// 1. sendInvitationを呼び出し、1号マイクの使用をリクエストします
String inviteId = mTRTCVoiceRoom.sendInvitation("ENTER_SEAT", ownerUserId, "1", null);

// 4.招待の同意リクエストを受信して、正式にマイク・オンにします
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCVoiceRoom.enterSeat(1, null);
    }
}

// キャスター側の視点
// 2.キャスターがリクエストを受信します
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("ENTER_SEAT")) {
        // 3.キャスターが視聴者のリクエストに同意します
         mTRTCVoiceRoom.acceptInvitation(id, null);
    }
}
```
#### キャスターから視聴者を招待してマイク・オン
1. キャスター側は、`sendInvitation`を呼び出して視聴者のuserIdおよび業務のカスタマイズコマンドワードなどを渡します。この時、関数は1個のinviteIdを返しこのinviteIdを記録します。
2. 視聴者側は、`onReceiveNewInvitation`のイベント通知を受信します。この時、UIはウィンドウをポップアップして、視聴者がマイク・オンに同意するかどうかを照会することができます。
3. 視聴者が同意を選択後、`acceptInvitation`を呼び出してinviteIdを渡します。
4. キャスター側は、`onInviteeAccepted`のイベント通知を受信し、`pickSeat`を呼び出し、視聴者に発言権を付与してマイク・オンにします。

![](https://main.qcloudimg.com/raw/5515f49d6e30410e12cd828b75a8db0b.png)

```
// キャスター側の視点
// 1.キャスターはsendInvitationを呼び出し、視聴者123に発言権を付与して2号マイクのマイク・オンをリクエストします
String inviteId = mTRTCVoiceRoom.sendInvitation("PICK_SEAT", "123", "2", null);

// 4.招待の同意リクエストを受信して、正式にマイク・オンにします
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCVoiceRoom.pickSeat(2, null);
    }
}

// 視聴者側の視点
// 2.視聴者がリクエストを受信します
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("PICK_SEAT")) {
        // 3.視聴者がキャスターのリクエストに同意します
         mTRTCVoiceRoom.acceptInvitation(id, null);
    }
}
```


[](id:model.step9)
### 手順9：文字チャットおよび弾幕コメントの実装
- `sendRoomTextMsg`によって通常のテキストメッセージを発信できるようになり、該当するルーム内の全てのキャスターおよび視聴者が`onRecvRoomTextMsg`のコールバックを受信することができます。
 IMバックエンドは、デフォルトのセンシティブワードフィルタルールを備えており、センシティブワードと認識されたテキストメッセージはクラウドに転送されることはありません。
```
// 発信側：テキストメッセージの発信
mTRTCVoiceRoom.sendRoomTextMsg("Hello Word!", null);
// 受信側：テキストメッセージの監視
mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
    @Override
    public void onRecvRoomTextMsg(String message, TRTCVoiceRoomDef.UserInfo userInfo) {
        Log.d(TAG,"が" + userInfo.userName + "から受信したメッセージ:" + message);
    }
});
```
- `sendRoomCustomMsg`によってカスタマイズ（シグナリング）情報を発信することができます。そのルーム内のすべてのキャスターおよび視聴者は`onRecvRoomCustomMsg`のコールバックを受信することができます。
カスタムメッセージは、カスタマイズ信号の送信によく用いられます。例えば、「いいね」情報の発信やブロードキャストに使用します。
```
// 発信側：カスタマイズCmdによって弾幕と「いいね」情報を区別することができます
// eg:「CMD_DANMU」は弾幕コメントを表し、「CMD_LIKE」は「いいね」情報を表します
mTRTCVoiceRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mTRTCVoiceRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// 受信側：カスタムメッセージの監視
mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, String message, TRTCVoiceRoomDef.UserInfo userInfo) {
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
