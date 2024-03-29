## デモンストレーション
[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)からAppをインストールして、マイク管理、低レイテンシー音声インタラクション、文字チャットなどのボイスチャットのユースケースにおけるTRTCの関連機能を含む、ボイスチャットルームの機能を体験できます。


ボイスチャットルーム機能をすばやく実装する必要がある場合は、当社が提供するAppを基に直接変更を加えて適合させることも、当社が提供するTUIVoiceRoomコンポーネントでカスタマイズしたUIを実装することも可能です。

[](id:DemoUI)
## AppのUIの再利用

[](id:ui.step1)
### 手順1：アプリケーションの新規作成
1. TRTCコンソールにログインし、 **開発支援** > **[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)**を選択します。
2. `TestLiveRoom`などのアプリケーション名を入力して、 **作成 **をクリックします。
3. **ダウンロードしました。次のステップ**をクリックすると、この手順をスキップします。

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>?本機能はTencent Cloud [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) と [IM](https://intl.cloud.tencent.com/document/product/1047) という2つの基本的な PaaS サービスを同時に使用し、TRTCをアクティブにした後、IM サービスを同期的にアクティブにすることができます。 IM は付加価値サービスであり、課金ルールの詳細については [Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。



[](id:ui.step2)
### 手順2：Appソースコードのダウンロード
クリックして[TUIVoiceRoom](https://github.com/tencentyun/TUIVoiceRoom)に進み、ソースコードをCloneまたはダウンロードします。

[](id:ui.step3)
### 手順3：Appプロジェクトファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `TUIVoiceRoom/Debug/GenerateTestUserSig.swift`ファイルを見つけて開きます。
3.`GenerateTestUserSig.swift`ファイル内の関連パラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 貼り付け完了後、**貼り付けました。次のステップ**をクリックすれば、作成が完了します。
5. コンパイル完了後、 **コンソール概要に戻る** をクリックすれば終了です。

>!
>- ここで言及するUserSigの発行方法は、クライアントコードの中でのSECRETKEY設定となりますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのAppクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)
### 手順4：Appの実行
Xcode（11.0以上のバージョン）を使用してソースコードプロセス`TUIVoiceRoom/TUIVoiceRoomApp.xcworkspace`を開き、**実行**をクリックすれば、このAppのデバッグが開始されます。

[](id:ui.step5)
### 手順5：Appソースコードの修正
ソースコードの`Source` フォルダは、uiとmodelの2つのサブフォルダを含んでいます。uiフォルダには、インターフェースコードとインターフェース関連のロジックが含まれています。以下の表にはそれぞれのswiftファイルまたはフォルダおよびそれらが対応するUIをリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ | 機能の説明                             |
|:-------:|:--------|
|TRTCVoiceRoomEnteryControl.swift|このフォルダにはすべてのViewControllerの初期化取得方法が含まれています。このインスタンスを介してViewControllerオブジェクトをすばやく取得することができます。|
| TRTCCreateVoiceRoomViewController |ボイスチャットルームページのロジック作成。 |
| TRTCVoiceRoomViewController | メインルームページ。管理者と視聴者という2種類のインターフェースがあります。 |

各`TRTC'XXXX'ViewController`フォルダには、`ViewController`、`RootView`および`ViewModel`が含まれ、各ファイルの役割は下表に示すとおりです。

| ファイル | 機能説明 |
|:-------:|:--------|
| ViewController.swift | ページコントローラ。画面のルーティング作業、RootViewおよびViweModelのバインディング作業を担当します。|
| RootView.swift | ビュー。すべてのビューのレイアウト。 |
| ViewModel.swift | ビューコントローラ。ビューのインタラクションに応答し、ビューの応答ステータスを返す作業を担当します。 |

## 体験アプリケーション
>! 体験アプリケーションには、少なくとも2台のデバイスが必要です。

### ユーザーA

1. ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. **ルームの作成**をクリックします。
2. ルームトピックを入力し、**チャット開始**をクリックします。

### ユーザーB
1. ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. ユーザーAが作成したルーム番号を入力し、**入室する**をクリックします。


>! ルームナンバーはユーザーAのルーム上部に表示されます。

[](id:model)
## UIカスタマイズの実装
[ソースコード](https://github.com/tencentyun/TUIVoiceRoom)の`Source`フォルダには、uiとmodelという2つのサブフォルダがあり、modelフォルダには再利用できるオープンソースコンポーネントTRTCChorusRoomが含まれています。`TRTCChorusRoom.h`ファイルでこのコンポーネントが提供するインターフェース関数を確認し、対応するインターフェースを使用してカスタマイズしたUIを実装することができます。
![](https://main.qcloudimg.com/raw/319beb14d72a43120e102380278aa1da.png)


[](id:model.step1)
### 手順1：SDKの統合 
ボイスチャットコンポーネントTRTCVoiceRoom は、TRTC SDKとIM SDKに依存し、次の手順で2つのSDKをプロジェクトに統合することができます。

- **方法1：cocoapodsリポジトリを介する依存**
<dx-codeblock>
::: swift
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
:::
</dx-codeblock>

- **方法2：ローカルを介する依存**
開発環境でのcocoapodsリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。
<table>
<tr><th>SDK</th><th>ダウンロードページ</th><th>統合ガイド</th></tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">統合ドキュメント</a></td>
</tr><tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">統合ドキュメント</a></td>
</tr></table>

[](id:model.step2)
### 手順2：権限の設定
info.plistファイルに`Privacy > Camera Usage Description`、`Privacy > Microphone Usage Description`を追加し、マイクの権限を申請する必要があります。

[](id:model.step3)
### 手順3：TUIVoiceRoomコンポーネントをインポート
**cocoapodsを介してコンポーネントをインポートします**。具体的な操作は次のとおりです。
1. プロジェクトディレクトリ下の`Source`、`Resources`、`TXAppBasic`フォルダ、`TUIVoiceRoom.podspec`ファイルをプロジェクトディレクトリ下へコピーします。
2. `Podfile`ファイル内に以下の依存関係を追加します。その後、`pod install`コマンドを実行すると、インポートが完了します。
<dx-codeblock>
::: swift
pod 'TXAppBasic', :path => "TXAppBasic/"
pod 'TXLiteAVSDK_TRTC'
pod 'TUIVoiceRoom', :path => "./", :subspecs => ["TRTC"] 
:::
</dx-codeblock>

[](id:model.step4)
### 手順4：コンポーネントの作成およびログイン
1. TRTCVoiceRoomの`sharedInstance`クラスメソッドを呼び出せば、TRTCVoiceRoomプロトコルを遵守するインスタンスオブジェクトを作成できます。`shared`クラスメソッドを呼び出しTRTCVoiceRoomImpインスタンスオブジェクトを取得して直接使用することもできます。両者は、TRTCVoiceRoomのインターフェースでの使い方に違いはありません。
2. `setDelegate`関数を呼び出して、コンポーネントのイベントコールバック通知を登録します。
3. `login`関数を呼び出してコンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
<table>    
<tr><th>パラメータ名</th><th>機能</th></tr><tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> で SDKAppIDを表示できます。</td>
</tr><tr>
<td>userId</td>
<td>現在のユーザーID。文字列タイプでは、英語のアルファベット（a-z、A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。業務の実際のアカウントシステムと組み合わせてご自身で設定することをお勧めします。</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、<a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSigの計算方法</a>をご参照ください。</td>
</tr></tr>
<tr>
<td>callback</td>
<td>ログインのコールバック。成功時にcodeは0になります。</td>
</tr></table>
<dx-codeblock>
::: Swift Swift
// Swift例
// コード内でビジネスロジックを担当するクラス
class YourController {
    // 属性を計算してシングルトンオブジェクトを取得
    var voiceRoom: TRTCVoiceRoomImp {
        return TRTCVoiceRoomImp.shared()
    }
    
    // その他のコードロジック
    ......
}
// voiceroomプロキシの設定
self.vocieRoom. setDelegate(delegate: voiceRoomDelegate)

// コール方法は以下のとおり。クロージャ―の中には weak self を使用して循環引用にしないことをお勧めします（以下の例示コードでは、 weak self 例を省略）
self.vocieRoom.login(sdkAppId: sdkAppID, userId: userId, userSig: userSig) { [weak self] (code, message) in
    guard let `self` = self else { return }
    // コールバックビジネスロジック        
}
:::
</dx-codeblock>

[](id:model.step5)
### 手順5：管理者側での配信開始
1. 管理者は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 管理者は、`createRoom`を呼び出して新しいボイスチャットルームを作成します。この時にルームID、マイク・オンに管理者の確認の要否、マイク数などルームのプロパティ情報を渡します。
3. 管理者は、ルーム作成に成功した後、`enterSeat`を呼び出して参加します。
4. 管理者は、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時、マイクリストの変更をUI上に更新することができます。
5. 管理者は、マイクリストのメンバーが参加した`onAnchorEnterSeat`というイベント通知も受信します。この時、マイク集音は自動的に開始されます。

![](https://main.qcloudimg.com/raw/256ebe5ce1426b3f175c8c8b68095d5b.png)

サンプルコード：
<dx-codeblock>
::: swift
// 1.管理者は、ニックネームおよびプロフィール画像を設定します
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 結果のコールバック           
}

// 2.管理者側でルームを作成します
let param = VoiceRoomParam.init()
Param.roomName = "ルーム名"
param.needRequest = true // リスナーのマイク・オンに対する管理者の同意の要否
param.coverUrl = 「カバーURL」
param.seatCount = 7 // ルームの座席数。ここでは計7席あり、管理者が1席を占め、残り6席がリスナーとなります
param.seatInfoList = []

for _ in 0..< param.seatCount {
    let seatInfo = VoiceRoomSeatInfo.init()
    param.seatInfoList.append(seatInfo)
}

self.voiceRoom.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { reutrn }
    // ルーム作成成功後、席の占有を開始
    self.voiceRoom.enterSeat(seatIndex: 0) { [weak self] (code, message) in
        guard let `self` = self else { return }
        if code == 0 {
            // 管理者による席の占有成功
        }else{
            // 管理者による席の占有失敗
        }
    }
}

// 3.席の占有に成功した後、onSeatListChangeイベント通知を受信します
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // マイクリストの更新
}

// 4. onAnchorEnterSeatイベント通知を受信します
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
  // 管理者のマイク・オンイベントの処理
}

