## コンポーネントの説明

TUIVoiceRoomはオープンソースのオーディオビデオUIコンポーネントであり、プロジェクトにTUIVoiceRoomコンポーネントを統合することにより、数行のコードを書くだけで、Appに「多人数ボイスチャット」などのシーンを組み込むことができます。TUIVoiceRoomは[iOS](https://intl.cloud.tencent.com/document/product/647/37287)などのプラットフォームをサポートしています。基本機能は下図のとおりです。

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/a30e897eabbc6f9104bd41db246f33b1.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/857d3b1651cdf1126f1653e1541b3bba.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/6ddb805c442974d202ef610db643fa39.png" width="250"></td>
</tr>
</tbody></table>


## コンポーネントの統合

### ステップ1：TUIVoiceRoomコンポーネントのダウンロードとインポート
クリックして[Github](https://github.com/tencentyun/TUIVoiceRoom)に進み、コードのクローン/ダウンロードを選択した後、Android/Sourceディレクトリをプロジェクトにコピーし、次のようにインポート動作を完了します。
- `setting.gradle`へのインポートを完了します。以下をご参照ください。
```
include ':Source'
```
- appのbuild.gradleファイルにSourceに対する依存関係を追加します。
```
api project(':Source')
```
- ルートディレクトリの`build.gradle`ファイルに`TRTC SDK`および`IM SDK`の依存関係を追加します。
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

### ステップ2：権限の設定および難読化ルール
AndroidManifest.xmlにAppの権限を設定します。SDKには次の権限が必要です（6.0以上のAndroidシステムではマイクの権限などを動的に申請する必要があります）。

```
<uses-permission android:name="android.permission.INTERNET" />              
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

proguard-rules.proファイルでは、SDK関連を非難読化リストに追加します。

```
-keep class com.tencent.** { *; }
```

### ステップ3：初期化およびログイン
```java
    // 1.初期化
    TRTCVoiceRoom mTRTCVoiceRoom = TRTCVoiceRoom.sharedInstance(this);
    mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
    );
		  // 2.ログイン
    mTRTCVoiceRoom.login(SDKAppID, userId, userSig, new TRTCVoiceRoomCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
            //ログイン成功
            }
        }
    });
```

**パラメータの説明：**
- **SDKAppID**：**TRTCアプリケーションID**です。Tencent Cloud TRTCサービスをアクティブ化していない場合は、[Tencent Cloud TRTCコンソール](https://console.cloud.tencent.com/trtc/app)に進み、新しいTRTCアプリケーションを作成した後、**アプリケーション情報**をクリックすると、SDKAppID情報が次の図のように表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**：**TRTC アプリケーションキー**であり、SDKAppIdに対応しています。[TRTCアプリケーション管理](https://console.cloud.tencent.com/trtc/app)に進むと、SecretKey情報が上の図のように表示されます。
- **userId**：現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。業務の実際のアカウントシステムと組み合わせてご自身で設定することをお勧めします。
- **userSig**：SDKAppId、userId，Secretkeyなどの情報に基づく計算によって得られるセキュリティ保護署名です。[ここ](https://console.cloud.tencent.com/trtc/usersigtool)をクリックするとデバッグ用のuserSigがオンラインで直接生成されます。また当社の[デモプロジェクト](https://github.com/tencentyun/TUIVoiceRoom/blob/main/Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java#L88)を参照してご自身で計算することもできます。その他の情報については、[UserSigの計算、使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### ステップ4：ボイスチャットルームの実装
1. **管理者によるボイスチャットルーム作成の実装[TRTCVoiceRoom#createRoom](https://intl.cloud.tencent.com/document/product/647/37339)**
```java
// 1.管理者が呼び出してルームを作成
int roomId = 12345; //ルームid
final TRTCVoiceRoomDef.RoomParam roomParam = new TRTCVoiceRoomDef.RoomParam();
roomParam.roomName = "ルーム名";
roomParam.needRequest = false; // マイク・オンに対する管理者の確認の要否
roomParam.seatCount = 7; // ルームの座席数。ここでは計7席あり、管理者が1席を占め、残り6席がリスナーとなります
roomParam.coverUrl = "ルームカバー図のURL ";
mTRTCVoiceRoom.createRoom(roomId, roomParam, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
				//作成に成功
        }
    }
});
```
2. **リスナーのボイスチャットルーム入室の実装[TRTCVoiceRoom#enterRoom](https://intl.cloud.tencent.com/document/product/647/37339)**
```java
// 1.リスナーが呼び出して入室
mTRTCVoiceRoom.enterRoom(roomId, new TRTCVoiceRoomCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
            //入室に成功 
            }
        }
});
```
3. **リスナーの自主的なマイク・オンの実装[TRTCVoiceRoom#enterRoom](https://intl.cloud.tencent.com/document/product/647/37339)**
```java
// 1: リスナーが呼び出してマイク・オン
int seatIndex = 2; //マイクのindex
mTRTCVoiceRoom.enterSeat(seatIndex, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
        //操作に成功しました
        }
    }
});

