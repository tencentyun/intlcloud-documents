ビデオ・インタラクティブストリーミングの機能をすばやく実装する必要がある場合、当社が提供するDemoをもとに直接修正を加えてフィットさせることも、当社が提供するTRTCLiveRoomコンポーネントを使用し、カスタマイズしたUIを実現することも可能です。

[](id:DemoUI)

## DemoのUIの再利用

[](id:ui.step1)

### 手順1：アプリケーションの新規作成

1. TRTCコンソールにログインし、【開発支援】>【[快速跑通Demo](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. `TestLive`などのアプリケーション名を入力して、【作成】をクリックします。

>! 本機能はTencent Cloud[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。



[](id:ui.step2)
### ステップ2：SDKおよびDemoソースコードをダウンロード

1. 実際のビジネスニーズに基づき、SDKおよび付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、【ダウンロード済み。次へ】をクリックします。
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:ui.step3)
### ステップ3：Demo プログラムファイルの設定

1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2.  `/example/lib/debug/GenerateTestUserSig.dart` ファイルを見つけて開きます。
3.  `GenerateTestUserSig.dart` ファイル内の関連パラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトはPLACEHOLDER。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトはPLACEHOLDER。実際のキー情報を設定してください。</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 貼り付け完了後、【貼り付けました。次へ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソールの概要ページに戻る】をクリックすればOKです。

>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)

###  手順4：コンパイル実行
>! Android端末は実際のマシンで実行する必要があり、エミュレーターのデバッグはサポートされていません。

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

ソースコードのTRTCLiveRoomフォルダは、uiとmodelの2つのサブフォルダを含んでいます。uiフォルダにはインターフェースコードが含まれています。以下の表にはファイルまたはフォルダおよび対応するUIをリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ                      | 機能の説明                             |
| ------------ | ------------------------------------ |
| base         | UIに使用される基礎となるクラス。                    |
| list         | リストページおよびルームページの作成。                 |
| room         | メインルームページは、キャスターと視聴者という2種類のインターフェースがあります。 |

[](id:model)

## UIカスタマイズの実装