:::
</dx-codeblock>

[](id:model.step6)
### 手順6：リスナー側の視聴
1. リスナー側は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. リスナー側は、業務バックエンドに最新のボイスチャットルームのルームリストを取得します。
>?Appのボイスチャットルームリストは、デモンストレーション用のためだけのものです。ボイスチャットルームリストのビジネスロジックは様々です。Tencent Cloudは現在、ボイスチャットルームリストの管理サービスを提供していませんので、ご自身でボイスチャットのルームリストを管理してください。
3. リスナー側は、`getRoomInfoList`を呼び出してルームの詳細情報を取得します。この情報は、管理者側が`createRoom`を呼び出してボイスチャットルームを作成するときに設定する簡単な説明情報です。
>!ボイスチャットルームのリストに十分に包括的な情報がある場合は、 `getRoomInfoList` の呼び出しに関する手順をスキップできます。
4．リスナーは1つのボイスチャットルームを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
5. 入室後、コンポーネントの`onRoomInfoChange` ルーム属性変更イベント通知を受信します。この時、ルーム属性を記録し、それに応じた修正を行うことができます。例：UIに表示するルーム名、発言者にする際の管理者への同意リクエストの要否の記録など。
6. 入室後は、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時、マイクリストの変更をUI上に更新することができます。
7. 入室後に、マイクリストにキャスターが参加した`onAnchorEnterSeat`というイベント通知も受信します。


