当社のAppを[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)してインストールし、多人数ビデオミーティングの効果を体験いただけます。これには、画面共有、美顔、低遅延ミーティングなど、TRTCの多人数ビデオミーティングシナリオ関連の機能が含まれています。

[](id:DemoUI)
## AppのUIの再利用
[](id:ui.step1)
### 手順1：アプリケーションの新規作成

1. TRTCコンソールにログインし、【開発支援】>【[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. アプリケーション名（例：`TestMeetingRoom`）を入力し、【作成】をクリックします。
3. 【ダウンロードしました。次のステップ】をクリックすると、この手順をスキップします。

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>! 本機能はTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については 、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。

[](id:ui.step2)
### 手順2：Appソースコードのダウンロード

[TRTCFlutterScenesDemo](https://github.com/tencentyun/TRTCFlutterScenesDemo)クリックして当該ページに入り、ソースコードをCloneまたはダウンロードします。

[](id:ui.step3)
### 手順3：Appファイルの設定

1. 設定変更ページに進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `/lib/debug/GenerateTestUserSig.dart`ファイルを見つけて開きます。
3.`GenerateTestUserSig.dart`ファイル内の関連パラメータを設定します。
<ul style="margin:0">
    <li>SDKAPPID：デフォルトはPLACEHOLDER。実際のSDKAppIDを設定してください。</li>
    <li>SECRETKEY：デフォルトはPLACEHOLDER。実際のキー情報を設定してください。</li>
</ul>

4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。

>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**のこの手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)
### 手順4：コンパイル実行

>! Android端末は実際のマシンで実行する必要があり、エミュレーターのデバッグはサポートされていません。

1. `flutter pub get`を実行します。
2. コンパイルを実行し、デバッグを行います。
<dx-tabs>
::: iOS\s端末
1. XCode（11.0およびそれ以降のバージョン）を使用して、ソースコードディレクトリの `/iosプロジェクト` を開きます。
2. コンパイルを行い、Demoプロジェクトを実行します。
:::
::: Android\s端末
1. `flutter run`を実行します。
2. Android Studio（3.5およびそれ以降のバージョン）を使用して、ソースプロジェクトを開き、【実行】をクリックすれば完了です。
:::

</dx-tabs>

[](id:ui.step5)
### 手順5：Demoソースコードの修正

ソースコードのTRTCMeetingDemoフォルダには、uiとmodelの2つのサブフォルダが含まれ、uiフォルダの中はいずれもインターフェースコードです。以下の表にはファイルまたはフォルダおよび対応するUIをリストアップし、二次調整に役立つようにしています。

| ファイルまたはフォルダ | 機能の説明 |
|-------|--------|
| TRTCMeetingIndex.dart | ミーティング作成または参加インターフェース |
| TRTCMeetingRoom.dart | ビデオミーティングのメインインターフェース |
| TRTCMeetingMemberList.dart | 参加者リストインターフェース |
| TRTCMeetingSetting.dart | ビデオミーティング関連パラメータ設定インターフェース |

[](id:model)
## カスタムUIの実装

[ソースコード](https://github.com/tencentyun/TRTCFlutterScenesDemo)の中のTRTCMeetingDemoフォルダにはuiとmodelの2つのサブフォルダが含まれ、modelフォルダには再利用可能なオープンソースコンポーネントTRTCMeetingが含まれています。`TRTCMeeting.dart` ファイルの中からこのコンポーネントが提供するインターフェース関数を見つけ、対応するインターフェースを使用してカスマイズUIを実装することが可能です。
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

[](id:model.step1)
### 手順1：SDKへの統合

インタラクティブライブストリーミングコンポーネントTRTCMeetingは、[TRTC SDK](https://pub.dev/packages/tencent_trtc_cloud)と[IM SDK](https://pub.dev/packages/tencent_im_sdk_plugin)に依存しています。`pubspec.yaml`を設定することで、自動的にダウンロードして更新できます。

プロジェクトの`pubspec.yaml`に次の依存関係を記述します。
```
dependencies:
  tencent_trtc_cloud: 最新バージョン番号
  tencent_im_sdk_plugin: 最新バージョン番号
```

[](id:model.step2)
### 手順2：権限の設定および難読化ルール

<dx-tabs>
::: iOS\s端末
1. `Info.plist`にカメラとマイクの権限申請を追加する必要があります。
```
<key>NSMicrophoneUsageDescription</key>
<string>通常の音声通話が行えるようにマイクの権限を承認します</string>
```
:::
::: Android\s端末
1. `/android/app/src/main/AndroidManifest.xml`ファイルを開きます。
2. `xmlns:tools="http://schemas.android.com/tools"` をmanifestの中に追加します。
3. `tools:replace="android:label"をapplicationの中に追加します。
>? この手順を実行しないと、[Android Manifest merge failedコンパイルの失敗](https://intl.cloud.tencent.com/document/product/647/39242)という問題が発生します。

![図](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)
:::
</dx-tabs>

[](id:model.step3)
### 手順3：TRTCMeetingコンポーネントのインポート

次のディレクトリ内のすべてのファイルをプロジェクトにコピーします。
```
lib/TRTCMeetingDemo/model/
```

[](id:model.step4)
### 手順4：コンポーネントの作成およびログイン

1. `sharedInstance`インターフェースを呼び出すと、TRTCMeetingコンポーネントのインスタンスオブジェクトを作成できます。
2. `registerListener`関数を呼び出して、コンポーネントのイベント通知を登録します。
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
</table>

<dx-codeblock>
::: dart dart
TRTCMeeting trtcMeeting = TRTCMeeting.sharedInstance();
trtcMeeting.registerListener(onListener);
ActionCallback res = await trtcMeeting.login(
    GenerateTestUserSig.sdkAppId,
    userId,
    GenerateTestUserSig.genTestSig(userId),
);
if (res.code == 0) {
    // ログイン成功
}
:::
</dx-codeblock>

[](id:model.step5)
### 手順5：多人数ミーティングの新規作成

1. キャスターは、[手順4](#model.step4)でログインした後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. キャスターがcreateMeetingを呼び出し、新しいミーティングルームを作成します。
3. キャスターは、`startCameraPreview`を呼び出してビデオ画面をキャプチャすることができ、`startMicrophone`を呼び出して音声をキャプチャすることもできます。
4. キャスターに美顔のニーズがある場合は、インターフェース上に美顔調節ボタンを設定して呼び出すことができ、getBeautyManager を介して美顔設定を行います。
>? エンタープライズ版以外のSDKは美顔やスタンプの機能をサポートしていません。

![](https://main.qcloudimg.com/raw/7d55d4983e6fe8da04e63babe5ab3822.png)

<dx-codeblock>
::: dart dart
// 1. キャスターがニックネームとプロフィール画像を設定
trtcMeeting.setSelfProfile('my_name', 'my_avatar');

// 2. キャスターがミーティングを作成
ActionCallback res = await trtcMeeting.createMeeting(roomId);
if (res.code == 0) {
    // ミーティング作成に成功
    // 3. カメラと音声キャプチャを起動
    trtcMeeting.startCameraPreview(true, TRTCCloudVideoViewId);
    trtcMeeting.startMicrophone();
    // 4. 美顔設定
    trtcMeeting.getBeautyManager().setBeautyStyle(TRTCCloudDef.TRTC_BEAUTY_STYLE_PITU);
    trtcMeeting.getBeautyManager().setBeautyLevel(6);
}
:::
</dx-codeblock>

[](id:model.step6)
### 手順6：参加者の多人数ミーティングへの参加

1. 参加者は、[手順4](#model.step4)でログインした後、setSelfProfileを呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 参加者は、enterMeeting呼び出してミーティングルーム番号を渡すと、ミーティングルームに参加できます。
3. 参加者は、startCameraPreviewを呼び出してビデオ画面をキャプチャすることができ、またstartMicrophoneを呼び出して音声をキャプチャすることもできます。
4. 他の参加者がカメラを起動すると、onUserVideoAvailableのイベントを受け取ります。この時、startRemoteViewを呼び出してuserIdを渡すと再生を開始できます。

![](https://main.qcloudimg.com/raw/ce4bc9c134a94709c3f8e1768c65be88.png)

<dx-codeblock>
::: dart dart
// 1. 参加者がニックネームとプロフィール画像を設定
trtcMeeting.setSelfProfile('my_name', 'my_avatar');

// 2. 参加者がenterMeetingを呼び出してミーティングルームに参加
ActionCallback res = await trtcMeeting.enterMeeting(roomId);
if (res.code == 0) {
    // ミーティング参加に成功
    // 3. カメラと音声キャプチャを起動
    trtcMeeting.startCameraPreview(true, TRTCCloudVideoViewId);
    trtcMeeting.startMicrophone();
    // 4. 美顔設定
    trtcMeeting.getBeautyManager().setBeautyStyle(TRTCCloudDef.TRTC_BEAUTY_STYLE_PITU);
    trtcMeeting.getBeautyManager().setBeautyLevel(6);
}

// 5. 参加者が他のメンバーのカメラ起動の通知を受信し、再生が開始されます
trtcMeeting.registerListener(onListener);
onListener(TRTCMeetingDelegate type, param) {
    switch (type) {
        case TRTCMeetingDelegate.onUserVideoAvailable:
            if (param['available']) {
                trtcMeeting.startCameraPreview(
                    param['userId'],
                    TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG,
                    TRTCCloudVideoViewId
                );
            } else {
                trtcMeeting.stopRemoteView(
                    param['userId'],
                    TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG
                );
            }
            break;
    }
}
:::
</dx-codeblock>

[](id:model.step7)
### 手順7：画面共有

1. 画面共有機能は、システムにフローティングウィンドウの権限を申請する必要があり、自分でUIの中で特定のロジックを実装する必要があります。
2. startScreenCaptureを呼び出し、エンコードパラメータとスクリーンキャプチャのプロセスのフローティングウィンドウを渡すと、画面共有機能を実装できます。具体的な情報については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)をご参照ください。
3. ミーティング中の他メンバーがonUserVideoAvailableのイベント通知を受け取ります。

>! 画面共有とカメラキャプチャは相互排他的な操作です。画面共有機能をアクティブにしたい場合は、先にstopCameraPreviewを呼び出してカメラキャプチャを停止してください。詳細については、[TRTC SDK](https://intl.cloud.tencent.com/document/product/647/39859)をご参照ください。

<dx-codeblock>
::: dart dart
await trtcMeeting.stopCameraPreview();
trtcMeeting.startScreenCapture(
    videoFps: 10,
    videoBitrate: 1600,
    videoResolution: TRTCCloudDef.TRTC_VIDEO_RESOLUTION_1280_720,
    videoResolutionMode: TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT,
    appGroup: iosAppGroup,
);
:::
</dx-codeblock>

[](id:model.step8)
### 手順8：文字チャットとミュートメッセージの実現

- sendRoomTextMsgにより、ノーマルなテキストメッセージを送信でき、そのミーティングのすべての参加者がonRecvRoomTextMsgのコールバックを受信します。IMバックエンドにはデフォルトのセンシティブワードフィルタリングルールが備わっており、センシティブワードと判定されたテキストメッセージがクラウドで転送されることはありません。
<dx-codeblock>
::: dart dart
// 送信側：テキストメッセージの送信
trtcMeeting.sendRoomTextMsg('Hello Word!');
// 受信側：テキストメッセージの監視
trtcMeeting.registerListener(onListener);
onListener(TRTCMeetingDelegate type, param) {
    switch (type) {
        case TRTCMeetingDelegate.onRecvRoomTextMsg:
            print( param['userName'] + 'からのメッセージ：' + param['message']+'を受信' );
            break;
    }
}
:::
</dx-codeblock>

- sendRoomCustomMsgにより、カスタム（コマンド）メッセージを送信でき、そのミーティングのすべての参加者がonRecvRoomCustomMsgのコールバックを受信します。カスタムメッセージは、通常カスタマイズしたシグナリングの転送に使用されます（例：ミュートの会場内制御など）。
<dx-codeblock>
::: dart dart
// 送信側：カスタマイズしたcmdでミュートの通知を区別できます
// eg: "CMD_MUTE_AUDIO"はミュートの通知を表します
trtcMeeting.sendRoomCustomMsg('CMD_MUTE_AUDIO', '1');
// 受信側：カスタムメッセージの監視
trtcMeeting.registerListener(onListener);
onListener(TRTCMeetingDelegate type, param) {
    switch (type) {
        case TRTCMeetingDelegate.onRecvRoomCustomMsg:
            if (param['command'] == 'CMD_MUTE_AUDIO') {
                // ミュートの通知を受信します
                print(param['userName'] +'から' + 'のミュートの通知：' + param['message']'を受信');
                trtcMeeting.muteLocalAudio(message == '1');
            }
            break;
    }
}
:::
</dx-codeblock>
