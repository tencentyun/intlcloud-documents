## デモンストレーション
[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)からAppをインストールして、デュエット低遅延コーラス、ギフトの送受信、文字チャットなどのChorusシーンにおけるTRTCの関連機能を含む、Chorusの機能を体験できます。
<table>
     <tr>
         <th style="text-align:center">管理者のマイク操作</th>  
         <th style="text-align:center">リスナーのマイク操作</th>  
     </tr>
<tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/206ba3492f4a2f18f36b1d5cba4e5558.jpg"/></td>
<td><img src="https://main.qcloudimg.com/raw/e52ccb64cd686f6af1c1f561d7969d36.jpg"/></td>
</tr>
</table>

Chorus機能にすばやくアクセスする必要がある場合、当社が提供するAppをもとに直接変更を加えて適応させるか、または当社が提供するTUIChorusコンポーネントでカスタマイズしたUIを実装することができます。
[](id:DemoUI)

## AppのUIの再利用
[](id:ui.step1)
### 手順1：アプリケーションの新規作成
1. TRTCコンソールにログインし、**開発支援**>**[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)**を選択します。
2. アプリケーション名（例：`TestChorus`）を入力し、**作成**をクリックします。
3. **ダウンロードしました。次のステップ**をクリックすると、この手順をスキップします。

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>?本機能はTencent Cloud[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPAASサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。


[](id:ui.step2)
### 手順2：Appソースコードのダウンロード
クリックして[TUIChorus](https://github.com/tencentyun/TUIChorus)に進み、ソースコードをCloneまたはダウンロードします。

[](id:ui.step3)
### 手順3：Appプロジェクトファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `TUIChorus/Debug/GenerateTestUserSig.swift`ファイルを見つけて開きます。
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
Xcode（11.0およびそれ以降のバージョン）を使用してソースコードプロセス`TUIChorus/TUIChorusApp.xcworkspace`を開き、**実行**をクリックすれば、このAppのデバッグが開始されます。

[](id:ui.step5)
### 手順5：Appソースコードの修正
ソースコードの`Source` フォルダは、uiとmodelの2つのサブフォルダを含んでいます。uiフォルダには、インターフェースコードとインターフェース関連のロジックが含まれています。以下の表にはそれぞれのswiftファイルまたはフォルダおよびそれらが対応するUIをリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ | 機能説明 |
|:-------:|:--------|
| TRTCChorusEnteryControl.swift|このファイルには、すべてのViewController初期化メソッドが含まれています。このインスタンスを介してViewControllerオブジェクトをすばやく取得することができます。|
| TRTCCreateChorusViewController | Chorusページのロジックを作成します。 |
| TRTCChorusViewController | メインルームページ。管理者および視聴者という2種類のインターフェースがあります。 |

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
2. ルームトピックを入力し、**一緒に歌う**をクリックします。

### ユーザーB
1. ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. ユーザーAが作成したルームナンバーを入力し、**入室する**をクリックします。<br>

>! ルームナンバーはユーザーAのルーム上部に表示されます。

[](id:model)
## UIカスタマイズの実装
[ソースコード](https://github.com/tencentyun/TUIChorus)の`Source`フォルダには、uiとmodelという2つのサブフォルダがあり、modelフォルダには再利用できるオープンソースコンポーネントTRTCChorusRoomが含まれています。`TRTCChorusRoom.h`ファイルでこのコンポーネントが提供するインターフェース関数を確認し、対応するインターフェースを使用してカスタマイズしたUIを実装することができます。
<img src="https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png">

[](id:model.step1)
### 手順1：SDKの統合 
ChorusコンポーネントTRTCChorusRoomは、TRTC SDKとIM SDKに依存し、次の手順で2つのSDKをプロジェクトに統合することができます。

- **方法1：cocoapodsリポジトリを介する依存**
  <dx-codeblock>
  ::: swift
  pod 'TXIMSDK_iOS'
  pod 'TXLiteAVSDK_TRTC'
  :::
  </dx-codeblock>
>?2つのSDK製品の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK)および[IM](https://github.com/tencentyun/TIMSDK)のGitHubトップページで取得することができます。
- **方法2：ローカルを介する依存**
開発環境でのcocoapodsリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。
<table>
<tr><th>SDK</th><th>ダウンロードページ</th><th>統合ガイド</th></tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35092">統合ドキュメント</a></td>
</tr><tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34307">統合ドキュメント</a></td>
</tr></table>

[](id:model.step2)

### 手順2：権限の設定
info.plistファイルにおいて、`Privacy > Microphone Usage Description`を追加して、マイクの権限を申請する必要があります。

[](id:model.step3)
### 手順3：TUIChorusコンポーネントのインポート
**cocoapodsを介してコンポーネントをインポートします**。具体的な操作は次のとおりです。
1. プロジェクトディレクトリ下の`Source`、`Resources`、`TXAppBasic`フォルダ、`TUIChorus.podspec`ファイルをプロジェクトディレクトリ下へコピーします。
2. `Podfile`ファイル内に以下の依存関係を追加します。その後、`pod install`コマンドを実行すると、インポートが完了します。
<dx-codeblock>
::: swift
pod 'TXAppBasic', :path => "TXAppBasic/"
pod 'TXLiteAVSDK_TRTC'
pod 'TUIChorus', :path => "./", :subspecs => ["TRTC"] 
:::
</dx-codeblock>

[](id:model.step4)

### 手順4：コンポーネントの作成およびログイン
1. TRTCChorusRoomの`sharedInstance`クラスメソッドを呼び出すと、TRTCChorusRoomプロトコルに準拠したインスタンスオブジェクトを作成することができます。また、`shared`クラスメソッドを呼び出して、TRTCChorusRoomインスタンスオブジェクトを取得し、直接使用することもできます。2つとも、TRTCChorusRoomのインターフェースでの使い方に違いはありません。
2. `setDelegate`関数を呼び出して、コンポーネントのイベントコールバック通知を登録します。
3. `login`関数を呼び出してコンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
<table>    
<tr><th>パラメータ名</th><th>機能</th></tr><tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> で SDKAppIDを表示できます。</td>
</tr><tr>
<td>userId</td>
<td>現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。</td>
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
    var chorusRoom: TRTCChorusRoom {
        return TRTCChorusRoom.shared()
    }
    
    // その他のコードロジック
    ......
}
// Chorusプロキシの設定
self.chorusRoom.setDelegate(delegate: chorusRoomDelegate)

// コール方法は以下のとおり。クロージャ―の中には weak self を使用して循環引用にしないことをお勧めします（以下の例示コードでは、 weak self 例を省略）
self.chorusRoom.login(sdkAppId: sdkAppID, userId: userId, userSig: userSig) { [weak self] (code, message) in
    guard let `self` = self else { return }
    // コールバックビジネスロジック        
}
:::
</dx-codeblock>

[](id:model.step5)
### 手順5：管理者によるルームの作成
1. 管理者は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 管理者は、`createRoom`を呼び出して新しいChorusルームを作成します。この時、ルームID、マイク・オンにすることの管理者の確認の要否などルームの属性情報を渡します。
3. 管理者は、ルームの作成に成功した後、`enterSeat`を自動的に呼び出して第1メインボーカルに参加します。
4. 管理者は、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時、マイクリストの変更をUI上に更新することができます。
5. 管理者は、マイクリストのメンバーが参加した`onAnchorEnterSeat`というイベント通知も受信します。この時、マイク集音は自動的に開始されます。

![](https://qcloudimg.tencent-cloud.cn/raw/7346adee3042426ca4c9f72777cebd2d.png)

サンプルコード：
<dx-codeblock>
::: swift
// 1.管理者は、ニックネームおよびプロフィール画像を設定します
self.chorusRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 結果のコールバック           
}

// 2.管理者側でルームを作成します
let param = RoomParam.init()
Param.roomName = "ルーム名"
param.needRequest = true // リスナーのマイク・オンに対する管理者の同意の要否
param.coverUrl = "カバーURL"
param.seatCount = 2 // ルームの座席数。ここには、メインボーカルとサブボーカルの計2席があります
param.seatInfoList = []

for _ in 0..< param.seatCount {
    let seatInfo = SeatInfo.init()
    param.seatInfoList.append(seatInfo)
}

self.chorusRoom.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { reutrn }
    // 作成に成功
    
    // 3.マイク・オン
    self.chorusRoom.enterSeat(seatIndex: 0) { [weak self] (code, message) in
        guard let `self` = self else { return }
        if code == 0 {
            // 管理者による席の占有成功
        }else{
            // 管理者による席の占有失敗
        }
    }
} 

// 4.マイク・オンに成功した後、onSeatListChangeイベント通知を受信します
func onSeatListChange(seatInfoList: [SeatInfo]) {
    // マイクリストの更新
}

// 5.  onAnchorEnterSeatイベント通知を受信
func onAnchorEnterSeat(index: Int, user: UserInfo) {
  // 管理者のマイク・オンイベントの処理
}

:::
</dx-codeblock>

[](id:model.step6)
### 手順6：リスナー側の視聴
1. リスナー側は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. リスナー側は、業務バックエンドから最新のChorusのルームリストを取得します。
>?App内のChorusルームリストはデモに使用するためだけのものです。Chorusルームリストの業務ロジックは千差万別です。現在、Tencent CloudはChorusルームリスト管理のサービスを提供していません。各自でご自分のChorusルームリストを管理してください。
3. リスナー側は、`getRoomInfoList`を呼び出してルームの詳細情報を取得します。この情報は、管理者側が`createRoom`を呼び出してChorusルームを作成するときに設定する簡単な説明情報です。
>!Chorusルームリストに十分に包括的な情報がある場合は、`getRoomInfoList`の呼び出しに関する手順をスキップできます。
4. リスナーは1つのChorusルームを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
5. 入室後、コンポーネントの`onRoomInfoChange` ルーム属性変更イベント通知を受信します。この時、ルーム属性を記録し、それに応じた修正を行うことができます。例：UIに表示するルーム名、発言者にする際の管理者への同意リクエストの要否の記録など。
6. 入室後は、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時、マイクリストの変更をUI上に更新することができます。
7. 入室後に、マイクリストにキャスターが参加した`onAnchorEnterSeat`というイベント通知も受信します。

![](https://qcloudimg.tencent-cloud.cn/raw/f225633062cf83d749ae8137cbb26fe1.png)
<dx-codeblock>
::: Swift Swift
// 1.リスナーは、ニックネームおよびプロフィール画像を設定します
self.chorusRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 結果のコールバック           
}

// 2.業務バックエンドから取得したルームリストをroomListと仮定します
let roomList: [Int] = getRoomIDList() // ルームIDリストを取得する関数

// 3. getRoomInfoListを呼び出すことによって、ルームの詳細情報を取得します
self.chorusRoom.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [RoomInfo]) in
    //結果の取得。この時、UIの更新が可能
}