![](https://main.qcloudimg.com/raw/33432f97eb632fbb9710a59cba9e4469.png)


<dx-codeblock>
::: Swift Swift
// 1.リスナーは、ニックネームおよびプロフィール画像を設定します
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 結果のコールバック           
}

// 2.業務バックエンドから取得したルームリストをroomListと仮定します
let roomList: [Int] = getRoomIDList() // ルームIDリストを取得する関数

// 3.getRoomInfoListを呼び出すことによって、ルームの詳細情報を取得します
self.voiceRoom.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [VoiceRoomInfo]) in
    //結果の取得。この時、UIの更新が可能
}

// 4.ボイスチャットルームを選択後、roomIdを渡して入室します
self.voiceRoom.enterRoom(roomID: roomInfo.roomID) { (code, message) in
    // 入室結果コールバック
    if code == 0 {
       // 入室に成功
    }
}

// 5.入室に成功後、onRoomInfoChangeイベント通知を受信します
func onRoomInfoChange(roomInfo: VoiceRoomInfo) {
    // ルーム名などの情報の更新可
}

// 6.入室に成功後、onSeatListChangeイベント通知を受信します
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // マイクリストを更新
}

// 7. onAnchorEnterSeatイベント通知を受信します
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // マイク・オンイベントの処理
}
:::
</dx-codeblock>

