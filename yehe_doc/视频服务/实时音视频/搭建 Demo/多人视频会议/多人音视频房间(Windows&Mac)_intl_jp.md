ここで紹介するPC版TUIRoomコンポーネントは、柔軟なレイアウトで、適用性の高いオーディオビデオコミュニケーションツールです。コラボレーションオフィス、リモート採用、リモート問診、保険金査定、オンラインカスタマーサービス、ビデオ面接、デジタル行政、金融のデジタル化、オンラインミーティング、eラーニングなどのシーンで使用することができます。 各業界のシナリオと深く結びつき、企業のコスト削減と効率アップを助け、デジタルトランスフォーメーションを加速し、競争力を向上させます。
Appを[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)してインストールすると、体験することができます。

## ソリューションの優位性
- 超低遅延のオーディオビデオ通話、チャットルーム、画面共有、美顔、デバイス検出、データ統計などの機能を統合し、多人数オーディオビデオルームの一般的な機能をカバーします。
- 二次開発の需要に応じて、カスタムUIやレイアウトを迅速に実装し、ビジネスの迅速な立ち上げに役立ちます。
- TRTCとIMの基本SDKをカプセル化し、基本的なロジックコントロールを実装し、呼び出しを容易にするインターフェースを提供します。

## アクセスガイド
多人数オーディオビデオルームの機能に素早くアクセスしたい場合は、当社が提供するAppを直接修正して適応させるか、App内のModuleを使用してカスタマイズしたUIを実装することができます。

