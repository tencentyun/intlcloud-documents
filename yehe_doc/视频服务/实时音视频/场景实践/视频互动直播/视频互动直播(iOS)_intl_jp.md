## デモンストレーション
[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)からDemoをインストールすると、インタラクティブストリーミング機能の効果を体験していただくことができます。これにはマイク接続によるインタラクション、キャスターPK、低レイテンシーの視聴、弾幕チャットなど、TRTCのインタラクティブライブストリーミングシーンにおける関連機能が含まれています。

ビデオ・インタラクティブストリーミングの機能をすばやく実装する必要がある場合、当社が提供するDemoをもとに直接修正を加えてフィットさせることも、当社が提供するTRTCLiveRoomコンポーネントを使用し、カスタマイズしたUIを実現することも可能です。

[](id:DemoUI)
## DemoのUIの再利用

[](id:ui.step1)
### 手順1：アプリケーションの新規作成
1．TRTCコンソールにログインし、【開発支援】>【[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. 例えば、`TestLiveRoom`などアプリケーション名を入力して、【作成】をクリックします。

>!本機能はTencent Cloud[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。


[](id:ui.step2)
### 手順2：SDKおよびDemoソースコードをダウンロード
1. 実際の業務ニーズに基づき、SDKおよび付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、【ダウンロードしました。次のステップ】をクリックします。

[](id:ui.step3)
### 手順3：Demoプロジェクトファイルの設定
1. 設定変更画面に入り、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h`のファイルを見つけて開きます。
3. `GenerateTestUserSig.h`のファイルの関連するパラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。

>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるよようになります。そのため**のこの手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)
### 手順4：Demoの実行
Xcode（11.0以上のバージョン）を使用してソースコードプロセス`iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace`を開き、【実行】をクリックすれば、このDemoのデバッグが開始されます。

[](id:ui.step5)
### 手順5：Demoソースコードの修正
ソースコードのtrtcliveroomdemoフォルダは、ui とmodelという2つのサブフォルダを含んでいます。uiフォルダにはインターフェースコードが含まれています。以下の表には各 swiftファイルまたはフォルダおよび対応するUIをリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ | 機能説明 |
|:-------:|:--------|
| Anchor | キャスター側に関するUIの実装コード。 |
| Audience | 視聴者側に関するUIの実装コード。 |
| ChatRoom | テキストチャットルームと弾幕メッセージのUI実装コード。 |
| Common | 再利用可能なUIコンポーネントの実装コード。 |
| StatusView | ステータスのフローティングレイヤー、ログ情報やビデオのローディングアニメーションを表示するためにビデオ画面上にオーバーレイされます。 |
| LiveRoomMainViewController.swift | ビデオ・インタラクティブストリーミングのトップページ画面UI。 |


[](id:model)
## UIカスタマイズの実現

[ソースコード](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCLiveRoomDemo)の中のtrtcliveroomdemoフォルダには、uiとmodelという2つのサブフォルダがあり、modelフォルダには再利用できるオープンソースコンポーネントTRTCLiveRoomがあります。`TRTCLiveRoom.swift`ファイルでこのコンポーネントが提供するインターフェース関数を見て、対応するインターフェースを使用してUIのカスタマイズを実現することができます。
![](https://main.qcloudimg.com/raw/710358e4e170d44304cdb9bc991ad209.jpg)


[](id:model.step1)
### 手順1：SDKへの統合
オーディオビデオ通話コンポーネントTRTCLiveRoomは、TRTC SDKとIM SDKに依存し、次の手順で2つのSDKをプロジェクトに統合することができます。

**方法1：cocoapodsリポジトリを介する依存**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?2つのSDK製品の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK)および[IM](https://github.com/tencentyun/TIMSDK)のGithubトップページで取得することができます。

**方法2：ローカルを介する依存**
開発環境でのcocoapodsリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。

| SDK | ダウンロードページ | ガイドの統合 |
|---------|---------|---------|
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/1047/34306) |

[](id:model.step2)
### 手順2：権限の設定
info.plistファイルに`Privacy > Camera Usage Description`， `Privacy > Microphone Usage Description`を追加し、カメラとマイクの権限をリクエストする必要があります。

[](id:model.step3)
### 手順3：TRTCLiveRoomコンポーネントをインポート
`iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCLiveRoomDemo/model`ディレクトリのすべてのファイルをプロジェクトにコピーします。


<span id="model.step4"></span>
### 手順4：コンポーネントの作成およびログイン
1. TRTCLiveRoomIの`init`インターフェースを呼び出すと、TRTCLiveRoomコンポーネントのインスタンスオブジェクトを作成することができます。
2. 1つの`TRTCLiveRoomConfig`オブジェクトを作成したら、このオブジェクトにuseCDNFirstとCDNPlayDomainの属性を設定することができます。
 - useCDNFirstの属性：視聴者の視聴方式の設定に使用します。trueは、一般視聴者のCDN経由での視聴を表し、料金は安価ですがレイテンシーは高めです。falseは、一般視聴者の低レイテンシーによる視聴を表し、料金はCDN とマイク接続の間ですが、遅延を1s以内に抑えることができます。
 - CDNPlayDomainの属性：useCDNFirstの設定をtrueにした時に有効になり、CDN経由の視聴の再生ドメイン名の指定に利用します。CSSコンソール >【[Domain Management](https://console.cloud.tencent.com/live/domainmanage)】の画面からログインし、設定することができます。
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
<tr>
<td>config</td>
<td>グローバルコンフィギュレーション情報。ログイン時に初期化してください。ログイン後は変更できなくなります。<ul style="margin:0;">
<li>useCDNFirstの属性：視聴者の視聴方式の設定に使用します。trueは、一般視聴者のCDN経由での視聴を表し、料金は安価ですがレイテンシーは高めです。falseは、一般視聴者の低レイテンシーによる視聴を表し、料金は CDN とマイク接続の間ですが、遅延を1s以内に抑えることができます。</li>
<li>CDNPlayDomainの属性：useCDNFirstの設定をtrueにした時に有効になり、CDN経由の視聴の再生ドメイン名の指定に利用します。CSSコンソール>【<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>】の画面からログインして設定を行うことができます。</li>
</ul></td>
</tr>
<tr>
<td>callback</td>
<td>ログインのコールバック。成功時にcodeは0になります。</td>
</tr>
</table>

```
class LiveRoomController: UIViewController {
	let mLiveRoom = TRTCLiveRoom()
}
//useCDNFirst：trueは一般視聴者のCDN経由の視聴、falseは一般視聴者の低レイテンシーによる視聴を表します
//CDNPlayDomain：CDN視聴時に設定する再生ドメイン名を表します
let config = TRTCLiveRoomConfig(useCDNFirst: useCDNFirst, cdnPlayDomain: yourCDNPlayDomain)
mLiveRoom.login(SDKAPPID, userID, userSig, config) { (code, error) in
	if code == 0 {
		//ログイン成功
	}
}
```


[](id:model.step5)
### 手順5：キャスター側での配信開始
1. キャスターは、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. キャスターは、配信開始前に先に`startCameraPreview`を呼び出してカメラのプレビューを起動させ、インターフェース上に美顔調節ボタンを設置して呼び出し、`getBeautyManager`で美顔設定を行うことができます。
 >?エンタープライズ版以外のSDKは変顔やスタンプの機能をサポートしていません。
 >
3. 美顔効果の変更後、キャスターは`createRoom`を呼び出して新しいライブストリーミングルームを作成することができます。
4. キャスターが`startPublish`を呼び出し、プッシュを開始します。CDN視聴のサポートが必要な場合は、ログイン時に渡される`TRTCLiveRoomConfig`パラメータの中で`useCDNFirst`と`CDNPlayDomain`を指定し、`startPublish`時にライブストリーミング・プルストリーム用のstreamIDを指定してください。

![](https://main.qcloudimg.com/raw/eab281d702879ae87728d0064a090dca.jpg)

```swift
// 1.キャスターは、ニックネームおよびプロフィール画像を設定します。
mLiveRoom.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2.キャスターが配信開始前にプレビューを立ち上げ、美顔パラメータを設定します
let view = UIView()
parentView.add(view)
mLiveRoom.startCameraPreview(frontCamera: true, view: view, callback: nil)
mLiveRoom.getBeautyManager().setBeautyStyle(.nature)
mLiveRoom.getBeautyManager().setBeautyLevel(6)

// 3.キャスターがルームを作成します
let param = TRTCCreateRoomParam(roomName: "テストルーム", coverUrl: "")
mLiveRoom.createRoom(roomID: 123456789, roomParam: param) { [weak self] (code, error) in
	if code == 0 {
		// 4.キャスターがプッシュを開始し、ストリームがCDNに配信されます。
		self?.mLiveRoom.startPublish(streamID: mSelfUserId + "_stream", callback: nil)
	}
}
```


[](id:model.step6)
### 手順6：視聴者側の視聴
1. 視聴者側は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 視聴者側が業務バックエンドから最新のライブストリーミングルームリストを取得します。
 >?Demoの中のライブルームリストはデモに使用するためだけのものです。ライブルームリストの業務ロジックは千差万別です。現在、Tencent Cloudはライブルームリスト管理のサービスを提供していません。各自でご自分のライブストリーミングルームリストを管理してください。
 >
3. 視聴者側は、`getRoomInfos`を呼び出してルームの詳細情報を取得します。この情報は、キャスター側が`createRoom`を呼び出してライブストリーミングルームを作成するときに設定する簡単な説明情報です。
 >!ライブストリーミングルームのリストに十分で全体的な情報がある場合は、`getRoomInfos`の呼び出しに関する手順をスキップできます。
 >
4. 視聴者は1つのライブストリーミングルームを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
5.  `startPlay`を呼び出してキャスターのuserIdを渡し、再生を開始します。
 - ライブストリーミングルームリストにキャスターのuserID情報がすでに含まれている場合、視聴者は直接`startPlay`を呼び出してキャスターのuserIdを渡せば、再生を開始できます。
 - ルーム参加前にキャスターのuserIDが一時的に取得できない場合、視聴者側はルーム参加後にキャスターの`onAnchorEnter`のイベントコールバックを受信します。このコールバックの中にキャスターのuserID情報が含まれていますので、`startPlay`を呼び出せば再生できます。 


![](https://main.qcloudimg.com/raw/2ff8b30de38a3084c12af0513068dc6e.jpg)

```swift
// 1.業務バックエンドから取得したルームリストをroomListと仮定します
var roomList: [UInt32] = GetRoomList()

// 2. getRoomInfosを呼び出すことによって、ルームの詳細情報を取得します
mliveRoom.getRoomInfos(roomIDs: roomList, callback: { (code, msg, list) in
if code == 0 {
		// ルーム詳細情報の取得後、キャスターリスト画面でキャスターのニックネーム、プロフィール画像等の関連情報を表示できます。
	}
})

// 3.roomidを選択しルームに参加します
mliveRoom.enterRoom(roomID: roomID, callback: callback)

// 4.視聴者がキャスターのルーム参加の通知を受信すると、再生が開始されます
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
	// 5.視聴者がキャスターの画面を再生します
	mliveRoom.startPlay(userID: userID, view: renderView, callback: nil) 
}
```


[](id:model.step7)
### 手順7：視聴者とキャスターとのマイク接続
1. 視聴者側が`requestJoinAnchor`を呼び出し、キャスター側にマイク接続のリクエストを送信します。
2. キャスター側は`TRTCLiveRoomDelegate#onRequestJoinAnchor`（視聴者からのマイク接続のリクエストがあります）のイベント通知を受信します。
3. キャスター側は`responseJoinAnchor`を呼び出し、視聴者からのマイク接続リクエストを受け入れるかどうか決定できます。
4. 視聴者側が`TRTCLiveRoomDelegate#responseCallback`のイベント通知を受信します。この通知にはキャスターの処理結果が含まれています。
5. キャスターがマイク接続リクエストに同意したら、視聴者側は`startCameraPreview`を呼び出し、ローカルカメラを起動させます。その後`startPublish`を呼び出し、視聴者側のプッシュを開始します。
6. キャスター側は、視聴者側の起動の通知の後に、`TRTCLiveRoomDelegate#onAnchorEnter`（別のオーディオ・ビデオストリーミングが届いています）の通知を受信します。この通知には視聴者側のuserIdが含まれています。
7. キャスター側が`startPlay`を呼び出すと、マイク接続の視聴者の画面を見ることができます。

![](https://main.qcloudimg.com/raw/05a8c6af8bdc8b441f90b297e83106fc.jpg)

```swift
// 視聴者側：
// 1.視聴者側がマイク接続のリクエストを送信します
mliveRoom.requestJoinAnchor(reason: mSelfUserId + "あなたとのマイク接続をリクエスト", responseCallback: { [weak self] (agreed, reason) in 
	  // 4.キャスターが視聴者のリクエストを受け入れます
     if agreed {
     	 // 5.視聴者がプレビューを起動し、プッシュを開始します
     	 self?.mliveRoom.startCameraPreview(frontCamera: true, view: localView, callback: nil)
     	 self?.mliveRoom.startPublish(streamID: streamID, callback: nil)
     }        
}, callback: callback)

// キャスター側：
// 2.キャスター側がマイク接続のリクエストを受信します
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestJoinAnchor user: TRTCLiveUserInfo, reason: String?, timeout: Double) {
	// 3.相手側のマイク接続のリクエストに同意します
	mliveRoom.responseJoinAnchor(userID: userID, agree: true, reason: "マイク接続に同意")
}

// 6.キャスターがマイク接続の視聴者のマイク・オンの通知を受信します
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
	// 7.キャスターが視聴者の画面を再生します
	mliveRoom.startPlay(userID: userID, view: view, callback: nil)
}
```

[](id:model.step8)
### 手順8：キャスターとキャスターPK
1. キャスターAが`requestRoomPK`を呼び出し、キャスターBにPKのリクエストを送信します。
2. キャスターBが`TRTCLiveRoomDelegate onRequestRoomPK`のコールバック通知を受信します。
3. キャスターBが`responseRoomPK`を呼び出し、キャスターA のPKのリクエストを受け入れるか決定します。
4. キャスターBは、キャスターAのリクエストを受け入れたら、`TRTCLiveRoomDelegate onAnchorEnter`の通知を待ってから、`startPlay`を呼び出し、キャスターAを表示します。
5. PKのリクエストが同意されたかについて、キャスターAが`responseCallback`のコールバック通知を受信します。
6. キャスターAのリクエストが同意されたら、`TRTCLiveRoomDelegate onAnchorEnter`の通知を待ってから、`startPlay`を呼び出し、キャスターBを表示します 。

![](https://main.qcloudimg.com/raw/5632056b6d86541db841026e9488468b.jpg)

```swift
// キャスターA:
// キャスターAがルーム12345を作成します
mLiveRoom.createRoom(roomID: 12345, roomParam: param, callback: nil)

// 1.キャスターAがキャスターBにPKのリクエストを送信します
mLiveRoom.requestRoomPK(roomID: 54321, userID: "B", responseCallback: { (agree, reason) in
	// 5.同意の有無のコールバックを受信します
	if agree {
	}       
}, callback: callback)

// キャスターAがキャスターBのルーム参加のコールバックを受信します
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
	// 6.Bのルーム参加の通知を受信し、Bの画面を再生します
	mLiveRoom.startPlay(userID: userID, view: view, callback: callback)
}

// キャスターB：
// キャスターBがルーム54321を作成します
mLiveRoom.createRoom(roomID: 54321, roomParam: param, callback: nil)

// 2.キャスターBがキャスターAのメッセージを受信します
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestRoomPK user: TRTCLiveUserInfo, timeout: Double) {
	// 3.キャスターBがキャスターAに回答し、リクエストを受け入れます
	mLiveRoom.responseRoomPK(userID: userID, agree: true, reason: reason)
}

public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
	// 4.キャスターBがキャスターAのルーム参加の通知を受信し、キャスターAの画面を再生します
	mLiveRoom.startPlay(userID: userID, view: view, callback: callback)
}
```

[](id:model.step9)
### 手順9：文字チャットおよび弾幕コメントの実装
- `sendRoomTextMsg`によって通常のテキストメッセージを発信できるようになり、該当するルーム内の全てのキャスターおよび視聴者が`onRecvRoomTextMsg`のコールバックを受信することができます。
IMバックエンドは、デフォルトのセンシティブワードフィルタルールを備えており、センシティブワードと認識されたテキストメッセージはクラウドに転送されることはありません。
```swift
// 発信側：テキストメッセージの発信
mLiveRoom.sendRoomTextMsg(message: "Hello Word!", callback: callback)
// 受信側：テキストメッセージの監視
mLiveRoom.delegate = self
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRecvRoomTextMsg message: String, fromUser user: TRTCLiveUserInfo) {
	debugPrint("\(user.userName)から受信したテキストメッセージ:\(message)")
}
```
- `sendRoomCustomMsg`によってカスタマイズ（シグナリング）情報を発信することができます。そのルーム内のすべてのキャスターおよび視聴者は`onRecvRoomCustomMsg`のコールバックを受信することができます。
 カスタムメッセージは、カスタマイズ信号の送信によく用いられます。例えば、「いいね」情報の発信やブロードキャストに使用します。
```swift
// 送信側：カスタマイズしたCmdで弾幕と「いいね！」のメッセージを区別することができます
// eg:「CMD_DANMU」は弾幕コメントを表し、「CMD_LIKE」は「いいね」情報を表します
mLiveRoom.sendRoomCustomMsg(command: "CMD_DANMU", message: "Hello world", callback: nil)
mLiveRoom.sendRoomCustomMsg(command: "CMD_LIKE", message: "", callback: nil)
// 受信側：カスタムメッセージの監視
mLiveRoom.delegate = self
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRecvRoomCustomMsg command: String, message: String, fromUser user: TRTCLiveUserInfo) {
	if "CMD_DANMU" == command {
		// 弾幕コメントの受信
		debugPrint("\(user.userName)から受信した弾幕のメッセージ:\(message)")
	} else if "CMD_LIKE" == command {
		// 「いいね」情報の受信
		debugPrint("\(user.userName)がいいねを付けました")
	}
}
```