[](id:model.step7)
### 手順7：マイク管理
<dx-tabs>
::: 管理者側
1. `pickSeat`は、対応するマイクおよびリスナーのuserIdを渡し、視聴者を発言できるように招待できます。ルーム内の全メンバーは`onSeatListChange`および`onAnchorEnterSeat`というイベント通知を受信します。
2. `kickSeat`は、対象となるマイクを渡した後、キックアウトしてマイク・オフにすることができます。ルーム内の全メンバーは`onSeatListChange`および`onAnchorLeaveSeat`というイベント通知を受信します。
3. `muteSeat`は、対応するマイクを渡した後、ミュート/ミュート解除をすることができます。ルーム内の全参加者は`onSeatListChange`および`onSeatMute`というイベント通知を受信します。
4．`closeSeat`は、対応するマイクを送信後、任意のマイクのクローズ/解除をすることができます。クローズ後は、リスナー側はこれ以上マイクを使用することはできません。ルーム内の全参加者は`onSeatListChange`および`onSeatClose`というイベント通知を受信します。
![](https://main.qcloudimg.com/raw/367a0c670d2f9899d0b311ed1f322ea3.png)
:::
::: リスナー側
1. `enterSeat`は、対応するマイクを渡した後、マイク・オンにすることができます。ルーム内の全参加者は`onSeatListChange`および`onAnchorEnterSeat`のイベント通知を受信します。
2. `leaveSeat`で、自主的にマイク・オフにします。ルーム内の全参加者は`onSeatListChange`および`onAnchorLeaveSeat`のイベント通知を受信します。

![](https://main.qcloudimg.com/raw/8d385dd387b6255b8512dbff5829e88a.png)

マイク操作後のイベント通知の順番は次のとおりです。callback > onSeatListChange > onAnchorEnterSeat など独立したイベント。

<dx-codeblock>
::: swift
// case1: 1. 管理者がピックして1号マイクをマイク・オンにします
self.voiceRoom.pickSeat(seatIndex: 1, userId: "123") { (code, message) in
    // 2. 結果のコールバック
	if code == 0 {
	}
}

// 3. onSeatListChangeコールバックを受信し、マイクリストを更新します
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // 更新したマイクリスト
}

// 4.単一のマイク変更の通知によって、ここでリスナーが実際にマイク・オンに成功したかを判断することができます
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // マイク・オンイベントの処理
}
:::
</dx-codeblock>

<dx-codeblock>
::: swift
// case2: 1. リスナーによる自主的な2号マイクのマイク・オン
voiceRoom.enterSeat(seatIndex: 2) { (code, message) in
    // 2. マイク・オン結果のコールバック
	if code == 0 {
	}
}

// 3. onSeatListChangeコールバックを受信し、マイクリストを更新します
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // 更新したマイクリスト
}

// 4.単一のマイク変更の通知によって、ここでご自身が適切な処理を行っているか判断することができます
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // マイク・オンイベントの処理
}
:::
</dx-codeblock>

:::
</dx-tabs>

[](id:model.step8)
### 手順8：招待シグナリングの使用
[マイク管理](#model.step7)では、リスナーがマイク・オン/オフにする場合や、管理者が視聴者を発言できるように招待する場合は、相手の同意を必要とせずに直接操作することができます。
Appが次の操作の業務フローを実施するために、相手の同意を必要とする場合、招待シグナリングによって対応するサポートを提供することができます。
<dx-tabs>
::: リスナーからの自主的なマイク・オン申請
1. リスナー側が`sendInvitation`を呼び出し、管理者のuserIdおよび業務のカスタムコマンドワードなどを渡します。この時、関数が1つのinviteIdを返しますので、このinviteIdを記録します。
2. 管理者側は、`onReceiveNewInvitation`というイベント通知を受信します。この時UIでウィンドウをポップアップさせ、管理者に同意の有無をたずねることができます。
3. 管理者が同意を選択後、`acceptInvitation`を呼び出してinviteIdを渡します。
4. リスナー側は、`onInviteeAccepted`というイベント通知を受信し、`enterSeat`を呼び出してマイク・オンにします。

![](https://main.qcloudimg.com/raw/5ccdb15f63efa127aa883ca6a7bcd80d.png)

<dx-codeblock>
::: Swift Swift
// リスナー側の視点
// 1. sendInvitationを呼び出し、1号マイクの使用をリクエストします
let inviteId = self.voiceRoom.sendInvitation(cmd: "ENTER_SEAT", userId: ownerUserId, content: "1") { (code, message) in
    // 送信結果のコールバック
}
// 2.招待のリクエスト同意を受信し、正式にマイク・オンになります
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.enterSeat(seatIndex: ) { (code, message) in
            // マイク・オン結果のコールバック
        }
    }
}

