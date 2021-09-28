TWebLiveはTencent CloudのWebライブストリーミングインタラクションコンポーネントです。Tencent Cloud端末R&Dチームによって開発された新しいSDKで、TRTC、IM、およびTCPlayerを統合し、Webライブストリーミングにおけるインタラクティブなシナリオでよく見られる機能（プッシュ、マイクのオン/オフ、カメラのオン/オフ、WeChatの共有視聴、チャットの「いいね！」など）をカバーすると同時に、簡単で使いやすい[API](https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/TWebLive.html)がパッケージされ、アクセスすると素早くWeb端末でプッシュ、プル、およびリアルタイムチャットなどのインタラクティブな機能を実現することができます。[Demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)に参加して体験できます。

## TWebLiveの特長
次の例示説明のとおり、開発者はこの[TWebLive SDK](https://www.npmjs.com/package/tweblive)を使用して、Flashプッシュソリューションと完全に置き換えることができ、Webプッシュ、低遅延Web視聴、CDN視聴、リアルタイムチャットインタラクション（または弾幕）を実現するための複雑さと時間コストを最大限に削減できます。

<dx-tabs>
::: プッシュ
プッシュする必要がある場合は、Pusher（プッシュ）オブジェクトを作成します。最も簡単なプッシュ操作は3ステップのみです。
<dx-codeblock>
::: html html

<div id="pusherView" style="width:100%; height:auto;"></div>
<script>
// 1、Pusher（プッシュ）オブジェクトを作成します
let pusher = TWebLive.createPusher({ userID: 'your userID' });
// 2、レンダリングインターフェースを設定し、マイクで音声を収集し、カメラで映像を収集します（デフォルト720p）
pusher.setRenderView({
  elementID: 'pusherView',
  audio: true,
  video: true
}).then(() => {

// 3、sdkappid roomidなどの情報を入力し、プッシュします
  // urlは `room://` から始まる必要があります
  let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}&livedomainname=${liveDomainName}&streamid=${streamID}`;
  pusher.startPush(url).then(() => {
    console.log('pusher | startPush | ok');
  });
}).catch(error => {
  console.error('pusher | setRenderView | failed', error);
});
</script>
:::
</dx-codeblock>
:::
::: プル
プル再生が必要な場合は、Player（プレーヤー）オブジェクトを作成します。最も簡単なプル操作は3ステップのみです。

<dx-codeblock>
::: html html

<div id="playerView" style="width:100%; height:auto;"></div>
<script>
// 1、Player（プレーヤー）オブジェクトを作成します
let player = TWebLive.createPlayer();

// 2、レンダリングインターフェースを設定します
player.setRenderView({ elementID: 'playerView' });

// 3-1、flvまたはhlsなどのフォーマットのCDN再生アドレスを入力できます。この際のURLは`https://`から始まる必要があります
let url = 'https://'
  + 'flv=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.flv' + '&' // 実際に使用可能な再生アドレスに置き換えてください
  + 'hls=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.m3u8' // 実際に使用可能な再生アドレスに置き換えてください

// 3-2、`room://`から始まるWebRTC再生アドレスを入力できます。このようなアドレスにより、超低遅延の再生を実現できます。
let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}`;
player.startPlay(url).then(() => {
  console.log('player | startPlay | ok');
}).catch((error) => {
  console.error('player | startPlay | failed', error);
});
</script>
:::
</dx-codeblock>
:::
::: チャットルーム
キャスターと視聴者がチャットをインタラクティブにする必要がある場合は、IMオブジェクトを作成します。最も簡単なメッセージの送受信の操作は3ステップのみです。

<dx-codeblock>
::: javascript javascript
// 1、IMオブジェクトを作成し、イベントを監視します
let im = TWebLive.createIM({
  SDKAppID: 0 // アクセスするときは、0をお客様のIMアプリケーションのSDKAppIDに置き換える必要があります
});
// IM_READY IM_TEXT_MESSAGE_RECEIVEDなどのイベントを監視します
let onIMReady = function(event) {
  im.sendTextMessage({ roomID: 'your roomID', text: 'hello from TWebLive' });
};
let onTextMessageReceived = function(event) {
  event.data.forEach(function(message) {
    console.log((message.from || message.nick) + ' : ', message.payload.text);
  });
};
// アクセス側でこのイベントを監視すると、SDKを呼び出してメッセージなどを送信できます
im.on(TWebLive.EVENT.IM_READY, onIMReady);
// テキストメッセージを受信し、画面に移動します
im.on(TWebLive.EVENT.IM_TEXT_MESSAGE_RECEIVED, onTextMessageReceived);

// 2、IMサービスにログインします
im.login({userID: 'your userID', userSig: 'your userSig'}).then((imResponse) => {
  console.log(imResponse.data); // ログイン成功
  if (imResponse.data.repeatLogin === true) {
    // アカウントがログイン済みであり、現在のログインが繰り返しのログインであることを示します
    console.log(imResponse.data.errorInfo);
  }
}).catch((imError) => {
  console.warn('im | login | failed', imError); // ログイン失敗の関連情報
});

// 3、ライブストリーミングルームに入室
im.enterRoom('your roomID').then((imResponse) => {
  switch (imResponse.data.status) {
    case TWebLive.TYPES.ENTER_ROOM_SUCCESS: // ライブストリーミングルームへの入室に成功
      break;
    case TWebLive.TYPES.ALREADY_IN_ROOM: //ライブストリーミングルームに入室済み
      break;
    default:
      break;
  }
}).catch((imError) => {
  console.warn('im | enterRoom | failed', imError); // ライブストリーミングルーム入室失敗の関連情報
});
:::
</dx-codeblock>
:::
</dx-tabs>

開発者の開発コストと人件費を削減するため、TWebLive SDKをベースに、PCとモバイルブラウザの両方に適合するオープンソースの[Demo](https://github.com/tencentyun/TWebLive)をGithubで提供しています。開発者はプロジェクトをfork&cloneしてローカルデバイスに複製し、若干の変更を加えてDemoを実行できます。また、Demoを自身のプロジェクトに統合してデプロイや起動することができます。

## 操作手順
### 手順1：アプリケーションの作成
<dx-tabs>
::: TRTCの場合
[TRTCコンソール](https://console.cloud.tencent.com/trtc/app)にログインし、左側ナビゲーションバーで【アプリケーション管理】>【アプリケーションの新規作成】をクリックしてアプリケーション名を入力し、【確定】をクリックするとTRTCアプリケーションが作成されます。作成が完了してから、SDKAPPIDを保存してください。
![](https://main.qcloudimg.com/raw/871c535f4b539ad7791f10d57ef0a9f3.png)

>?同時に、同じSDKAppIDを持つIMアプリケーションが自動的に作成されます。
:::
::: IMの場合
1. [IMコンソール](https://console.cloud.tencent.com/im)にログインし、【新規アプリケーションを作成する】をクリックするとダイアログボックスがポップアップ表示されます。
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
2. 自分のアプリケーション名を入力して、【OK】をクリックすると作成が完了します。
![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
3. [IMコンソール](https://console.cloud.tencent.com/im)の概要画面で、新規作成したアプリケーションのステータス、サービスバージョン、SDKAppID、作成時間、有効期限を確認することができます。SDKAppID情報を記録してください。
:::
</dx-tabs>

### 手順2：サービスのアクティブ化とキーの取得
<dx-tabs>
::: TRTCの場合
1. [TRTCコンソール](https://console.cloud.tencent.com/trtc/app)にログインし、左側ナビゲーションバーで【アプリケーション管理】をクリックします。「操作」列の【機能設定】をクリックしてアプリケーションの詳細ページに入ります。
![](https://main.qcloudimg.com/raw/bafd4eae90bd282b4f82421172d67e39.png)
2. 【Relayed Pushを有効にする】をクリックして、Relayed Push方式でGlobal Auto-relayを選択します。Relayed Pushの起動後、TRTCルーム内の各チャネル画面に対し対応する再生アドレスが割り当てられます。
![](https://main.qcloudimg.com/raw/a153540779d95dff8a9b381b3566b36e.png)
>?CDNライブストリーミングが必要ない場合、Relayed Pushを起動する手順を省略することができます。
3. 【クイックスタート】をクリックすると、キー情報を表示することができます。キーは保存してください。[](id:step2)
![](https://main.qcloudimg.com/raw/8ec16ab9cab85e324a347dea511f7e4e.png)
4. [CSSコンソール](https://console.cloud.tencent.com/live/)で再生ドメイン名を設定し、CNAME設定を完了します。詳細な操作手順については、[CDN Relayed Live Streamingの実装](https://intl.cloud.tencent.com/document/product/647/35242)ドキュメントをご参照ください。
>?CDNライブストリーミングが必要ない場合、再生ドメイン名を設定する手順を省略することができます。
:::
::: IMの場合
1. [IMコンソール](https://console.cloud.tencent.com/im) の概要ページで、作成したIMアプリケーションをクリックして、直ちにそのアプリケーションの基本構成ページにリダイレクトします。【基本情報】領域で、【キーを表示する】をクリックして、キー情報をコピーし保存します。
![](https://main.qcloudimg.com/raw/610dee5720e94e324a48b44f4728816a.png)
  >!キー情報を適切に保管して、漏えいしないようにしてください。
2. そのアプリケーションの基本構成ページで、TRTCサービスをアクティブ化します。
![](https://main.qcloudimg.com/raw/8fb2940618dfb8b7ea06eecd62212468.png)
:::
</dx-tabs>

### 手順3：Demoのダウンロードと設定
1. [TWebLiveライブストリーミングインタラクションコンポーネントのDemoプロジェクト](https://github.com/tencentyun/TWebLive)をダウンロードします。
2. `TWebLive/dist/debug/GenerateTestUserSig.js` ファイルを開き、関連パラメータを設定します。
 - SDKAPPID：[手順1](#step1)で取得した実際のアプリケーションSDKAppIDを設定してください。
 - SECRETKEY：[手順2](#step2)で取得した実際のキー情報に設定してください。
 - PUSHDOMAIN：CDNライブストリーミングの場合、再生プッシュドメイン名を設定します。（CDNライブストリーミングが必要ない場合は、この設定を無視してかまいません。）
3. プロジェクトでnpmを介して最新版のtim-js-sdk、trtc-js-sdk、twebliveをインストールします。プロジェクトにtim-js-sdkまたはtrtc-js-sdkが統合済みの場合は、直接最新版にアップグレードしてください。
<dx-codeblock>
::: 1 javascript
npm install tim-js-sdk --save
npm install trtc-js-sdk --save
npm install tweblive --save
:::
</dx-codeblock>
4. プロジェクトにTWebLiveをインポートします。
<dx-codeblock>
::: 1 javascript
import TWebLive from 'tweblive'
Vue.prototype.TWebLive = TWebLive
:::
</dx-codeblock>
5. scriptタグの外部リンクを介してインポートする必要がある場合は、 tim-js.js、trtc.js、tweblive.js をプロジェクトにコピーし、それらを順番にインポートする必要があります。
<dx-codeblock>
::: 1 javascript
<script src="./trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tweblive.js"></script>
:::
</dx-codeblock>

>!
>- ローカルで UserSigを計算する方式は、ローカルでの開発デバッグにのみ使用し、オンライン上に直接リリースしないでください。一度 `SECRETKEY`が漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。
>- 正しい UserSigの発行方法は、 UserSig の計算コードをお客様のサーバーに統合して、App向けのインタフェースを用意し、UserSig を必要とするときは、App から業務サーバーにリクエストを出して、ダイナミックUserSigを取得することです。より詳細な内容については、 [サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

### 手順4：Demoの動作
Chrome ブラウザを使用して `dist` ディレクトリの下の `index.html`のファイルを開けば、Demoが動作します。
>!
>
>- 通常の場合、体験 Demo はサーバーにデプロイする必要があり、`https://ドメイン名/xxx`経由でアクセスするか、または直接ローカルにサーバーを構築して、 `localhost:ポート`経由でアクセスします。
- 現在デスクトップ版Chrome ブラウザでは、TRTC デスクトップブラウザ SDKの関連機能がかなり完全にサポートされています。よってChrome ブラウザを使用して体験することをお勧めします。
>- TWebLiveは、カメラとマイクを使用して、オーディオとビデオをキャプチャする必要があります。体験中、Chromeブラウザから関連プロンプトが表示されることがありますが、その場合は【許可】をクリックします。


## アーキテクチャとプラットフォームのサポート

### TWebLiveアーキテクチャ
TWebLiveアーキテクチャの設計は下図に示すとおりです。
![](https://main.qcloudimg.com/raw/ab2b13a441da8b0631cc664f95ad18db.png)
Webプッシュおよび低遅延Web視聴はWebRTC技術を用います。

- WeChatおよびスマホQQミニプラグロムはいずれもサポートされており、モバイル端末ではミニプログラムソリューションの使用をお勧めします。プラットフォームのNative技術の実現により、オーディオビデオの性能も向上し、かつ主なスマホブランドに対し、適切な対応を行っています。
- お客様のユースケースが主に教育シーンである場合、教師用端末はより安定性の高い[Electron](https://intl.cloud.tencent.com/document/product/647/35097)ソリューションを使用することをお勧めします。このソリューションは、大小のデュアルチャネル画面、より柔軟性の高い画面共有ソリューションおよび脆弱なネットワークに対する高い回復力をサポートしています。
>?WebRTCのテクノロジーはGoogleが初めて提唱し、現在、デスクトップ版Chromeブラウザ、デスクトップ版Edgeブラウザ、デスクトップ版Firefoxブラウザ、デスクトップ版Safariブラウザおよびモバイル版Safariブラウザでは比較的万全なサポートが提供されています。その他のプラットフォーム（Androidプラットフォームブラウザなど）のサポート状況は未だ不十分です。

### TWebLiveプラットフォームのサポート

|  OS   |          ブラウザタイプ          | ブラウザの最小バージョン要件 | 受信（再生） | 送信（マイク・オン） |
| :---------: | :--------------------------: | :----------------: | :----------: | :----------: |
|   Mac OS    |    デスクトップ版Safariブラウザ     |        11+         |     サポート     |     サポート     |
|   Mac OS    |     デスクトップ版Chromeブラウザ     |        56+         |     サポート     |     サポート     |
|   Mac OS    |    デスクトップ版Firefoxブラウザ     |        56+         |     サポート     |     サポート     |
|   Mac OS    |      デスクトップ版Edgeブラウザ      |        80+         |     サポート     |     サポート     |
|   Windows   |     デスクトップ版Chromeブラウザ     |        56+         |     サポート     |     サポート     |
|   Windows   | デスクトップ版QQブラウザ（クイックコア） |       10.4+        |     サポート     |     サポート     |
|   Windows   |    デスクトップ版Firefoxブラウザ     |        56+         |     サポート     |     サポート     |
|   Windows   |     デスクトップ版Edgeブラウザ      |        80+         |     サポート     |     サポート     |
| iOS 11.1.2+ |     モバイル版Safariブラウザ     |        11+         |     サポート     |     サポート     |
| iOS 12.1.4+ |         WeChat埋込みウェブページ         |         -          |     サポート     |    未サポート    |
|   Android   |       モバイル版 QQ ブラウザ       |         -          |    サポートなし    |    サポートなし    |
|   Android   |       モバイル版UCブラウザ       |         -          |    サポートなし    |    サポートなし    |
|   Android   |  WeChat Embedded Webページ（TBSコア）   |         -          |     サポート     |     サポート     |
|   Android   |  WeChat Embedded Webページ（XWEBコア）   |         -          |     サポート     |    サポートなし    |

>! H.264著作権の制限によって、HuaweiシステムのChromeブラウザおよびChrome WebViewをコアとするブラウザでは、TRTCデスクトップブラウザSDKの正常動作をサポートしていません。
[](id:sos)
## 注意事項

- アカウントと認証を再利用するためには、TRTCアプリケーションとIMアプリケーションのSDKAppIDが一致している必要があります。
- UserSigをローカルで計算する方式は、ローカルでの開発とデバッグのみに使用されます。SECRETKEYが漏洩すると、攻撃者がTencent Cloudトラフィックを盗用する可能性があるので、オンラインで直接発行しないでください。UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出しダイナミックUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

## よくあるご質問
<dx-accordion>
::: 1.\sキーをクエリーするとき、パブリックキーおよびプライベートキーの情報しか取得できませんが、キーはどうしたら取得できますか。
2019年8月より前に作成したTRTCおよびIMアプリケーション（SDKAppID）では、デフォルトでパブリックキーおよびプライベートキーを区別するECDSA-SHA256署名アルゴリズムを使用しています。HMAC-SHA256署名アルゴリズムにアップグレードしてキーを使用することを強くお勧めします。

- IMのアップグレード方法については、[基本設定](https://intl.cloud.tencent.com/document/product/1047/34540)をご参照ください。
- TRTCのアップグレード方法については、[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。
:::
::: 2.\sクライアントエラーの発生：「RtcError:\sno\svalid\sice\scandidate\sfound」の対処法。
このエラーが発生した場合、TRTCデスクトップブラウザSDKがSTUNトンネリングに失敗したことを意味しますので、環境要件に応じてファイアウォールの設定を確認してください。設定を完了すると、公式サイトの[Demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)にアクセスして体験し、設定が有効かどうかを検査することができます。
- TCPポート：8687
- UDPポート：8000、8080、8800、843、443、16285
- ドメイン名：qcloud.rtc.qq.com
:::
::: 3.\sクライアントエラーの発生：「RtcError:\sICE/DTLS\sTransport\sconnection\sfailed」または\s「RtcError:\sDTLS\sTransport\sconnection\stimeout」の対処法。
このエラーが発生した場合、TRTCデスクトップブラウザSDKがSTUNトンネリングに失敗したことを意味しますので、環境要件に応じてファイアウォールの設定を確認してください。設定を完了すると、公式サイトの[Demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)にアクセスして体験し、設定が有効かどうかを検査することができます。
- TCPポート：8687
- UDPポート：8000、8080、8800、843、443、16285
- ドメイン名：qcloud.rtc.qq.com
:::
::: 4.\s10006\serror\sが発生したときの対処方法は？
 `"Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it"`というエラーが出現した場合は、[TRTCコンソール](https://console.cloud.tencent.com/rav)にログインし、作成したアプリケーションをクリックして、【アカウント情報】をクリックし、アカウント情報パネルでお客様のTRTCアプリケーションのサービスが使用可能な状態かを確認してください。
![](https://main.qcloudimg.com/raw/13c9b520ea333804cffb4e2c4273fced.png)
:::
::: 5.\sWebRTC\s低遅延再生で、iOS\sはプル再生できませんか。
1. TWebLive SDKを1.2.0にアップグレードします。
2. player.startPlay() メソッドを呼び出した後、ブラウザが自動再生を許可しない PLAYER_AUTOPLAY_NOT_ALLOWEDを監視します。
3. 自動再生できないことを確認すると、再生ボタンが表示されます。再生ボタンをクリックすると[resumePlay()](https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/Player.html#resumePlay)メソッドが呼び出され、再生が再開します。
>?iOSは自動再生が制限されます。[制限された自動再生の処理に関するアドバイス](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-21-advanced-auto-play-policy.html)をご参照ください。
:::
</dx-accordion>

## 結び

ここでは、Tencent Cloudの新しいWebライブストリーミングインタラクションコンポーネントであるTWebLiveを紹介しました。このSDKによって、開発者は迅速かつ簡単にWebプッシュ、低遅延Web視聴、CDNライブストリーミングおよびリアルタイムチャットインタラクション（または弾幕）などの機能を実装でき、従来のFlashプッシュソリューションとの置き換えが充分に可能です。

また詳細なアクセスソリューションと[オンラインDemo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)を提供しています。現在、TWebLiveは主流のデスクトップブラウザで良好に機能し、モバイルではミニプログラムのソリューションをサポートしています。

将来的には、プッシュ側での画面共有、画像メッセージのインタラクション、視聴者の複数のラインによる視聴（WebRTC低遅延回線とCDN回線）、キャスターと視聴者のマイク接続によるインタラクションなどの機能のサポートなど、より全方位的なライブストリーミング機能サービスを提供する予定です。

参考資料：

- [TWebLiveインターフェースマニュアル](https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/TWebLive.html)
- [Demo体験](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)