// 4.Chorusを選択後、roomIdを渡して入室します
self.chorusRoom.enterRoom(roomID: roomInfo.roomID) { (code, message) in
    // 入室結果コールバック
    if code == 0 {
       // 入室に成功
    }
}

// 5.入室に成功後、onRoomInfoChangeイベント通知を受信します
func onRoomInfoChange(roomInfo: RoomInfo) {
    // ルーム名などの情報の更新可
}

// 6.入室に成功後、onSeatListChangeイベント通知を受信します
func onSeatListChange(seatInfoList: [SeatInfo]) {
    // マイクリストを更新
}

// 7. onAnchorEnterSeatイベント通知を受信します
func onAnchorEnterSeat(index: Int, user: UserInfo) {
    // マイク・オンイベントの処理
}
:::
</dx-codeblock>

[](id:model.step7)
### 手順7：マイク管理
<dx-tabs>
::: 管理者側
1. `pickSeat`は、対応するマイクおよびリスナーのuserIdを渡し、視聴者を発言できるように招待できます。ルーム内の全メンバーは`onSeatListChange`および`onAnchorEnterSeat`というイベント通知を受信します。
2. `kickSeat`は、対象となるマイクを渡して、コーラスが終了した後にキックアウトしてマイク・オフにすることができます。ルーム内の全メンバーは`onSeatListChange`および`onAnchorLeaveSeat`というイベント通知を受信します。
3．`closeSeat`は、対応するマイクを送信後、任意のマイクのクローズ/解除をすることができます。クローズ後は、リスナー側はこれ以上マイクを使用することはできません。ルーム内の全参加者は`onSeatListChange`および`onSeatClose`というイベント通知を受信します。
![](https://qcloudimg.tencent-cloud.cn/raw/bbb72bdc50cfd1b5d4b567239b035d32.png)
:::
::: リスナー側
1. `enterSeat`は、対象となるマイクを渡した後、マイク・オンにすることができます。ルーム内の全メンバーは`onSeatListChange`および`onAnchorEnterSeat`というイベント通知を受信します。
2. `leaveSeat`は、コーラスの終了後、視聴者側が自主的にマイク・オフを申請できます。ルーム内の全メンバーは`onSeatListChange`および`onAnchorLeaveSeat`というイベント通知を受信します。

![](https://qcloudimg.tencent-cloud.cn/raw/9747219d17f955530c5e502745008dce.png)

マイク操作後のイベント通知の順番は次のとおりです。callback > onSeatListChange > onAnchorEnterSeat など独立したイベント。

<dx-codeblock>
::: swift
// case1: 管理者がピックして1号マイクをマイク・オンにします
self.chorusRoom.pickSeat(seatIndex: 1, userId: "123") { (code, message) in
    // 結果のコールバック
}

// 3. onSeatListChangeコールバックを受信し、マイクリストを更新します
func onSeatListChange(seatInfoList: [ChorusRoomSeatInfo]) {
    // 更新したマイクリスト
}

// 4.単一のマイク変更の通知によって、ここでリスナーが実際にマイク・オンに成功したかを判断することができます
func onAnchorEnterSeat(index: Int, user: ChorusRoomSeatInfo) {
    // マイク・オンイベントの処理
}
:::
</dx-codeblock>

<dx-codeblock>
::: swift
// case2: リスナーによる自主的なサブボーカルマイク
chorusRoom.enterSeat(seatIndex: 1) { (code, message) in
    // マイク・オン結果のコールバック
}

// 3. onSeatListChangeコールバックを受信し、マイクリストを更新します
func onSeatListChange(seatInfoList: [SeatInfo]) {
    // 更新したマイクリスト
}

// 4.単一のマイク変更の通知によって、ここでご自身が適切な処理を行っているか判断することができます
func onAnchorEnterSeat(index: Int, user: UserInfo) {
    // マイク・オンイベントの処理
}
:::
</dx-codeblock>
:::
</dx-tabs>

[](id:model.step8)
### 手順8：招待シグナリングの使用
[マイク管理](#model.step7)では、リスナーがマイク・オン/オフにする場合や、管理者が視聴者を発言できるように招待する場合は、相手の同意を必要とせずに直接操作することができます。
Appにおいて相手の同意がなければ、次の操作の業務フローを実施できない場合は、招待シグナリングによって相応のサポートを行うことができます。
<dx-tabs>
::: リスナーからの自主的なマイク・オン申請
1. リスナー側が`sendInvitation`を呼び出し、管理者のuserIdおよび業務のカスタムコマンドワードなどを渡します。この時、関数が1つのinviteIdを返しますので、このinviteIdを記録します。
2. 管理者側は、`onReceiveNewInvitation`というイベント通知を受信します。この時UIでウィンドウをポップアップさせ、管理者に同意の有無をたずねることができます。
3. 管理者が同意を選択後、`acceptInvitation`を呼び出してinviteIdを渡します。
4. リスナー側は、`onInviteeAccepted`というイベント通知を受信し、`enterSeat`を呼び出してマイク・オンにします。

![](https://qcloudimg.tencent-cloud.cn/raw/1b37fa84f59c81dc89bf50ce4e30551f.png)

<dx-codeblock>
::: Swift Swift
// リスナー側の視点
// 1. sendInvitationを呼び出し、1号マイクの使用をリクエストします
let inviteId = self.chorusRoom.sendInvitation(cmd: "ENTER_SEAT", userId: ownerUserId, content: "1") { (code, message) in
    // 発信結果のコールバック
}
// 2.招待のリクエスト同意を受信し、正式にマイク・オンになります
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chorusRoom.enterSeat(seatIndex: ) { (code, message) in
            // マイク・オン結果のコールバック
        }
    }
}

// 管理者側の視点
// 1.管理者がリクエストを受信します
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 2.管理者がリスナーのリクエストに同意します
        self.chorusRoom.acceptInvitation(identifier: identifier, callback: nil)
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

![](https://qcloudimg.tencent-cloud.cn/raw/3a8b31dac680c70d1adac92287e645dd.png)


<dx-codeblock>
::: Swift Swift
// 管理者側の視点
// 1.管理者はsendInvitationを呼び出して、リスナー「123」をピックしてサブボーカルのマイクをリクエストします
let inviteId = self.chorusRoom.sendInvitation(cmd: "PICK_SEAT", userId: ownerUserId, content: "1") { (code, message) in
    // 発信結果のコールバック
}

// 2.招待のリクエスト同意を受信し、正式にマイク・オンになります
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chorusRoom.pickSeat(seatIndex: ) { (code, message) in
            // マイク・オン結果のコールバック
        }
    }
}

// リスナー側の視点
// 1.リスナーがリクエストを受信します
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 2.リスナーが管理者のリクエストに同意します
        self.chorusRoom.acceptInvitation(identifier: identifier, callback: nil)
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
  // 発信側：テキストメッセージの発信
  self.chorusRoom.sendRoomTextMsg(message: message) { (code, message) in
         

}
// 受信側：テキストメッセージのモニタリング
func onRecvRoomTextMsg(message: String, userInfo: UserInfo) {
    // 受信したmessage情報の処理方法        
}
:::
</dx-codeblock>
- `sendRoomCustomMsg`によって、カスタム（シグナリング）メッセージを送信できます。当該ルーム内のすべてのサブボーカルと視聴者が`onRecvRoomCustomMsg`コールバックを受信できます。
 カスタムメッセージは、カスタマイズ信号の送信によく用いられます。例えば、「いいね」情報の発信やブロードキャストに使用します。
  <dx-codeblock>
  ::: Swift Swift
  // 例：発信側：カスタマイズCmdによって、弾幕と「いいね」情報を区分することができます
  // eg:「CMD_DANMU」は弾幕コメントを表し、「CMD_LIKE」は「いいね」情報を表します
  self.chorusRoom.sendRoomCustomMsg(cmd: "CMD_DANMU", message: "hello world", callback: nil)
  self.chorusRoom.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
  // 受信側：カスタムメッセージのモニタリング
  func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: UserInfo) {
    if cmd == "CMD_DANMU" {
        // 弾幕コメントの受信
    }
    if cmd == "CMD_LIKE" {
        // 「いいね」情報の受信
    }
  }
  :::
  </dx-codeblock>