// 2. onSeatListChangeコールバックを受信し、マイクリストを更新します
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
}
```
4. **管理者による視聴者発言招待の実装[TRTCVoiceRoom#pickSeat](https://intl.cloud.tencent.com/document/product/647/37339)**
```java
// 1: 管理者が呼び出して、視聴者が発言できるように招待
int seatIndex = 2; //マイクのindex
String userId = "123"; //マイク・オンが必要なユーザーid
mTRTCVoiceRoom.pickSeat(1, userId, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
				//操作に成功しました
        }
    }
});

// 2. onSeatListChangeコールバックを受信し、マイクリストを更新します
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
}
```
5. **リスナーによるマイク・オン申請の実装 [TRTCVoiceRoom#sendInvitation](https://intl.cloud.tencent.com/document/product/647/37339)**
```java
// リスナー側の視点
// 1.リスナーが呼び出してマイク・オンを申請
String seatIndex = "1"; //マイクのindex
String userId = "123"; //ユーザーid
String inviteId = mTRTCVoiceRoom.sendInvitation("takeSeat", userId, seatIndex, null);

// 2.招待のリクエスト同意を受信し、正式にマイク・オンになります
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCVoiceRoom.enterSeat(index, null);
    }
}

// 管理者側の視点
// 1.管理者がリクエストを受信します
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("takeSeat")) {
        // 2.管理者がリスナーのリクエストに同意します
         mTRTCVoiceRoom.acceptInvitation(id, null);
    }
}
```
6. **管理者によるマイク・オンへの招待の実装 [TRTCVoiceRoom#sendInvitation](https://intl.cloud.tencent.com/document/product/647/37339)**
```java
// 管理者側の視点
// 1.管理者が呼び出して、視聴者が発言できるように招待をリクエスト
String seatIndex = "1"; //マイクのindex
String userId = "123"; //ユーザーid
String inviteId = mTRTCVoiceRoom.sendInvitation("pickSeat", userId, seatIndex, null);

// 2.招待のリクエスト同意を受信し、正式にマイク・オンになります
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCVoiceRoom.pickSeat(index, null);
    }
}

// リスナー側の視点
// 1.リスナーがリクエストを受信します
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("pickSeat")) {
        // 2.リスナーが管理者のリクエストに同意します
         mTRTCVoiceRoom.acceptInvitation(id, null);
    }
}
```
7. **テキストチャットの実装[TRTCVoiceRoom#sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/37339)**
```java
// 発信側：テキストメッセージの発信
mTRTCVoiceRoom.sendRoomTextMsg("Hello Word!", null);
// 受信側：テキストメッセージのモニタリング
mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
  @Override
  public void onRecvRoomTextMsg(String message, TRTCVoiceRoomDef.UserInfo userInfo) {
      Log.d(TAG,"が" + userInfo.userName + "から受信したメッセージ:" + message);
  }
});
```
8. **弾幕コメントの実装 [TRTCVoiceRoom#sendRoomCustomMsg](https://intl.cloud.tencent.com/document/product/647/37339)**
```java
// 発信側：カスタマイズCmdによって弾幕と「いいね」情報を区別することができます
// eg:「CMD_DANMU」は弾幕コメントを表し、「CMD_LIKE」は「いいね」情報を表します
mTRTCVoiceRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mTRTCVoiceRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// 受信側：カスタムメッセージのモニタリング
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

## よくあるご質問
ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。
