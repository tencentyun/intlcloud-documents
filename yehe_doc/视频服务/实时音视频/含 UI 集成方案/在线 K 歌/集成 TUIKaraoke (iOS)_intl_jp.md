## コンポーネントの説明

TUIKaraokeはオープンソースのオーディオビデオUIコンポーネントであり、プロジェクトにTUIKaraokeコンポーネントを統合することにより、数行のコードを書くだけで、アプリケーションにオンラインカラオケシーンを組み込むことができ、カラオケ、マイク管理、ギフトの送付と受領、テキストチャットなどのTRTCのKTVシーンでの関連機能を体験できるようになります。TUIKaraokeはAndroidプラットフォーム用のソースコードもサポートしています。基本機能は下図のとおりです。

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

クリックして[Github](https://github.com/tencentyun/TUIKaraoke)に進み、コードのクローン/ダウンロードを選択した後、iOSディレクトリ下の`Source`、`Resources`、`TXAppBasic`フォルダ、`TUIKaraoke.podspec`ファイルをプロジェクトにコピーし、次のようにインポート動作を完了します。

- `Podfile`ファイルにインポートコマンドを追加します。次をご参照ください。
```
pod 'TUIKaraoke', :path => "./", :subspecs => ["TRTC"]
pod 'TXLiteAVSDK_TRTC'
pod 'TXAppBasic', :path => "TXAppBasic/"
```
- 端末を開き、`Podfile`ファイルのあるディレクトリ下に進み、インストールコマンドを実行します。次をご参照ください。
```
pod install
```

### ステップ2：権限の設定
プロジェクトのinfo.plistファイルの中でAppの権限を設定します。SDKには以下の権限が必要です（iOSシステムではマイクを動的に申請する必要があります）。
```
 <key>NSMicrophoneUsageDescription</key>
    <string>Karaokeにはマイクへのアクセス権限が必要です</string>
```


### ステップ3：初期化およびログイン
インターフェースに関する説明については、[TUIKaraoke](https://intl.cloud.tencent.com/document/product/647/41942)をご参照ください。
```swift
  // 1.初期化
  let karaokeRoom = TRTCKaraokeRoom.shared()
  karaokeRoom.setDelegate(delegate: self)
  // 2.ログイン
  karaokeRoom.login(SDKAppID: Int32(SDKAppID), UserId: UserId, UserSig: ProfileManager.shared.curUserSig()) { code, message in
		if code == 0 {
			//ログイン成功
		}
  }
```
**パラメータの説明**：
- **SDKAppID**：**TRTCアプリケーションID**です。Tencent Cloud TRTCサービスをアクティブ化していない場合は、[Tencent Cloud TRTCコンソール](https://console.cloud.tencent.com/trtc/app)に進み、新しいTRTCアプリケーションを作成した後、**アプリケーション情報**をクリックすると、SDKAppID情報が次の図のように表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**：**TRTCアプリケーションキー**であり、SDKAppIdに対応しています。[TRTCアプリケーション管理](https://console.cloud.tencent.com/trtc/app)に進むと、SecretKey情報が上の図のように表示されます。
- **userId**：現在のユーザーのIDです。文字列形式で、長さは32バイト以内とし、特殊文字の使用はサポートしていません。英語または数字の使用をお勧めします。業務の実際のアカウントシステムと組み合わせてご自身で設定することができます。
- **userSig**：SDKAppId、userId、Secretkeyなどの情報に基づく計算によって得られるセキュリティ保護署名です。[ここ](https://console.cloud.tencent.com/trtc/usersigtool)をクリックするとデバッグ用のUserSigがオンラインで直接生成されます。また当社の[TUICallingデモプロジェクト](https://github.com/tencentyun/TUICalling/blob/main/Android/App/src/main/java/com/tencent/liteav/demo/LoginActivity.java#L74)を参照してご自身で計算することもできます。その他の情報については、[UserSigの計算、使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。


### ステップ4：オンラインKTVシーンの実装
1. **キャスターがルームを作成[TUIKaraoke.createRoom](https://intl.cloud.tencent.com/document/product/647/41942)**
```swift
int roomId = "ルームID";
let param = RoomParam.init()
param.roomName = "ルーム名";
param.needRequest = false; // 管理者によるマイク・オン確認の要否
param.seatCount = 8;       //ルームの座席数。計8席あります
param.coverUrl = "ルームカバー図のURL";

karaokeRoom.createRoom(roomID: Int32(roomInfo.roomID), roomParam: param) { [weak self] (code, message) in
	guard let `self` = self else { return }
	if code == 0 {
        //作成に成功
	}
}
```
2. **リスナーが入室[TUIKaraoke.enterRoom](https://intl.cloud.tencent.com/document/product/647/41942)**
```swift
karaokeRoom.enterRoom(roomID: roomInfo.roomID) { [weak self] (code, message) in
	guard let `self` = self else { return }
	if code == 0 {
		//入室に成功 
	}
}
```
3. **リスナーが自主的にマイク・オン[TUIKaraoke.enterSeat](https://intl.cloud.tencent.com/document/product/647/41942)**
```swift
// 1.リスナーが呼び出してマイク・オン
int seatIndex = 1; 
karaokeRoom.enterSeat(seatIndex: seatIndex) { [weak self] (code, message) in
	guard let `self` = self else { return }
	if code == 0 {
		//マイク・オン成功
	}
}
// 2.onSeatListChangeコールバックを受信し、マイクリストを更新します
func onSeatListChange(seatInfoList: [SeatInfo]) {
}
```

>? マイク管理に関連するその他の操作については、[TUIKaraokeインターフェースドキュメント](https://intl.cloud.tencent.com/document/product/647/41942)をご参照の上、必要に応じて実装するか、または[TUIKaraokeデモプロジェクト](https://github.com/tencentyun/TUIKaraoke/)をご参照ください。

4. **音楽再生とKTV体験シーンの実装**
ご自身の業務に応じて音楽IDおよびURLリンクを取得し、楽曲を再生できます。詳細については[TUIKaraoke音楽再生インターフェース](https://intl.cloud.tencent.com/document/product/647/41942#.E9.9F.B3.E4.B9.90.E6.92.AD.E6.94.BE.E6.8E.A5.E5.8F.A32)をご参照ください。
```swift
//音楽の再生
karaokeRoom.startPlayMusic(musicID: musicID, originalUrl: muscicLocalPath, accompanyUrl: accompanyLocalPath);
//音楽の停止
karaokeRoom.stopPlayMusic();
```

上記の手順が完了すると、KTVの基本機能を実装できます。業務上、チャット、ギフト送付などの機能も必要な場合、次の機能を統合することができます。

### ステップ6：テキストチャット機能（オプション）
各キャスターまたはリスナー間のテキストチャット機能を実装したい場合は、次のメソッドによってチャットメッセージを送受信することができます。
インターフェースに関する説明については、[TRTCKaraokeRoom.sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/41942#sendroomtextmsg)をご参照ください。
```swift
// 発信側：テキストメッセージの発信
karaokeRoom.sendRoomTextMsg(message: message) { [weak self] (code, message) in
	if code == 0 {
		//送信に成功
	}
}
// 受信側：テキストメッセージのモニタリング
karaokeRoom.setDelegate(delegate: self)
func onRecvRoomTextMsg(message: String, userInfo: UserInfo) {
	debugPrint("" + userInfo.userName + "から受信したメッセージ：" + message)
}
```

### ステップ7：ギフト送付機能（オプション）
ギフト送付および受領機能を実装したい場合は、次のメソッドによってギフトを送付または受領し、表示することができます。
```swift
// 送信側：カスタマイズした「IMCMD_GIFT」によってギフトメッセージを区別
karaokeRoom.sendRoomCustomMsg(cmd: kSendGiftCmd, message: message) { code, msg in
	if (code == 0) {
		//送信に成功
	}
}

// 受信側：ギフトメッセージのモニタリング
karaokeRoom.setDelegate(delegate: self)
func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: UserInfo) {
	if cmd == kSendGiftCmd {
		debugPrint("" + userInfo.userName + "から受領したギフト：" + message)
	}
}
```

## よくあるご質問

### TUIKaraokeコンポーネントはボイスチェンジ、キー調整、リバーブなどのオーディオエフェクト機能をサポートしていますか。
サポートしています。具体的には[TUIKaraokeデモプロジェクト](https://github.com/tencentyun/TUIKaraoke/blob/main/iOS/Source/ui/TRTCKTVViewController/SubViews/TRTCKaraokeSoundEffectAlert.swift)をご参照ください。

? ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。