[](id:step1_1)
### 手順1：Appソースコードのダウンロード
[RoomApp](https://github.com/tencentyun/TUIMeeting)をクリックして移動し、ソースコードをCloneまたはダウンロードします。

[](id:step1_2)
### 手順2：Appファイルの設定
<dx-tabs>
::: Windows端末の設定
1. `Windows\RoomApp\utils\usersig\win\GenerateTestUserSig.h` ファイルを見つけて開きます。
2. `GenerateTestUserSig.h`内のパラメータを設定します。
	- **SDKAPPID**：デフォルトは0。実際のSDKAPPIDを設定してください。
	- **SECRETKEY**：デフォルトはブランク、実際のSECRETKEYを設定してください。
![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
:::
::: Mac端末の設定
1. `Windows\RoomApp\utils\usersig\mac\UserSigConfig.h`ファイルを見つけて開きます。
2. `UserSigConfig.h`内のパラメータを設定します。
	- **SDKAPPID_**：デフォルトは0。実際のSDKAPPIDを設定してください。
	- **SecretKey_**：デフォルトはブランク。実際のSECRETKEYを設定してください。
:::
</dx-tabs>

>!
>- ここで言及するUserSigの発行方法は、クライアントコードの中でのSECRETKEY設定となりますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのAppクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:step1_3)
### ステップ3：Appの設定および実行
<dx-tabs>
::: Windows端末の設定
1. コンパイル環境にはVirtual Studio（2015バージョン以上）を使用します。
2. AppのUIには、現在主流のQTフレームワーク5.9バージョンを使用します。QTをダウンロードしてインストールし、VSでQTツールを設定してください。またはバージョンに応じて、AppプロジェクトでQT設定を変更して設定を完了してください。
3. RoomAppのRoomApp.vcxproj ソースコードプロジェクトを開き、プログラムをコンパイルし、実行します。

:::
::: Mac端末の設定
1. コンパイル環境にはQtCreatorを使用します。 QTのインストール時に、QtCreatorの同時インストールを選択すればよく、バージョンはQTの公式インストールパッケージに従います。
2. AppのUIには現在主流のQTフレームワークを使用します。バージョンは5.9です。QT5.9をダウンロードしてインストールし、システム環境変数QTDIRがQTのインストールディレクトリを指向するように設定してください。
3. RoomAppのRoomApp.proソースコードプロジェクトを開き、プログラムをコンパイルし、実行します。
:::
</dx-tabs>

[](id:step1_4)
### 手順4：Appソースコードの修正
-  Module層は、TRTCとIMをカプセル化して、基本的なロジックコントロールを実装し、UI層の呼び出しを容易にする機能インターフェースを提供します。
- AppモジュールはUIモジュールであり、インターフェースの機能実装が含まれています。必要に応じて二次開発を行ったり、UI全体を置き換えたりすることができます。

## 体験アプリケーション
>! 体験アプリケーションには、少なくとも2台のデバイスが必要です。
### ログインインターフェース
図のように、ルーム番号とユーザー名（ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください）を入力してログインします。
![](https://qcloudimg.tencent-cloud.cn/raw/22cbaa8ac1d47cfc39076fa6149649c2.png)

### デバイス検出ページ
ここでは、デバイスの検出や、入室に使用するデバイスの設定、美顔効果の設定などを必要に応じて行うことができます。
![](https://qcloudimg.tencent-cloud.cn/raw/e5aed81f7ad0c07193c5506ebe0466d1.png)

### メインインターフェース
最初に入室するのはキャスターです。メインインターフェースには配信側リスト、下部のツールバー、上部のツールバーなどが含まれます。
![](https://qcloudimg.tencent-cloud.cn/raw/33d901c254c6c37c8afa4bce759b0bb3.png)

### 配信側リスト
配信側リストには現在のルームのメンバーを表示できます。相手がカメラとマイクを起動すると、相手の画面を見ること、相手の声を聞くことができます。

### 下部のツールバー
自身のマイク/カメラの制御、画面共有の開始、メンバーリスト、チャットルームなどの機能を実装しました。

### 上部のコントロールバー
ネットワーク情報、設定ページ、配信側リストレイアウト機能を実装しました。

### 設定ウィンドウ
設定ウィンドウでは、デバイスを選択し、美顔などのパラメータを設定することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/9eb20c81799dddc5be3f3fa7ef88dbac.png)

### チャットルーム
- チャットルームはグループメンバーのチャットを行うことができます。
- キャスターは全員に対してミュート/ミュート解除を行うことができます。
![](https://qcloudimg.tencent-cloud.cn/raw/9d927c98a595667d9f3f16d597abc77e.png)

### 退室
キャスターが退室する場合、2つの選択肢があります。
- **ルームの解散**：全員が退室することを指します。全員が退室する必要があります。
- **自身が退室**：キャスターの権限を渡して、他のユーザーがキャスターとなります。

![](https://qcloudimg.tencent-cloud.cn/raw/e2485085cdb43de94ef9d8bc6851a436.png)

## UIカスタマイズの実装
ソースコードのModuleには、TRTC SDKおよびIM SDK のカプセル化が含まれています。`TUIRoomCore.h`、`TUIRoomCoreCallback.h`、`TUIRoomDef.h` などのファイルでこのモジュールが提供するインターフェース関数およびその他定義を確認し、対応するインターフェースを使用してカスタマイズされたUIを実装できます。

[](id:step2_1)
### ステップ1：SDKの統合
公式サイトから [TRTC SDK](https://intl.cloud.tencent.com/document/product/647/34615)と[IM SDK](https://intl.cloud.tencent.com/document/product/1047/33996)をダウンロードし、外部のSDKディレクトリのIM SDKとLiteAVSDKディレクトリのファイルを置き換えます。
>! IM SDKはC++バージョンを使用します。

|SDK|ダウンロードページ|統合ガイド|
|--|--|--|
|TRTC SDK|[DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615)|[統合ドキュメント](https://intl.cloud.tencent.com/document/product/647/35095)|
|IM SDK|[DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996)[統合ドキュメント](https://intl.cloud.tencent.com/document/product/1047/34310)|

[](id:step2_2)
### ステップ2：プロジェクト設定SDKディレクトリおよびライブラリファイル
- **Windows端末**：VSでヘッダーファイルディレクトリ、静的ライブラリディレクトリ、および依存する静的ライブラリファイルを設定します。
- **Mac端末**：proおよびpriファイルで依存ライブラリとファイルディレクトリを追加します。

[](id:step2_3)
### ステップ3：作成およびログイン
1. `IUIRoomCore::Instance`インターフェースを使用してIUIRoomCoreシングルトンを作成し使用します。
2. AddCallbackインターフェースを呼び出し、コールバッククラスを設定し、SDKのコールバック通知を受信します。
3. Loginインターフェースを呼び出し、ログインを行います。
<table>
<thead><tr><th>パラメータ名</th><th>説明</th></tr></thead>
<tbody><tr>
<td>sdk_appid</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> で SDKAppIDを表示できます。</td>
</tr>
<tr>
<td>user_id</td>
<td>現在のユーザーID。文字列タイプでは、英語のアルファベット（a-z、A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。業務の実際のアカウントシステムと組み合わせてご自身で設定することをお勧めします。</td>
</tr>
<tr>
<td>user_sig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、<a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSigの計算、使用方法</a>をご参照ください。</td>
</tr>
</tbody></table>

[](id:step2_4)
### ステップ4：ニックネームの設定
正常にログインした後、SetSelfProfileを呼び出し、ユーザー情報を設定します。

[](id:step2_5)
### ステップ5：ルームの作成
1. メンバーがCreateRoomインターフェースを呼び出し、新たなルームを作成します。ルームの作成後、キャスターとしてチャットルームとTRTC ルームを含むルームに入室します。
2. メンバーがStartCameraPreviewインターフェースを呼び出し 、ローカルビデオのキャプチャと表示を開始します。

![](https://qcloudimg.tencent-cloud.cn/raw/485afdb0dc5218a03410de86b215004d.png)

[](id:step2_6)
### ステップ6：ルームの解散
1. キャスターがDestoryRoomインターフェースを呼び出し 、ルームを解散します。IMグループチャットを解散して、TRTCルームを退室します
2. メンバー側は、グループを解散し、TRTCルームを退室するよう通知するOnExitRoomコールバックメッセージを受信します

[](id:step2_7)
### ステップ7：ルームの譲渡
1. キャスターが、退室操作のためにTransferRoomMasterインターフェースを呼び出し、ルームを他の人に譲り渡します。
2. メンバー側は、ルームキャスターの変更を通知するOnRoomMasterChangedコールバックメッセージを受信します。
3. 変更後のキャスターは、キャスター権限を取得し、グループメンバーをコントロールできます

[](id:step2_8)
### ステップ8：ルームへの参加
1. ルーム参加手順は、作成手順と基本的に同じです。メンバーは、入室時にまずルームを作成する必要があり、作成に失敗した場合、メンバーとして入室します。
2. ルームの作成に失敗した場合、まずルーム情報を取得し、その後、再度入室します。
3. その他メンバーは、メンバーの入室があったことを通知するOnRemoteUserEnter コールバックを受信します。

![](https://qcloudimg.tencent-cloud.cn/raw/89d63df3ad5243e3b45386777fbb07e5.png)

[](id:step2_9)
### ステップ9：退室
1. メンバーがLeaveRoomインターフェースを呼び出し、IM ルームとTRTC ルームを退室します。
2. その他メンバーグループ側は、メンバーが退室したことを通知するOnRemoteUserLeaveコールバックを受信します。

[](id:step2_10)
### 手順10：画面共有
1. StartScreenCaptureインターフェース呼び出し 、画面共有を行います。
2. その他メンバーは、メンバーが画面共有中であることを通知するOnRemoteUserScreenVideoAvailableコールバックを受信します。

>? 画面共有モジュールは、ウィンドウ選択のロジックを実行する必要があります。具体的な実装については、Appの`ScreenShareWindow.h`の実装をご参照ください。

[](id:step2_11)
### 手順11：文字チャットとミュートメッセージの実現
1. SendChatMessageインターフェースを呼び出し、テキストを送信すると、ルーム内のメンバーはOnRecevieChatMessageコールバックメッセージを受信し、チャットメッセージを取得し表示できます。
2. キャスターはMuteChatRoomインターフェースを呼び出し、チャットをミュートし、または解除できます。メンバー側はOnChatRoomMutedコールバックを受信し、UI層が対応する処理を行います。
