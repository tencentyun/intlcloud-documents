## コンポーネントの説明

`TUILiveRoom`はオープンソースのビデオライブストリーミング`UI`コンポーネントであり、プロジェクトに`TUILiveRoom`コンポーネントを統合することにより、数行のコードを書くだけで、`App`に「ビデオインタラクティブストリーミング」のシーンを組み込むことができます。`TUILiveRoom`には`Android`、`iOS`などのプラットフォーム用のソースコードが含まれます。基本機能は下図のとおりです。
<table>
<tr>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/34337da1f6427b9a834f6562eba5c663.jpg"/></td>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/52eb1656b5a892e6da65f49a1d503735.jpg"/></td>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/70c9e1e7290592f8c7892b236fb1061e.jpg"/></td>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/ed8c3666aa03951c6d0d9cfe2dccc495.jpg"/></td>
</tr>
</table>

[](id:model)

## コンポーネントの統合
[](id:model.step1)
### ステップ1：TUILiveRoomコンポーネントのダウンロードとインポート
クリックして[Github](https://github.com/tencentyun/TUILiveRoom)に進み、コードのクローン/ダウンロードを選択した後、`Android/Beauty`、`Android/Debug`、`Android/Source`ディレクトリをプロジェクトにコピーし、次のようにインポート動作を完了します。

- `setting.gradle`へのインポートを完了します。以下をご参照ください。
```
include ':Beauty'
include ':Source'
include ':Debug'
```
- `app`の`build.gradle`ファイルに`Source`に対する依存関係を追加します。
```
api project(":Source")
```
- ルートディレクトリの`build.gradle`ファイルに`TRTC SDK`および`IM SDK`の依存関係を追加します。
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

[](id:model.step2)
### ステップ2：権限の設定および難読化ルール
1. AndroidManifest.xmlにAppの権限を設定します。SDKには次の権限が必要です（6.0以上のAndroidシステムではカメラ、ストレージ読み取りの権限を動的に申請する必要があります）。
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
2. proguard-rules.proファイルでは、SDK関連クラスを非難読化リストに追加します。
<dx-codeblock>
::: java java
-keep class com.tencent.** { *; }
:::
</dx-codeblock>

[](id:model.step3)
### ステップ3：コンポーネントの初期化およびログイン
<dx-codeblock>
::: java java
TRTCLiveRoom mLiveRoom = TRTCLiveRoom.sharedInstance(this);
//useCDNFirst：trueは一般視聴者のCDN経由の視聴、falseは一般視聴者の低レイテンシーによる視聴を表します
//yourCDNPlayDomain：CDN視聴時に設定する再生ドメイン名を表します。
TRTCLiveRoomDef.TRTCLiveRoomConfig config = 
    new TRTCLiveRoomDef.TRTCLiveRoomConfig(useCDNFirst, CDNPlayDomain);
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

**パラメータの説明：**
- **SDKAppID**：**TRTCアプリケーションID**です。Tencent Cloud TRTCサービスをアクティブ化していない場合は、[Tencent Cloud TRTCコンソール](https://console.cloud.tencent.com/trtc/app)に進み、新しいTRTCアプリケーションを作成した後、**アプリケーション情報**をクリックすると、SDKAppID情報が次の図のように表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**：**TRTC アプリケーションキー**であり、SDKAppIdに対応しています。[TRTCアプリケーション管理](https://console.cloud.tencent.com/trtc/app)に進むと、SecretKey情報が上の図のように表示されます。
- **userId**：現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。業務の実際のアカウントシステムと組み合わせてご自身で設定することをお勧めします。
- **userSig**：SDKAppId、userId，Secretkeyなどの情報に基づく計算によって得られるセキュリティ保護署名です。[ここ](https://console.cloud.tencent.com/trtc/usersigtool)をクリックするとデバッグ用のuserSigがオンラインで直接生成されます。また当社の[デモプロジェクト](https://github.com/tencentyun/TUIRoom/blob/main/Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java#L88)を参照してご自身で計算することもできます。その他の情報については、[UserSigの計算、使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。
- **config**：グローバルコンフィギュレーション情報。ログイン時に初期化してください。ログイン後は変更できなくなります。
- **useCDNFirst** ：視聴者の視聴方式の設定に使用します。trueは、一般視聴者のCDN経由での視聴を表し、料金は安価ですがレイテンシーは高めです。falseは、一般視聴者の低レイテンシーによる視聴を表し、料金はCDN とマイク接続の間ですが、遅延を1s以内に抑えることができます。
- **CDNPlayDomain**：useCDNFirstの設定をtrueにした時に有効になり、CDN経由の視聴の再生ドメイン名の指定に利用します。**CSSコンソール** > [ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)ページからログインし、設定することができます。
- **callback**：ログインのコールバック。成功時にcodeは0になります。



[](id:model.step4)
### ステップ4：ビデオインタラクティブストリーミングルームの実装
1. **キャスターが配信開始 [TRTCLiveRoom#createRoom](https://intl.cloud.tencent.com/document/product/647/37333)**
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
2. **視聴者側が視聴 [TRTCLiveRoom#enterRoom](https://intl.cloud.tencent.com/document/product/647/37333)**
```java
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
				//mTXCloudVideoViewは視聴者側の再生viewです
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
```

3. **視聴者とキャスターがマイク接続 [TRTCLiveRoom#requestJoinAnchor](https://intl.cloud.tencent.com/document/product/647/37333)**
<dx-codeblock>
::: java java
// 1.視聴者側がマイク接続のリクエストを送信します
// LINK_MIC_TIMEOUTはタイムアウト時間です
mLiveRoom.requestJoinAnchor(mSelfUserId + "あなたとのマイク接続をリクエスト", LINK_MIC_TIMEOUT
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
4. **キャスター間のPK [TRTCLiveRoom#requestRoomPK](https://intl.cloud.tencent.com/document/product/647/37333)**
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
5. **テキストチャットの実装[TRTCLiveRoom#sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/37333)**
<dx-codeblock>
::: java java
// 発信側：テキストメッセージの発信
mLiveRoom.sendRoomTextMsg("Hello Word!", null);
// 受信側：テキストメッセージのモニタリング
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
	@Override
	public void onRecvRoomTextMsg(String roomId, 
			String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo) {
			Log.d(TAG,"が" + userInfo.userName + "から受信したメッセージ:" + message);
	}
});
:::
</dx-codeblock>
6. **弾幕コメントの実装 [TRTCLiveRoom#sendRoomCustomMsg](https://intl.cloud.tencent.com/document/product/647/37333)**
<dx-codeblock>
::: java java
// 発信側：カスタマイズCmdによって弾幕と「いいね」情報を区別することができます
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
            Log.d(TAG, "が" + userInfo.userName + "から受信した弾幕コメント:" + message);
        } else if ("CMD_LIKE".equals(cmd)) {
            // 「いいね」情報の受信
            Log.d(TAG, userInfo.userName + "いいねを付けました！");
        }
    }
});
:::
</dx-codeblock>

## よくあるご質問
ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。