[ソースコード](https://github.com/tencentyun/TRTCFlutterScenesDemo)フォルダ`TRTCLiveRoom`にはuiとmodelの2つのサブフォルダが含まれ、そのうちmodelフォルダには再利用可能なオープンソースコンポーネントTRTCLiveRoomが含まれています。このコンポーネントが提供するインターフェース関数は`TRTCLiveRoom.dart`ファイルで確認でき、対応するインターフェースを使用してカスタマイズUIを実装することができます。

[](id:model.step1)

### 手順1：SDKの統合 

インタラクティブライブストリーミングコンポーネントTRTCLiveRoomは、[TRTC SDK](https://pub.dev/packages/tencent_trtc_cloud)と[IM SDK](https://pub.dev/packages/tencent_im_sdk_plugin)に依存しています。`pubspec.yaml`を設定することで、自動的にダウンロードして更新できます。

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
`Info.plist`にカメラとマイクの権限申請を追加する必要があります。
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

### 手順3：TRTCLiveRoomコンポーネントをインポート

次のディレクトリ内のすべてのファイルをプロジェクトにコピーします。

```
lib/TRTCLiveRoom/model/
```

[](id:model.step4)

### 手順4：コンポーネントの作成およびログイン

1. `sharedInstance`インターフェースを呼び出すと、TRTCLiveRoomコンポーネントのインスタンスオブジェクトを作成できます。
2. `registerListener`関数を呼び出して、コンポーネントのイベント通知を登録します。
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
<td>useCDNFirst</td>
<td>視聴者の視聴方式の設定に使用します。trueは一般視聴者のCDN経由での視聴を表し、料金は安価ですがレイテンシーは高めです。falseは一般視聴者の低レイテンシーによる視聴を表し、料金はCDN とマイク接続の間ですが、遅延を1s以内に抑えることができます。</td>
</tr>
<tr>
<td>CDNPlayDomain</td>
<td>useCDNFirstの設定をtrueにした時に有効になり、CDN経由の視聴の再生ドメイン名の指定に利用します。CSSコンソール >【<a href="https://console.cloud.tencent.com/live/domainmanage">ドメイン名管理</a>】ページからログインし、設定することができます。</td>
</tr>
</table>

[](id:model.step5)
### 手順5：キャスター側での配信開始

1. キャスターは、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. キャスターは、配信開始前に先に`startCameraPreview`を呼び出してカメラのプレビューを起動させ、インターフェース上に美顔調節ボタンを設置して呼び出し、`getBeautyManager`で美顔設定を行うことができます。
>?エンタープライズ版以外のSDKは美顔やスタンプの機能をサポートしていません。
3. 美顔効果の変更後、キャスターは `createRoom` を呼び出して新しいライブストリーミングルームを作成することができます。
4. キャスターが`startPublish`を呼び出し、プッシュを開始します。CDN視聴のサポートが必要な場合は、login時に渡される`TRTCLiveRoomConfig`パラメータ内で`useCDNFirst`と`CDNPlayDomain`を指定し、`startPublish`時にライブストリーミング・プルストリーム用のstreamIDを指定してください。

![](https://main.qcloudimg.com/raw/eab281d702879ae87728d0064a090dca.jpg)

[](id:model.step6)
### 手順6：視聴者側での視聴

1. 視聴者側は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 視聴者側が業務バックエンドから最新のライブストリーミングルームリストを取得します。
>?Demo内のライブストリーミングルームリストはデモに使用するためだけのものです。ライブストリーミングルームリストの業務ロジックは千差万別です。現在、Tencent Cloudはライブストリーミングルームリスト管理のサービスを提供していません。各自でご自分のライブストリーミングルームリストを管理してください。
3. 視聴者側は、`getRoomInfos`を呼び出してルームの詳細情報を取得します。この情報は、キャスター側が`createRoom`を呼び出してライブストリーミングルームを作成するときに設定する簡単な説明情報です。
 >!ライブストリーミングルームのリストに十分に包括的な情報がある場合は、`getRoomInfos`の呼び出しに関する手順をスキップできます。
4. 視聴者は1つのライブストリーミングルームを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
5. `startPlay`を呼び出してキャスターのuserIdを渡し、再生を開始します。
 - ライブストリーミングルームリストにキャスターのuserID情報がすでに含まれている場合、視聴者は直接`startPlay`を呼び出してキャスターのuserIdを渡せば、再生を開始できます。
 - ルーム参加前にキャスターのuserIDが一時的に取得できない場合、視聴者側はルーム参加後にキャスターの`onAnchorEnter`のイベントコールバックを受信します。このコールバックの中にキャスターのuserID情報が含まれていますので、`startPlay`を呼び出せば再生できます。 

![](https://main.qcloudimg.com/raw/2ff8b30de38a3084c12af0513068dc6e.jpg)

[](id:model.step7)
### 手順7：視聴者とキャスターとのマイク接続のオンとオフ

1. 視聴者側が`requestJoinAnchor`を呼び出し、キャスター側にマイク接続のリクエストを送信します。
2. キャスター側は `TRTCLiveRoomDelegate#onRequestJoinAnchor`（視聴者からのマイク接続のリクエストがあります）のイベント通知を受信します。
3. キャスター側は`responseJoinAnchor`を呼び出し、視聴者からのマイク接続リクエストを受け入れるかどうか決定できます。
4. 視聴者側は`onAnchorAccepted`イベント通知を受信します。この通知にはキャスター側の処理結果が含まれています。
5. キャスターがマイク接続リクエストに同意したら、視聴者側は`startCameraPreview`を呼び出し、ローカルカメラを起動させます。その後`startPublish`を呼び出し、視聴者側のプッシュを開始します。
6. キャスター側は、視聴者側の起動の通知の後に、`TRTCLiveRoomDelegate#onAnchorEnter`（別のオーディオ・ビデオストリーミングが届いています）の通知を受信します。この通知には視聴者側のuserIdが含まれています。
7. キャスター側が `startPlay` を呼び出すと、マイク接続の視聴者の画面を見ることができます。

![](https://main.qcloudimg.com/raw/05a8c6af8bdc8b441f90b297e83106fc.jpg)


[](id:model.step8)

### 手順8：キャスターとキャスターPK

1. キャスターAが`requestRoomPK`を呼び出し、キャスターBにPKのリクエストを送信します。
2. キャスターBが`TRTCLiveRoomDelegate onRequestRoomPK`のコールバック通知を受信します。
3. キャスターBが `responseRoomPK` を呼び出し、キャスターA のPKのリクエストを受け入れるか決定します。
4. キャスターBは、キャスターAのリクエストを受け入れたら、`TRTCLiveRoomDelegate onAnchorEnter`の通知を待ってから、`startPlay`を呼び出し、キャスターAを表示します。
5. PKのリクエストが同意されたかについて、キャスターAが `onRoomPKAccepted`のコールバック通知を受信します。
6. キャスターAのリクエストが同意されたら、`TRTCLiveRoomDelegate onAnchorEnter`の通知を待ってから、`startPlay`を呼び出し、キャスターBを表示します 。

![](https://main.qcloudimg.com/raw/5632056b6d86541db841026e9488468b.jpg)

[](id:model.step9)
### 手順9：文字チャットおよび弾幕コメントの実装
- `sendRoomTextMsg`によって通常のテキストメッセージを送信できるようになり、該当するルーム内の全てのキャスターおよび視聴者が`onRecvRoomTextMsg`のコールバックを受信することができます。
  IMバックエンドは、デフォルトでNGワードフィルター規則を有し、NGワードと認識されたテキストメッセージはクラウドに転送されることはありません。
<dx-codeblock>
::: dart dart
// 発信側：テキストメッセージの発信
trtcLiveCloud.sendRoomTextMsg("Hello Word!");
  

// 受信側：テキストメッセージのモニタリング
onListenerFunc(type, params) async {
  switch (type) {
    case TRTCLiveRoomDelegate.onRecvRoomTextMsg:
          //グループテキストメッセージを受信すると、テキストチャットルームを使用できます
      break;
  }
}
:::
</dx-codeblock>
- `sendRoomCustomMsg`によって、カスタム（シグナル）メッセージを送信できます。当該ルーム内のすべてのキャスターと視聴者が`onRecvRoomCustomMsg` コールバックを受信できます。
  カスタムメッセージは、カスタマイズ信号の送信によく用いられます。例えば、「いいね」情報の発信やブロードキャストに使用します。