// 管理者側の視点
// 1.管理者がリクエストを受信します
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 2.管理者がリスナーのリクエストに同意します
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
:::
</dx-codeblock>
:::
::: 管理者からの招待によるリスナーのマイク・オン
1. 管理者側が`sendInvitation`を呼び出し、リスナーのuserIdおよび業務のカスタムコマンドワードなどを渡します。この時、関数が1つのinviteIdを返しますので、このinviteIdを記録します。
2. リスナー側は、`onReceiveNewInvitation`というイベント通知を受信します。この時UIでウィンドウをポップアップさせ、リスナーに同意の有無をたずねることができます。
3. リスナーが同意を選択後、`acceptInvitation`を呼び出してinviteIdを渡します。
4. 管理者側は、`onInviteeAccepted`というイベント通知を受信し、`pickSeat`を呼び出しリスナーをピックしてマイク・オンにします。

![](https://main.qcloudimg.com/raw/5515f49d6e30410e12cd828b75a8db0b.png)


<dx-codeblock>
::: java java
// 管理者側の視点
// 1.管理者はsendInvitationを呼び出して、リスナー「123」をピックして2号マイクのマイク・オンをリクエストします
let inviteId = self.voiceRoom.sendInvitation(cmd: "PICK_SEAT", userId: ownerUserId, content: "2") { (code, message) in
    // 送信結果のコールバック
}

// 2.招待のリクエスト同意を受信し、正式にマイク・オンになります
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.pickSeat(seatIndex: ) { (code, message) in
            // マイク・オン結果のコールバック
        }
    }
}

// リスナー側の視点
// 1.リスナーがリクエストを受信します
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 2.リスナーが管理者のリクエストに同意します
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
:::
</dx-codeblock>
:::
</dx-tabs>

[](id:model.step9)
### 手順9：文字チャットおよび弾幕コメントの実装
- `sendRoomTextMsg`によって通常のテキストメッセージを送信できるようになり、このルーム内のすべてのキャスターおよびリスナーが`onRecvRoomTextMsg`のコールバックを受信することができます。
IMバックエンドは、デフォルトでNGワードフィルター規則を有し、NGワードと認識されたテキストメッセージはクラウドに転送されることはありません。
<dx-codeblock>
::: Swift Swift
// 送信側：テキストメッセージの送信
self.voiceRoom.sendRoomTextMsg(message: message) { (code, message) in
         

}
// 受信側：テキストメッセージのモニタリング
func onRecvRoomTextMsg(message: String, userInfo: VoiceRoomUserInfo) {
    // 受信したmessage情報の処理方法        
}
:::
</dx-codeblock>
- `sendRoomCustomMsg`によって、カスタム（シグナル）メッセージを送信できます。当該ルーム内のすべてのキャスターとリスナーが`onRecvRoomCustomMsg`コールバックを受信できます。
 カスタムメッセージは、カスタマイズ信号の送信によく用いられます。例えば、「いいね」情報の発信やブロードキャストに使用します。
<dx-codeblock>
::: Swift Swift
// 例：送信側：カスタマイズCmdによって、弾幕と「いいね」情報を区分することができます
// eg:「CMD_DANMU」は弾幕コメントを表し、「CMD_LIKE」は「いいね」情報を表します
self.vocieRoom.sendRoomCustomMsg(cmd: "CMD_DANMU", message: "hello world", callback: nil)
self.voiceRoom.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
// 受信側：カスタムメッセージのモニタリング
func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: VoiceRoomUserInfo) {
    if cmd == "CMD_DANMU" {
        // 弾幕コメントの受信
    }
    if cmd == "CMD_LIKE" {
        // 「いいね」情報の受信
    }
}
:::
</dx-codeblock>
