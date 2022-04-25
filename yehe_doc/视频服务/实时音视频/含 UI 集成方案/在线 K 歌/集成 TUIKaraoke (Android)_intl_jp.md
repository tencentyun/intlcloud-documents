## コンポーネントの説明
TUIKaraokeはオープンソースのオーディオビデオUIコンポーネントであり、プロジェクトにTUIKaraokeコンポーネントを統合することにより、数行のコードを書くだけで、アプリケーションにオンラインカラオケシーンを組み込むことができ、カラオケ、マイク管理、ギフトの送付と受領、テキストチャットなどのTRTCのKTVシーンでの関連機能を体験できるようになります。TUIKaraokeはiOSプラットフォーム用のソースコードもサポートしています。基本機能は下図のとおりです。

<table>
     <tr>
         <th width=20%  style="text-align:center">チャット</th>
         <th width=20%  style="text-align:center">オーディオエフェクト管理</th>
     </tr>
<tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/819e86970cecabcb10143a49a4759b32.png" width="400"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/3616f2a5193c26bad447744ed7bf417d.png" width="400"></td>
</tr>
</table>



## コンポーネントの統合
### ステップ1：TUIKaraokeコンポーネントのダウンロードとインポート

クリックして[Github](https://github.com/tencentyun/TUIKaraoke)に進み、コードのクローン/ダウンロードを選択した後、Androidディレクトリ下のSource、Debugディレクトリをプロジェクトにコピーし、次のようにインポート動作を完了します。
- `setting.gradle`へのインポートを完了します。以下をご参照ください。
```
include ':Source'
include ':Debug'
```
- appのbuild.gradleファイルにTUIKaraokeに対する依存関係を追加します。
```
api project(':Source')
```
- ルートディレクトリの`build.gradle`ファイルに`TRTC SDK`および`IM SDK`の依存関係を追加します。
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTCl:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

### ステップ2：権限の設定および難読化ルール

AndroidManifest.xmlにAppの権限を設定します。SDKには次の権限が必要です（6.0以上のAndroidシステムではマイク、ストレージ読み取りの権限などを動的に申請する必要があります）。

```
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />        // ユースケース：フローティングウィンドウ機能にはこの権限が必要です。
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />                  // ユースケース：Bluetoothイヤホンを使用する場合はこの権限が必要です。
```

proguard-rules.proファイルでは、SDK関連を非難読化リストに追加します。
```
-keep class com.tencent.** { *; }
```

### ステップ3：初期化およびログイン 
インターフェースに関する詳細については、[TUIKaraoke](https://intl.cloud.tencent.com/document/product/647/41943)をご参照ください。

```java
  // 1.初期化
  TRTCKaraokeRoom mTRTCKaraokeRoom = TRTCKaraokeRoom.sharedInstance(this);
  mTRTCKaraokeRoom.setDelegate(this);
  // 2.ログイン
  mTRTCKaraokeRoom.login(SDKAppID, UserID, UserSig, new TRTCKaraokeRoomCallback.ActionCallback() {
      @Override
      public void onCallback(int code, String msg) {
          if (code == 0) {
          //ログイン成功
          }
      }
  });
```
**パラメータの説明**：
- **SDKAppID**：**TRTCアプリケーションID**です。Tencent Cloud TRTCサービスをアクティブ化していない場合は、[Tencent Cloud TRTCコンソール](https://console.cloud.tencent.com/trtc/app)に進み、新しいTRTCアプリケーションを作成した後、**アプリケーション情報**をクリックすると、SDKAppID情報が次の図のように表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**：**TRTCアプリケーションキー**であり、SDKAppIdに対応しています。[TRTCアプリケーション管理](https://console.cloud.tencent.com/trtc/app)に進むと、SecretKey情報が上の図のように表示されます。
- **userId**：現在のユーザーのIDです。文字列形式で、長さは32バイト以内とし、特殊文字の使用はサポートしていません。英語または数字の使用をお勧めします。業務の実際のアカウントシステムと組み合わせてご自身で設定することができます。
- **userSig**：SDKAppId、userId、Secretkeyなどの情報に基づく計算によって得られるセキュリティ保護署名です。[ここ](https://console.cloud.tencent.com/trtc/usersigtool)をクリックするとデバッグ用のUserSigがオンラインで直接生成されます。また当社の[TUICallingデモプロジェクト](https://github.com/tencentyun/TUICalling/blob/main/Android/App/src/main/java/com/tencent/liteav/demo/LoginActivity.java#L74)を参照してご自身で計算することもできます。その他の情報については、[UserSigの計算、使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### ステップ4：オンラインKTVシーンの実装
1. **キャスターがルームを作成[TUIKaraoke.createRoom](https://intl.cloud.tencent.com/document/product/647/41943)**
```java
int roomId = "ルームID";
TRTCKaraokeRoomDef.RoomParam roomParam = new TRTCKaraokeRoomDef.RoomParam();
roomParam.roomName = "ルーム名";
roomParam.needRequest = false; // マイク・オンに対する管理者の確認の要否
roomParam.seatCount = 8;       //ルームの座席数。計8席あります
roomParam.coverUrl = "ルームカバー図のURL";
mTRTCKaraokeRoom.createRoom(roomId, roomParam, new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
      if (code == 0) {
        //作成に成功
      }
    }
});
```
2. **リスナーが入室[TUIKaraoke.enterRoom](https://intl.cloud.tencent.com/document/product/647/41943)**
```java
mTRTCKaraokeRoom.enterRoom(roomId, new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
        //入室に成功 
        }
    }
});
```
3. **リスナーが自主的にマイク・オン [TUIKaraoke.enterSeat](https://intl.cloud.tencent.com/document/product/647/41943)**
```java
// 1.リスナーが呼び出してマイク・オン
int seatIndex = 1;
mTRTCKaraokeRoom.enterSeat(seatIndex, new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
        //マイク・オン成功
        }
    }
});
// 2.onSeatListChangeコールバックを受信し、マイクリストを更新します
@Override
public void onSeatListChange(final List<TRTCKaraokeRoomDef.SeatInfo> seatInfoList) {
}
```

>? マイク管理に関連するその他の操作については、[TUIKaraokeインターフェースドキュメント](https://intl.cloud.tencent.com/document/product/647/41943)をご参照の上、必要に応じて実装するか、または当社の[TUIKaraokeデモプロジェクト](https://github.com/tencentyun/TUIKaraoke/)をご参照ください。

4. **音楽再生とKTV体験シーンの実装**
ご自身の業務に応じて音楽IDおよびURLリンクを取得し、楽曲を再生できます。インターフェースの詳細については[TUIKaraoke音楽再生インターフェース](https://intl.cloud.tencent.com/document/product/647/41943#.E9.9F.B3.E4.B9.90.E6.92.AD.E6.94.BE.E6.8E.A5.E5.8F.A32)をご参照ください。
```java
//音楽の再生
mTRTCKaraokeRoom.startPlayMusic(musicID,url);
//音楽の停止
mTRTCKaraokeRoom.stopPlayMusic();
```

上記の手順が完了すると、KTVの基本機能を実装できます。業務上、テキストチャット、ギフト送付などの機能も必要な場合、次の機能を統合することができます。

### ステップ5：テキストチャット機能（オプション）
各キャスターまたはリスナー間のテキストチャット機能を実装したい場合は、次のメソッドによってチャットメッセージを送受信することができます。
インターフェースに関する詳細については、[TRTCKaraokeRoom.sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/41943#sendroomtextmsg)をご参照ください。
```java
// 発信側：テキストメッセージの発信
mTRTCKaraokeRoom.sendRoomTextMsg("Hello Word!", new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            //送信に成功
        }
    }
});
// 受信側：テキストメッセージのモニタリング
mTRTCKaraokeRoom.setDelegate(new TRTCKaraokeRoomDelegate() {
  @Override
  public void onRecvRoomTextMsg(String message, TRTCKaraokeRoomDef.UserInfo userInfo) {
      Log.d(TAG,"が" + userInfo.userName + "から受信したメッセージ:" + message);
  }
});
```

### ステップ6：ギフト送付機能（オプション）
ギフト送付および受領機能を実装したい場合は、次のメソッドによってギフトを送付または受領し、表示することができます。
```java
// 送信側：カスタマイズした「CMD_GIFT」によってギフトメッセージを区別
mTRTCKaraokeRoom.sendRoomCustomMsg("CMD_GIFT",date, new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            //送信に成功
        }
    }
});

// 受信側：ギフトメッセージのモニタリング
mTRTCKaraokeRoom.setDelegate(new TRTCKaraokeRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, String message, TRTCKaraokeRoomDef.UserInfo userInfo) {
        if ("CMD_GIFT".equals(cmd)) {
            // ギフトメッセージの受信
            Log.d(TAG, "" + userInfo.userName + "からのギフトを受信:" + message);
        }
    }
});
```

## よくあるご質問
### TUIKaraokeコンポーネントはボイスチェンジ、キー調整、リバーブなどのオーディオエフェクト機能をサポートしていますか。
サポートしています。具体的には[TUIKaraokeデモプロジェクト](https://github.com/tencentyun/TUIKaraoke/blob/main/Android/Source/src/main/java/com/tencent/liteav/tuikaraoke/ui/audio/AudioEffectPanel.java)をご参照ください。

>? ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。
