## デモンストレーション
[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076) して Demo をインストールして、マイク管理、低遅延音声インタラクション、文字チャットなどのボイスチャットのユースケースにおけるTRTCの関連能力を含めた、ボイスチャットルームの機能を体験できます。











ボイスチャットルーム機能をすばやく実装する必要がある場合、当社が提供するDemoをもとにアダプターを修正するか、または当社が提供するTRTCVoiceRoom コンポーネントでUIのカスタマイズを実装することができます。

<span id="DemoUI"> </span>
## Demo の UI の再利用

<span id="ui.step1"></span>
### 手順1：アプリケーションの新規作成
1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2．【今すぐ開始】をクリックし、例えば、`TestVoiceRoom`などアプリケーション名を入力して、【アプリケーションの作成】をクリックします。

>?本機能はTencent Cloud [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) と [IM](https://intl.cloud.tencent.com/document/product/1047) という2つの基本的な PaaS サービスを同時に使用し、TRTCをアクティブにした後、IM サービスを同期的にアクティブにすることができます。 IM は付加価値サービスであり、請求ルールの詳細については [Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。



<span id="ui.step2"></span>
### 手順2：SDKおよびDemoのソースコードをダウンロード
１．マウスを該当するカードまで移動し、【[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Android)】をクリックしてGithub（または【[ZIP](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip)】をクリック）にジャンプして、関連するSDK および付属のDemoのソースコードをダウンロードします。
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. ダウンロード完了後、Tencent Real-Time Communicationコンソールに戻り、【ダウンロードしました。次のステップ】をクリックすれば、SDKAppIDおよびキー情報をクエリできます。

<span id="ui.step3"></span>
### 手順3：Demoプロジェクトファイルの設定
1．[手順2](#ui.step2) でダウンロードしたソースコードパッケージを解凍します。
2.  `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` ファイルを探して開きます。
3.  `GenerateTestUserSig.h`ファイルの関連パラメータの設定：
  <ul><li>SDKAPPID：デフォルトは0、実際のSDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</li></ul> 
    <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4．Tencent Real-Time Communicationコンソールに戻り、【貼り付け完了。次のステップ】をクリックします。
5.【ガイドを閉じてコンソールへ進む】をクリックします。

>!本書で言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになり、そのため**のこの手法はローカルDemo実行および機能デバッグにのみ適合します**。
≻ UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

<span id="ui.step4"></span>
### 手順4：Demoの動作
Xcode（11.0以上のバージョン）を使用してソースコードプロセス `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace`を開き、【実行】をクリックすれば本 Demoのデバッグを開始することができます。

<span id="ui.step5"></span>
### 手順5：Demo ソースコードの修正
ソースコードのTRTCVoiceRoomDemo フォルダは、 ui と modelの2つのサブフォルダを含んでいます。ui フォルダには、インターフェースコードとインターフェース関連のロジックが含まれています。以下の表にはそれぞれのswiftファイルまたはフォルダ及びそれらが対応する UI をリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ | 機能説明 |
|:-------:|:--------|
|TRTCVoiceRoomEnteryController|このフォルダはすべてのViewController の初期化取得方法を含んでおり、このインスタンスによってすばやく ViewController オブジェクトを取得できます。|
| NetworkRoomManager | 業務バックエンド交互相関。 | 
| TRTCCreateVoiceRoomViewController |ボイスチャットルーム画面のロジック作成。 | 
| TRTCVoiceRoomListViewController | 表画面のロジック。 | 
| TRTCVoiceRoomViewController | メインルーム画面。キャスターおよび視聴者の2種類のインターフェースがあります。 | 

各`TRTC'XXXX'ViewController`フォルダには、`ViewController`、`RootView`および`ViewModel`が含まれ、各ファイルの役割は下表に示すとおりです。

| ファイル | 機能説明 |
|:-------:|:--------|
| ViewController | 画面制御装置。画面のルーティング作業、 RootView および ViweModel のバインディング作業を担当。 | 
| RootView | ビュー。すべてのビューのレイアウト。 | 
| ViewModel | ビュー制御装置。ビューのインタラクションに応答し、ビューの応答ステータスを返す作業を担当。 

<span id="model"> </span>
## UIカスタマイズの実装
[ソースコード]  のtrtcvoiceroomdemo フォルダには、 ui と modelの2つのサブフォルダがあり、model フォルダには再利用できるオープンソースコンポーネント TRTCVoiceRoomがあります。`TRTCVoiceRoom.swift`ファイルでこのコンポーネントが提供するインターフェース関数を見て、対応するインターフェースを使用してUI のカスタマイズ を実装することができます。
![](https://main.qcloudimg.com/raw/319beb14d72a43120e102380278aa1da.png)


<span id="model.step1"> </span>
### 手順1： SDKへの統合
ボイスチャットコンポーネントTRTCVoiceRoom は、TRTC SDK と IM SDKに依存し、次の手順で2つの SDKをプロジェクトに統合することができます。

**方法一：cocoapodsリポジトリを介する依存**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?2つの SDK 製品の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK) および [IM](https://github.com/tencentyun/TIMSDK) の Github トップページで取得することができます。

**方法二：ローカルを介する依存**
開発環境でのcocoapods リポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。

| SDK | ダウンロード画面 | ガイドの統合 |
|---------|---------|---------|
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK   | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/1047/34306) |

<span id="model.step2"> </span>
### 手順2：権限の設定
info.plist ファイルに Privacy > Camera Usage Description， Privacy > Microphone Usage Description を追加し、カメラとマイクの権限をリクエストする必要があります。

<span id="model.step3"> </span>
### 手順3： TRTCVoiceRoom コンポーネントをインポート
`iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCVoiceRoomDemo/model`ディレクトリのすべてのファイルをプロジェクトにコピーします。

<span id="model.step4"> </span>
### 手順4：コンポーネントの作成およびログイン
1.  TRTCVoiceRoom の`sharedInstance`クラスメソッドをコールすれば、 TRTCVoiceRoom プロトコルを遵守するインスタンスオブジェクトを作成できます。`shared`クラスメソッドをコールして TRTCVoiceRoomImpインスタンスオブジェクトを取得して直接使用することもできます。両者は、TRTCVoiceRoom のインターフェースの使用において何の違いもありません。
2. `setDelegate`関数をコールしてコンポーネントのイベントコールバック通知を登録します。
3. `login`関数をコールしてコンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
<table>    
<tr>
<th>パラメータ名</th>
<th>作用</th>
</tr>
<tr>
<td>sdkAppID</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">Tencent Real-Time Communicationコンソール</a> で SDKAppIDを表示できます。</td>
</tr>
<tr>
<td>userId</td>
<td>現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については<a href="https://intl.cloud.tencent.com/document/product/647/35166"> UserSig</a>の計算方法をご参照ください。</td>
</tr>
</tr>
<tr>
<td>callback</td>
<td>ログインのコールバック。成功時に code は0になります。</td>
</tr>
</table>

```swift
// Swift 例
// ビジネスロジックを担当するクラス
class YourController {
    // 属性を計算してシングルトンオブジェクトを取得
    var voiceRoom: TRTCVoiceRoomImp {
        return TRTCVoiceRoomImp.shared()
    }
    
    // その他のコードロジック
    ......
}
//  voiceroom プロキシの設定
self.vocieRoom. setDelegate(delegate: voiceRoomDelegate)

// コール方法は以下のとおり。クロージャ―の中には weak self を使用して循環参照にしないことをお薦めします（以下のサンプルコードでは、 weak self 例を省略）
self.vocieRoom.login(sdkAppId: sdkAppID, userId: userId, userSig: userSig) { [weak self] (code, message) in
    guard let `self` = self else { return }
    // コールバックビジネスロジック        
}
```

<span id="model.step5"> </span>
### 手順5：キャスター側の放送開始
1. キャスターは、[手順4](#model.step4) でログイン後、`setSelfProfile`をコールして自身のニックネームおよびプロファイル写真を設定することができます。
2. キャスターは、 `createRoom` をコールして新しいボイスチャットルームを作成します。この時にルーム ID、マイク・オンに管理者の確認の要否、マイク数などルームの属性情報を伝達します。
3. キャスターは、ルームの作成成功後、 `enterSeat` をコールして参加します。
4. キャスターは、コンポーネントの `onSeatListChange` マイクリスト変更イベント通知を受信します。この時、マイクリストの変更を UI 上に更新することができます。
5. キャスターは、マイクリストのメンバーが参加した `onAnchorEnterSeat` のイベント通知も受信します。この時はマイク集音は自動的に開始されます。

![](https://main.qcloudimg.com/raw/256ebe5ce1426b3f175c8c8b68095d5b.png)

サンプルコード：

```swift
// 1.キャスターは、ニックネームおよびプロファイル写真を設定します。
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 結果のコールバック           
}

// 2.キャスター側によるルーム作成
let param = VoiceRoomParam.init()
Param.roomName = "ルーム名"
param.needRequest = true // 視聴者のマイク・オンに対するキャスターの同意の要否
param.coverUrl = "カバーURL"
param.seatCount = 7; // 座席数。ここは計7席あり、管理者が1席を占めた後、残り6席は視聴者が占めます
param.seatInfoList = []
for _ in 0..<param.seatCount {
    let seatInfo = VoiceRoomSeatInfo.init()
    param.seatInfoList.append(seatInfo)
}
self.voiceRoom.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { reutrn }
    // ルーム作成成功後、席取りを開始
    self.voiceRoom.enterSeat(seatIndex: 0) { [weak self] (code, message) in
        guard let `self` = self else { return }
        if (code == 0) {
            // 管理者による席取り成功
        }else{
            // 管理者による席取り失敗
        }

    }
}

// 4.席取りの成功後、 onSeatListChange イベント通知を受信
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // マイクリストの更新
}
// 5.  onAnchorEnterSeat イベント通知を受信
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // キャスターのマイク・オンイベントの処理
}
```

<span id="model.step6"> </span>
### 手順6：視聴者の視聴
1. 視聴者側は、[手順4](#model.step4) でログイン後、`setSelfProfile`をコールして自身のニックネームおよびプロファイル写真を設定することができます。
2. 視聴者側は、業務バックエンドに最新のボイスチャットルームのルームリストを取得します。
 >?Demo のボイスチャットルームリストは、デモンストレーションでの使用のみです。ボイスチャットルームリストのビジネスロジックは様々です。Tencent Cloudは、ボイスチャットのルームリスト管理サービスを一時的に提供しませんので、自身でボイスチャットのルームリストを管理してください。
3. 視聴者側は、`getRoomInfoList`をコールしてルームの詳細情報を取得します。この情報は、キャスター側が`createRoom`をコールしてボイスルームを作成するときに設定する簡単な説明情報です。
 >!ボイスルームのリストに十分で全体的な情報がある場合は、`getRoomInfoList`のコール関連の手順をスキップできます。
4．視聴者は一つのチャットルームを選択し、 `enterRoom` をコールしてルームナンバーを渡すと、そのルームに入室できます。
5. 入室後、コンポーネントの `onRoomInfoChange` ルーム属性の変更イベント通知を受信します。この時はルーム属性を記録し相応の修正を行うことができます。例：UI に表示されるルーム名、マイク・オンにキャスターへの同意を求める要否の記録などを表示します。
6. 入室後は、コンポーネントの `onSeatListChange` マイクリスト変更イベント通知を受信します。この時、マイクリストの変更を UI上に更新することができます。
7. 入室後に、マイクリストにキャスターが参加した `onAnchorEnterSeat` というイベント通知も受信することがあります。


![](https://main.qcloudimg.com/raw/33432f97eb632fbb9710a59cba9e4469.png)

```swift
// 1.視聴者は、ニックネームおよびプロファイル写真を設定します。
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 結果のコールバック           
}

// 2.業務バックエンドから取得したルームリストを roomListと仮定します
let roomList: [Int] = getRoomIDList() // ルームID表を取得した関数

// 3. getRoomInfoList をコールすることによって、ルームの詳細情報を取得します
self.voiceRoom.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [VoiceRoomInfo]) in
    //結果の取得。この時、UIの更新が可能
}

// 4.ボイスチャットルームを選択後、 roomid を渡して入室します
self.voiceRoom.enterRoom(roomID: roomInfo.roomID) { (code, message) in
    // 入室結果コールバック
    if (code == 0) {
       //入室に成功
    }
}

// 5.入室に成功後、 onRoomInfoChange イベント通知を受信します
func onRoomInfoChange(roomInfo: VoiceRoomInfo) {
    // ルーム名などの情報の更新可
}

// 6.入室に成功後、 onSeatListChange イベント通知を受信します
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // マイクリストを更新
}

// 7.  onAnchorEnterSeat イベント通知を受信します
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // マイク・オンイベントの処理
}

```

<span id="model.step7"> </span>
### 手順7：マイク管理
キャスター側：
1. `pickSeat`は、対応するマイクおよび視聴者の userIdを渡し、着席してマイク・オンできます。ルーム内の全参加者は`onSeatListChange`および`onAnchorEnterSeat`のイベント通知を受信します。
2. `kickSeat`は、対応するマイクを渡した後、離席してマイク・オフにすることができます。ルーム内の全参加者は`onSeatListChange`および`onAnchorLeaveSeat`のイベント通知を受信します。
3. `muteSeat`は、対応するマイクを渡した後、ミュート／ミュート解除をすることができます。ルーム内の全参加者は `onSeatListChange` および `onSeatMute` のイベント通知を受信します。
4．`closeSeat`は、対応するマイクを送信後、任意のマイクのクローズ／解除をすることができます。クローズ後は、視聴者側はこれ以上マイクを使用することはできません。ルーム内の全参加者は`onSeatListChange`および`onSeatClose`のイベント通知を受信します。
![](https://main.qcloudimg.com/raw/367a0c670d2f9899d0b311ed1f322ea3.png)

視聴者側：
1. `enterSeat`は、対応するマイクを渡した後、マイク・オンにすることができます。ルーム内の全参加者は`onSeatListChange`および`onAnchorEnterSeat`のイベント通知を受信します。
2. `leaveSeat`は、自主的にマイク・オフにします。ルーム内の全参加者は`onSeatListChange`および`onAnchorLeaveSeat`のイベント通知を受信します。

![](https://main.qcloudimg.com/raw/8d385dd387b6255b8512dbff5829e88a.png)

マイク操作後のイベント通知の順序は次のとおりです。
callback > onSeatListChange > onAnchorEnterSeat など独立したイベント

```swift
// case1: キャスターによって、着席して1号マイクを使用
self.voiceRoom.pickSeat(seatIndex: 1, userId: "123") { (code, message) in
    // 結果のコールバック
}

// 3. onSeatListChange コールバックを受信し、マイクリストを更新
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // 更新したマイクリスト
}

// 4.単一マイクの変更通知によって、オーディエンスがマイク・オンに実際に成功しているか判断可
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // マイク・オンイベントの処理
}
```

```swift
// case2: オーディエンスは主動で2号マイクのマイク・オン
voiceRoom.enterSeat(seatIndex: 2) { (code, message) in
    // マイク・オン結果のコールバック
}

// 3. onSeatListChange コールバックを受信し、マイクリストを更新
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // 更新したマイクリスト
}

// 4.単一のマイク変更の通知によって、ここで自身が相応の処理を行っているか判断することができます。
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // マイク・オンイベントの処理
}
```

<span id="model.step8"> </span>
### 手順8：招待シグナリングの使用
 [マイク管理](#model.step7) では、視聴者がマイク・オン／オフにするか、キャスターによって着席してマイク・オンにするかは、相手の同意を必要とせずに直接操作することができます。
Appが相手の同意がなければ、次の操作の業務フローを実施できない場合は、招待シグナリングによって相応のサポートを行うことができます。
視聴者のマイク・オンにリクエストが必要な場合：
1. 視聴者側は、`sendInvitation`をコールしてキャスターの userId および業務のカスタムコマンドワードなどを渡します。この時、関数は1個の inviteIdを返しこの inviteIdを記録します。
2. キャスター側は、`onReceiveNewInvitation`のイベント通知を受信します。この時、 UI はウィンドウをポップアップして、キャスターに同意するかどうか照会することができます。
3. キャスターが同意を選択後、`acceptInvitation`をコールして inviteIdを渡します。
4. 視聴者側は、`onInviteeAccepted`のイベント通知を受信し、`enterSeat`をコールしてマイク・オンにします。

![](https://main.qcloudimg.com/raw/5ccdb15f63efa127aa883ca6a7bcd80d.png)

```swift
// 視聴者側の視点
// 1. sendInvitationをコールし、1号マイクの使用をリクエストします
let inviteId = self.voiceRoom.sendInvitation(cmd: "ENTER_SEAT", userId: ownerUserId, content: "1") { (code, message) in
    // 発信結果のコールバック
}
// 4.招待の同意リクエストを受信して、正式にマイク・オンにします
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.enterSeat(seatIndex: ) { (code, message) in
            // マイク・オン結果のコールバック
        }
    }
}

// キャスター側の視点
// 2.キャスターによるリクエストの受信
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 3.キャスターが視聴者のリクエストに同意
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
```

キャスターが招待を発信しないと、視聴者が着席してマイク・オンにできない場合：
1. キャスター側は、`sendInvitation`をコールしてオーディエンスの userId および業務のカスタマイズコマンドワードなどを渡します。この時、関数は1個の inviteIdを返しこの inviteIdを記録します。
2. 視聴者側は、`onReceiveNewInvitation`のイベント通知を受信します。この時、 UI はウィンドウをポップアップして、視聴者がマイク・オンに同意するかどうかを照会することができます。
3. 視聴者が同意を選択後、`acceptInvitation`をコールして inviteIdを渡します。
4. キャスター側は、`onInviteeAccepted`のイベント通知を受信し、`pickSeat`をコールし視聴者が着席してマイク・オンにします。

![](https://main.qcloudimg.com/raw/5515f49d6e30410e12cd828b75a8db0b.png)

```java
// キャスター側の視点
// 1.キャスターは、 sendInvitationをコールして、オーディエンス123を着席させて2号マイクのマイク・オンをリクエストします
let inviteId = self.voiceRoom.sendInvitation(cmd: "PICK_SEAT", userId: ownerUserId, content: "2") { (code, message) in
    // 発信結果のコールバック
}

// 4.招待の同意リクエストを受信して、正式にマイク・オンにします
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.pickSeat(seatIndex: ) { (code, message) in
            // マイク・オン結果のコールバック
        }
    }
}

// 視聴者側の視点
// 2.視聴者のリクエストの受信
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 3.視聴者がキャスターのリクエストに同意
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
```

<span id="model.step9"> </span>
### 手順9：文字チャットおよび弾幕コメントの実装
- `sendRoomTextMsg`によって通常のテキストメッセージを発信できるようになり、該当するルーム内の全てのキャスターおよび視聴者が`onRecvRoomTextMsg`のコールバックを受信することができます。
IMバックエンドは、デフォルトのNGワードフィルター規則を有し、NGワードと認識されたテキストメッセージはクラウドに転送されることはありません。

```swift
// 発信側：テキストメッセージの発信
self.voiceRoom.sendRoomTextMsg(message: message) { (code, message) in
         
}
// 受信側：テキストメッセージのモニタ
func onRecvRoomTextMsg(message: String, userInfo: VoiceRoomUserInfo) {
    // 受信したmessage情報の処理方法        
}
```
- `sendRoomCustomMsg`によってカスタマイズ（シグナリング）情報を発信することができます。そのルーム内の全てのキャスターおよび視聴者は`onRecvRoomCustomMsg`のコールバックを受信することができます。
 カスタマイズメッセージは、カスタマイズ信号の伝送によく用いられます。例：「いいね」情報の発信および放送。
 
```swift
// 例：発信側：カスタマイズ Cmd によって、弾幕と「いいね」情報を区分することができます
// eg:"CMD_DANMU"は弾幕コメントを表し、"CMD_LIKE"は「いいね」情報を表します
self.vocieRoom.sendRoomCustomMsg(cmd: “CMD_DANMU”, message: "hello world", callback: nil)
self.voiceRoom.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
// 受信側：カスタマイズメッセージのモニタ
func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: VoiceRoomUserInfo) {
    if cmd == "CMD_DANMU" {
        // 弾幕コメントの受信
    }
    if cmd == "CMD_LIKE" {
        // 「いいね」情報の受信
    }
}
```


