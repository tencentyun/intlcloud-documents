## デモンストレーション

>! 現在、このプロジェクトはFlutter2.0をサポートしていません。Flutter2.0バージョンを使用している場合は、あらかじめバージョンをダウングレードしてください。

[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)してDemoをインストールし、ボイスチャット、マイクのオン・オフ、低遅延音声インタラクションなどのボイスチャットのユースケースにおけるTRTCの関連機能を含む、ボイスサロンの機能を体験できます。


ボイスサロン機能をすばやく実装する必要がある場合、当社が提供するDemoをもとにアダプタを修正するか、または当社が提供するTRTCChatSalonコンポーネントでUIのカスタマイズを実装することができます。

[](id:DemoUI)

## DemoのUIの再利用

[](id:ui.step1)
### 手順1：アプリケーションの新規作成
1．TRTCコンソールにログインし、【開発支援】>【[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. アプリケーション名（例：`TestChatSalon`）を入力し、【作成】をクリックします。

>!本機能はTencent Cloud[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。



[](id:ui.step2)
### 手順2：SDKおよびDemoソースコードをダウンロード
1. 実際の業務ニーズに基づき、SDKおよび付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、【ダウンロードしました。次のステップ】をクリックします。

[](id:ui.step3)
### 手順3：Demoプロジェクトファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `/example/lib/debug/GenerateTestUserSig.dart`ファイルを見つけて開きます。
3.`GenerateTestUserSig.dart`ファイル内の関連パラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトはPLACEHOLDER。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトはPLACEHOLDER。実際のキー情報を設定してください。</ul>
4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。


>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**のこの手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)
### 手順4：コンパイル実行

>! Androidは実際のマシンで実行する必要があり、エミュレーターのデバッグはサポートされていません。

1. `flutter pub get`を実行します。
2. コンパイルを実行し、デバッグを行います。
<dx-tabs>
:::  Android\s端末
1. `flutter run`を実行します。
2. Android Studio（3.5およびそれ以降のバージョン）を使用して、ソースプロジェクトを開き、【実行】をクリックすれば完了です。
:::
::: iOS\s端末
1. XCode（11.0およびそれ以降のバージョン）を使用して、ソースコードディレクトリの `/iosプロジェクト` を開きます。
2. コンパイルを行い、Demoプロジェクトを実行します。
:::
</dx-tabs>

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
[ソースコード](https://github.com/c1avie/TRTCChatSalon)のtrtcchatsalondemoフォルダには、uiとmodelという2つのサブフォルダがあり、modelフォルダには再利用できるオープンソースコンポーネントTRTCChatSalonが含まれています。`TRTCChatSalon.dart`ファイルでこのコンポーネントが提供するインターフェース関数を確認し、対応するインターフェースを使用してカスタマイズしたUIを実装することができます。
![](https://main.qcloudimg.com/raw/fcf694c8550664623414604d14ffcd94.png)

[](id:model.step1)
### 手順1：SDKへの統合
ボイスサロンコンポーネントtrtcchatsalondemoは、[TRTC SDK](https://pub.dev/packages/tencent_trtc_cloud)と[IM SDK](https://pub.dev/packages/tencent_im_sdk_plugin)に依存しています。`pubspec.yaml`を設定することで、更新を自動的にダウンロードできます。

プロジェクトの`pubspec.yaml` に次の依存関係を記述します。
```
dependencies:
  tencent_trtc_cloud: 最新バージョン番号
  tencent_im_sdk_plugin: 最新バージョン番号
```

[](id:model.step2)

### 手順2：権限の設定および難読化ルール
#### iOS端末
`Info.plist`にカメラとマイクの権限申請を追加する必要があります。
```
<key>NSMicrophoneUsageDescription</key>
<string>通常の音声通話が行えるようにマイクの権限を承認します</string>
```
#### Android端末
1. `/android/app/src/main/AndroidManifest.xml`ファイルを開きます。
2. `xmlns:tools="http://schemas.android.com/tools"` をmanifestの中に追加します。
3. `tools:replace="android:label"をapplicationの中に追加します。
>? この手順を実行しないと、[Android Manifest merge failedコンパイルの失敗](https://intl.cloud.tencent.com/document/product/647/39242)という問題が発生します。

![アイコン](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)


[](id:model.step3)
### 手順3：TRTCChatSalonコンポーネントのインポート
次のディレクトリ内のすべてのファイルをプロジェクトにコピーします。
```
lib/TRTCChatSalonDemo/model/
```

<span id="model.step4"></span>
### 手順4：コンポーネントの作成およびログイン
1. `sharedInstance`インターフェースを呼び出すと、TRTCChatSalonコンポーネントのインスタンスオブジェクトを作成できます。
2. `registerListener`関数を呼び出して、コンポーネントのイベント通知を登録します。
3. `login`関数を呼び出してコンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
<table>
<tr>
<th>パラメータ名</th>
<th>作用</th>
</tr>
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
</table>

```
TRTCChatSalon trtcVoiceRoom = await TRTCChatSalon.sharedInstance();
trtcVoiceRoom.registerListener(onVoiceListener);
ActionCallback resValue = await trtcVoiceRoom.login(
    GenerateTestUserSig.sdkAppId,
    userId,
    GenerateTestUserSig.genTestSig(userId),
);
if (resValue.code == 0) {
    //ログイン成功
}
```

[](id:model.step5)

### 手順5：キャスター側での配信開始

1. キャスターは、[手順4](#model.step4) でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. キャスターは、`createRoom`を呼び出して新しいボイスサロンを作成します。このとき、ルームID、ルーム名などルームの属性情報を渡します。
3. キャスターは、メンバーが参加した`TRTCChatSalonDelegate.onAudienceEnter`のイベント通知を受信します。このとき、マイク集音は自動的に開始されます。

![](https://tccweb-1258344699.cos.ap-nanjing.myqcloud.com/sdk/trtc/chatsalon/chatsalon_zbo.png)

```
// 1.キャスターは、ニックネームおよびプロフィール画像を設定します
trtcVoiceRoom.setSelfProfile("my_name", "my_face_url", null);

// 2.キャスターは、createRoomを呼び出してルームを作成します
ActionCallback resp = await trtcVoiceRoom.createRoom(
    roomId,
    RoomParam(
    coverUrl: 'ルームカバー図のURL',
    roomName: 'ルーム名',
    ),
);
if (resp.code == 0) {
   // 席の占有成功
}

// 4.席の占有に成功した後、 TRTCChatSalonDelegate.onAudienceEnterのイベント通知を受信します
onVoiceListener(type, param) async {
    switch (type) {
        case TRTCChatSalonDelegate.onAudienceEnter:
            //視聴者のルーム入室
            break;
    }
}
```

[](id:model.step6)

### 手順6：視聴者側の視聴

1. 視聴者側は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 視聴者側は、業務バックエンドから最新のボイスサロンのルームリストを取得します。
 >?Demoのボイスサロンリストは、デモンストレーションでの使用のみです。ボイスサロンリストのビジネスロジックは様々です。Tencent Cloudでは現在、ボイスサロンリストの管理サービスを提供していませんので、ご自身でボイスサロンリストを管理してください。
3. 視聴者側は、`getRoomList`を呼び出してルームの詳細情報を取得します。この情報は、キャスター側が`createRoom`を呼び出してボイスサロンを作成するときに設定する簡単な説明情報です。
> !ボイスサロンリストに十分に包括的な情報がある場合は、`getRoomList`の呼び出しに関する手順をスキップできます。また、ルーム番号を入力すると、そのルームに入室できます。
4. 入室後、コンポーネントの `TRTCChatSalonDelegate.onAudienceEnter`と `TRTCChatSalonDelegate.onAudienceExit`という視聴者の入退室通知を受信します。イベントコールバックを監視した後、変更をUI上に更新できます。
5. 入室後、マイクリストのキャスターが参加した`TRTCChatSalonDelegate.onAnchorEnterMic`と `TRTCChatSalonDelegate.onAnchorLeaveMic`のイベントの通知も受信します。

![](https://tccweb-1258344699.cos.ap-nanjing.myqcloud.com/sdk/trtc/chatsalon/chatsalon.png)
```
// 1.視聴者は、ニックネームおよびプロフィール画像を設定します
trtcVoiceRoom.setSelfProfile("my_name", "my_face_url");

// 2.業務バックエンドから取得したルームリストをroomListと仮定します
List<Integer> roomList = GetRoomList();

// 3.getRoomInfoListを呼び出すことによって、ルームの詳細情報を取得します
RoomInfoCallback resp = await trtcVoiceRoom.getRoomInfoList(roomList);
if (resp.code == 0) {
    //この時、自分のUIルームリストを更新することができます
} 

// 4.roomidを渡してルームに参加します
ActionCallback enterRoomResp =
          await trtcVoiceRoom.enterRoom(_currentRoomId);
if (enterRoomResp.code == 0) {
    //入室に成功
}
// 5.入室に成功すると、処理イベント通知を受信します
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onAudienceEnter:
            //視聴者のルーム入室
        break;
      case TRTCChatSalonDelegate.onAudienceExit:
            //視聴者のルーム退出
        break;
      case TRTCChatSalonDelegate.onAnchorLeaveMic:
          //キャスターのルーム退出
        break;
      case TRTCChatSalonDelegate.onAnchorEnterMic:
          //キャスターのルーム入室
        break;
    }
}
```

[](id:model.step7)
### 手順7：マイクのオン・オフ
#### キャスター側
1.  `leaveMic`は自主的にマイク・オフにし、ルーム内の全メンバーは`onAnchorLeaveMic`のイベント通知を受信します。
2.  `kickMic`は、対応するユーザーのuserIdを渡し、キックアウトしてマイク・オフできます。グループマスターは、キックアウトしてマイク・オフにし、ルーム内の全メンバーは`onAnchorLeaveMicのイベント通知を受信します。

![](https://tccweb-1258344699.cos.ap-nanjing.myqcloud.com/sdk/trtc/chatsalon/chatsalon-ma-m.png)
```
// 1.キャスターによる自主的なマイク・オフ
trtcVoiceRoom.leaveMic();

//2.キックアウトしてマイク・オフ
trtcVoiceRoom.kickMic(userId);
```
#### 視聴者側：
1.  `enterMic`はマイク・オンにし、ルーム内の全メンバーは`onAnchorEnterMic`のイベント通知を受信します。
2.  `leaveMic`は自主的にマイク・オフにし、ルーム内の全メンバーは`onAnchorLeaveMic`のイベント通知を受信します。

![](https://tccweb-1258344699.cos.ap-nanjing.myqcloud.com/sdk/trtc/chatsalon/chatsalon-ma-au.png)
```
// 1.視聴者が自主的にマイク・オンします
trtcVoiceRoom.enterMic();

// 2.自主的なマイク・オフ
trtcVoiceRoom.leaveMic();
```


[](id:model.step8)

### 手順8：挙手によるマイク・オンシグナリングの使用リクエスト

Appが次の操作の業務フローを実施するために、相手の同意を必要とする場合、招待シグナリングによって対応するサポートを提供することができます。

#### 視聴者からの自主的なマイク申請：

1. 視聴者側は、`raiseHand`を呼び出して挙手を申請します。
2. キャスター側は、`onRaiseHand`のイベントを受信します。このとき、UIはウィンドウをポップアップし、キャスターに同意するかどうか尋ねることができます。
3. キャスターが同意を選択した場合、`agreeToSpeak`を呼び出し、userIdを渡します。
4. 視聴者側は、`onAgreeToSpeak`のイベントを受信し、`enterMic`を呼び出して、マイク・オンします。

![](https://tccweb-1258344699.cos.ap-nanjing.myqcloud.com/sdk/trtc/chatsalon/chatsalon-si.png)
```
// 視聴者側の視点
// 1. sendInvitationを呼び出し、マイク・オンをリクエストします
trtcVoiceRoom.raiseHand();

// 2.招待の同意リクエストを受信して、正式にマイク・オンにします
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onRaiseHand:
           trtcVoiceRoom.enterMic();
        break;
    }
}

// キャスター側の視点
// 1.キャスターがリクエストを受信します
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onAgreeToSpeak:
           trtcVoiceRoom.agreeToSpeak();
        break;
    }
}
```

[](id:model.step9)

### 手順9：文字チャットおよび弾幕コメントの実装
`sendRoomTextMsg`によって通常のテキストメッセージを送信できるようになり、このルーム内の全てのキャスターおよび視聴者が`onRecvRoomTextMsg`のコールバックを受信することができます。
IMバックエンドは、デフォルトのセンシティブワードフィルタルールを備えており、センシティブワードと認識されたテキストメッセージはクラウドに転送されることはありません。
```
// 送信側：テキストメッセージの送信
trtcVoiceRoom.sendRoomTextMsg("Hello Word!");
// 受信側：テキストメッセージの監視
onVoiceListener(type, param) async {
  switch (type) {
    case TRTCChatSalonDelegate.onRecvRoomTextMsg:
          //グループテキストメッセージを受信すると、テキストチャットルームを使用できます
      break;
  }
}
```