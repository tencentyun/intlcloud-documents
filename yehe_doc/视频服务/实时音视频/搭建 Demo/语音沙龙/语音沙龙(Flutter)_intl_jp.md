## デモンストレーション
<table>
     <tr>
         <th>管理者によるマイク操作</th>  
         <th>リスナーによるマイク操作</th>  
     </tr>
<tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/849c3cff658d82b0fe0d3e7b1a490e13.png"/></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/25cc9b7695cc208c946b50710e842e41.png"/></td>
</tr>
</table>



ボイスサロン機能をすばやく実装する必要がある場合、当社が提供するDemoをもとにアダプタを直接修正するか、または当社が提供するTRTCChatSalonコンポーネントでカスタマイズしたUIを実装することができます。

[](id:DemoUI)

## DemoのUIの再利用

[](id:ui.step1)
### 手順1：アプリケーションの新規作成
1. TRTCコンソールにログインし、【開発支援】>【[快速跑通Demo](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. アプリケーション名（例：`TestChatSalon`）を入力し、【作成】をクリックします。

>!本機能はTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。



[](id:ui.step2)
### ステップ2：SDKおよびDemoソースコードをダウンロード
1. 実際のビジネスニーズに応じて、SDKと付属の[Demoソースコード](https://github.com/tencentyun/TRTCFlutterScenesDemo)をダウンロードします。
2. ダウンロード完了後、【ダウンロード済み。次へ】をクリックします。
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:ui.step3)
### ステップ3：Demo プログラムファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2.  `/example/lib/debug/GenerateTestUserSig.dart` ファイルを見つけて開きます。
3.  `GenerateTestUserSig.dart` ファイル内の関連パラメータを設定します。
<ul><li/>SDKAPPID：デフォルトはPLACEHOLDER、実際のSDKAppIDを設定してください。
	<li/>SECRETKEY：デフォルトはPLACEHOLDER、実際のキー情報を設定してください。</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png"/>

4. 貼り付け完了後、【貼り付けました。次へ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソールの概要ページに戻る】をクリックすればOKです。

>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)
###  手順4：コンパイル実行

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
[ソースコード](https://github.com/tencentyun/TRTCFlutterScenesDemo) のtrtcchatsalondemoフォルダには2つのサブフォルダuiとmodelが含まれ、uiフォルダにはインターフェースコードが含まれています。下表に各ファイルまたはフォルダおよび対応するUIをリストアップし、二次調整に役立つようにしています。

| ファイルまたはフォルダ                      | 機能の説明                             |
| ------------ | ------------------------------------ |
| base         | UIに使用される基礎となるクラス。                    |
| list         | リストページおよびルームページの作成。                 |
| room         | メインルームページは、管理者とリスナーという2種類のインターフェースがあります。 |
| widget       | 汎用ウィジェット。                           |

[](id:model)
## UIカスタマイズの実装
[ソースコード](https://github.com/tencentyun/TRTCFlutterScenesDemo) のtrtcchatsalondemoフォルダには2つのサブフォルダuiとmodelが含まれ、modelフォルダには再利用できるオープンソースコンポーネントTRTCChatSalonが含まれています。`TRTCChatSalon.dart`ファイルでこのコンポーネントが提供するインターフェース関数を確認し、対応するインターフェースを使用してカスタマイズしたUIを実装することができます。
![](https://main.qcloudimg.com/raw/7613bd7ec5b4e665f32ee5df69e5de85.png)

[](id:model.step1)
### 手順1：SDKの統合 
ボイスサロンコンポーネントtrtcchatsalondemoは、[TRTC SDK](https://pub.dev/packages/tencent_trtc_cloud)と[IM SDK](https://pub.dev/packages/tencent_im_sdk_plugin)に依存しています。`pubspec.yaml`を設定することで、更新を自動的にダウンロードできます。

プロジェクトの`pubspec.yaml` に次の依存関係を記述します。
```
dependencies:
  tencent_trtc_cloud: 最新バージョン番号
  tencent_im_sdk_plugin: 最新バージョン番号
```

[](id:model.step2)

### 手順2：権限の設定および難読化ルール
<dx-tabs>
::: iOS\s端末
`Info.plist`にマイクの権限申請を追加する必要があります。
```
<key>NSMicrophoneUsageDescription</key>
<string>通常の音声通話が行えるようにマイクの権限を承認します</string>
```
:::
:::  Android\s端末
1. `/android/app/src/main/AndroidManifest.xml`ファイルを開きます。
2. `xmlns:tools="http://schemas.android.com/tools"` をmanifestの中に追加します。
3. `tools:replace="android:label"をapplicationの中に追加します。
>? この手順を実行しないと、[Android Manifest merge failedコンパイルの失敗](https://intl.cloud.tencent.com/document/product/647/39242)という問題が発生します。

![アイコン](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)
:::
</dx-tabs>


[](id:model.step3)
### 手順3：TRTCChatSalonコンポーネントのインポート
次のディレクトリ内のすべてのファイルをプロジェクトにコピーします。
```
lib/TRTCChatSalonDemo/model/
```

[](id:model.step4)
### 手順4：コンポーネントの作成およびログイン
1. `sharedInstance`インターフェースを呼び出すと、TRTCChatSalonコンポーネントのインスタンスオブジェクトを作成できます。
2. `registerListener`関数を呼び出して、コンポーネントのイベント通知を登録します。
3. `login`関数を呼び出してコンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
<table>
<tr>
<th>パラメータ名</th>
<th>機能</th>
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
</table>

<dx-codeblock>
::: dart dart
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
:::
</dx-codeblock>

[](id:model.step5)

### 手順5：管理者側での配信開始

1. 管理者は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 管理者は、`createRoom`を呼び出して新しいボイスサロンを作成します。このとき、ルームID、ルーム名などルームの属性情報を渡します。
3. 管理者は、メンバーが参加した`TRTCChatSalonDelegate.onAudienceEnter`のイベント通知を受信します。このとき、マイク集音は自動的に開始されます。

![](https://main.qcloudimg.com/raw/dfe6ed5d0c973e399e834eb233c96ec6.png)

<dx-codeblock>
::: java java
// 1.管理者は、ニックネームおよびプロフィール画像を設定します
trtcVoiceRoom.setSelfProfile("my_name", "my_face_url", null);

// 2.管理者は、createRoomを呼び出してルームを作成します
ActionCallback resp = await trtcVoiceRoom.createRoom(
    roomId,
    RoomParam(
    coverUrl: 'ルームカバー図のURL',
    roomName: 'ルーム名',
    ),
);
if (resp.code == 0) {
   //3.席の占有成功
}

// 4.席の占有に成功した後、 TRTCChatSalonDelegate.onAudienceEnterのイベント通知を受信します
onVoiceListener(type, param) async {
    switch (type) {
        case TRTCChatSalonDelegate.onAudienceEnter:
            //リスナーの入室
            break;
    }
}
:::
</dx-codeblock>

[](id:model.step6)

### 手順6：リスナー側の視聴

1. リスナー側は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. リスナー側は、業務バックエンドから最新のボイスサロンのルームリストを取得します。
 >?Demoのボイスサロンリストは、デモンストレーション用のためだけのものです。ボイスサロンリストのビジネスロジックは様々です。Tencent Cloudでは現在ボイスサロンリストの管理サービスを提供していません。ご自身でボイスサロンリストを管理してください。
3. リスナー側は、`getRoomList`を呼び出してルームの詳細情報を取得します。この情報は、管理者側が`createRoom`を呼び出してボイスサロンを作成するときに設定する簡単な説明情報です。
> !ボイスサロンリストに十分に包括的な情報がある場合は、`getRoomList`の呼び出しに関する手順をスキップできます。また、ルーム番号を入力すると、そのルームに入室できます。
4. 入室後、コンポーネントの `TRTCChatSalonDelegate.onAudienceEnter`と `TRTCChatSalonDelegate.onAudienceExit`という視聴者の入退室通知を受信します。イベントコールバックを監視した後、変更をUI上に更新できます。
5. 入室後、マイクリストのキャスターが参加した`TRTCChatSalonDelegate.onAnchorEnterMic`と `TRTCChatSalonDelegate.onAnchorLeaveMic`のイベントの通知も受信します。

![](https://main.qcloudimg.com/raw/6fbabfa4e217022cf3d05677e4a45538.png)
<dx-codeblock>
::: dart dart
// 1.リスナーは、ニックネームおよびプロフィール画像を設定します
trtcVoiceRoom.setSelfProfile("my_name", "my_face_url");

// 2.業務バックエンドから取得したルームリストをroomListと仮定します
List<Integer> roomList = GetRoomList();

// 3. getRoomInfoListを呼び出すことによって、ルームの詳細情報を取得します
RoomInfoCallback resp = await trtcVoiceRoom.getRoomInfoList(roomList);
if (resp.code == 0) {
    //この時、自分のUIルームリストを更新することができます
} 

// 4.roomIdを渡してルームに参加します
ActionCallback enterRoomResp =
          await trtcVoiceRoom.enterRoom(_currentRoomId);
if (enterRoomResp.code == 0) {
    //入室に成功 
}
// 5.入室に成功すると、処理イベント通知を受信します
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onAudienceEnter:
            //リスナーの入室
        break;
      case TRTCChatSalonDelegate.onAudienceExit:
            //リスナーの退室
        break;
      case TRTCChatSalonDelegate.onAnchorLeaveMic:
          //管理者の退室
        break;
      case TRTCChatSalonDelegate.onAnchorEnterMic:
          //管理者の入室
        break;
    }
}
:::
</dx-codeblock>

[](id:model.step7)
### 手順7：マイクのオン・オフ
<dx-tabs>
::: 管理者側
1.  `leaveMic`は自主的にマイク・オフにし、ルーム内の全メンバーは`onAnchorLeaveMic`のイベント通知を受信します。
2.  `kickMic`は、対応するユーザーのuserIdを渡し、キックアウトしてマイク・オフできます。管理者は、キックアウトしてマイク・オフにし、ルーム内の全メンバーは`onAnchorLeaveMic`のイベント通知を受信します。

![](https://qcloudimg.tencent-cloud.cn/raw/0eb3dbe14b166a24252f0efb45a6b24f.png)
<dx-codeblock>
::: dart dart
// 1.自主的なマイク・オフ
trtcVoiceRoom.leaveMic();

//2.キックアウトしてマイク・オフ
trtcVoiceRoom.kickMic(userId);
:::
</dx-codeblock>
:::
::: リスナー側
1.  `enterMic`はマイク・オンにし、ルーム内の全メンバーは`onAnchorEnterMic`のイベント通知を受信します。
2.  `leaveMic`は自主的にマイク・オフにし、ルーム内の全メンバーは`onAnchorLeaveMic`のイベント通知を受信します。

![](https://main.qcloudimg.com/raw/c9611b5017536604f63333ce7c19c309.png)
<dx-codeblock>
::: dart dart
// 1.リスナーがユーザーを発言者にします
trtcVoiceRoom.enterMic();

// 2.自主的なマイク・オフ
trtcVoiceRoom.leaveMic();

:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step8)

### 手順8：挙手によるマイク・オンシグナリングの使用リクエスト

Appにおいて相手の同意がなければ、次の操作の業務フローを実施できない場合は、招待シグナリングによって相応のサポートを行うことができます。

#### リスナーからのからの自主的なマイク・オン申請

1. リスナー側が`raiseHand`を呼び出し、挙手を申請します。
2. 管理者側は、`onRaiseHand`のイベントを受信します。このとき、UIはウィンドウをポップアップし、管理者に同意するかどうか尋ねることができます。
3. 管理者が同意を選択した場合、`agreeToSpeak`を呼び出し、userIdを渡します。
4. リスナー側は、`onAgreeToSpeak`のイベント通知を受信し、`enterMic`を呼び出して、マイク・オンします。

![](https://main.qcloudimg.com/raw/3543bf768896cfd78b0163dc9378e659.png)
<dx-codeblock>
::: dart dart
// リスナー側の視点
// 1.sendInvitationを呼び出し、マイク・オンをリクエストします
trtcVoiceRoom.raiseHand();

// 2.招待のリクエスト同意を受信し、正式にマイク・オンになります
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onRaiseHand:
           trtcVoiceRoom.enterMic();
        break;
    }
}

// 管理者側の視点
// 1.管理者がリクエストを受信します
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onAgreeToSpeak:
           trtcVoiceRoom.agreeToSpeak();
        break;
    }
}
:::
</dx-codeblock>

[](id:model.step9)

### 手順9：文字チャットおよび弾幕コメントの実装
`sendRoomTextMsg`によって通常のテキストメッセージを送信できるようになり、このルーム内のすべてのキャスターおよびリスナーが`onRecvRoomTextMsg`のコールバックを受信することができます。
  IMバックエンドは、デフォルトでNGワードフィルター規則を有し、NGワードと認識されたテキストメッセージはクラウドに転送されることはありません。
  <dx-codeblock>
  ::: dart dart
  // 発信側：テキストメッセージの発信
  trtcVoiceRoom.sendRoomTextMsg("Hello Word!");

// 受信側：テキストメッセージのモニタリング
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onRecvRoomTextMsg:
            //グループテキストメッセージを受信すると、テキストチャットルームを使用できます
        break;
    }
}
:::
</dx-codeblock>
