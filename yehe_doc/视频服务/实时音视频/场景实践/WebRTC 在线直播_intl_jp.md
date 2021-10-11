## TWebLiveの概要

TWebLiveはTencent CloudのWebライブストリーミングインタラクションコンポーネントです。Tencent Cloud端末R&Dチームによって開発された新しいSDKで、Tencent CloudのTRTC、IM、およびSuper Player TCPlayerを統合し、Webライブストリーミングにおけるインタラクティブなシナリオでよく見られる機能（プッシュ、マイクのオン/オフ、カメラのオン/オフ、WeChatの共有視聴、チャットの「いいね！」など）をカバーすると同時に、簡単で使いやすい[API](https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/TWebLive.html)がパッケージされ、アクセスすると素早くWeb端末でプッシュ、プル、およびリアルタイムチャットなどのインタラクティブな機能を実現することができます。[Demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)に参加して体験できます。




## TWebLiveの特徴

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

// 3、再生CDNストリームをプルするためのflv、hlsアドレスなどの情報を入力します。この時のurlは `https://` から始まる必要があります
// またはsdkappid、roomidなどの情報を入力し、WebRTC低遅延ストリームをプルして再生します。この時のurlは `room://` から始まる必要があります
let url = 'https://'
  + 'flv=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.flv' + '&' // 実際に使用可能な再生アドレスに置き換えてください
  + 'hls=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.m3u8' // 実際に使用可能な再生アドレスに置き換えてください

// let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}`;
player.startPlay(url).then(() => {
  console.log('player | startPlay | ok');
}).catch((error) => {
  console.error('player | startPlay | failed', error);
});
</script>
:::
</dx-codeblock>
:::
::: インタラクティブなライブストリーミング
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

// 2、ログイン
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
    case TWebLive.TYPES.ALREADY_IN_ROOM: // ライブストリーミングルームに入室済み
      break;
    default:
      break;
  }
}).catch((imError) => {
  console.warn('im | enterRoom | failed', imError); // ライブストリーミングルーム入室失敗の関連情報
});
</script>
:::
</dx-codeblock>
:::
</dx-tabs>

開発者の開発コストと人件費を削減するため、TWebLive SDKをベースに、PCとモバイルブラウザの両方に適合するオープンソースの[Demo](https://github.com/tencentyun/TWebLive)をGithubで提供しています。開発者はプロジェクトをfork&cloneしてローカルデバイスに複製し、若干の変更を加えてDemoを実行できます。また、Demoを自身のプロジェクトに統合してデプロイや起動することができます。



## TWebLiveの使用
### 注意事項
- アカウントと認証を再利用するためには、TRTCアプリケーションとIMアプリケーションのSDKAppIDが一致している必要があります。
- UserSigをローカルで計算する方法は、ローカルの開発とデバッグにのみ使用されます。SECRETKEYが漏えいすると、攻撃者がTencent Cloudトラフィックを盗用する可能性があるので、ネット上にそのまま公開しないでください。UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを送信し、動的にUserSigを取得します。詳細については、[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。


### 操作手順
<dx-tabs>
::: 方法1：TRTCの場合
[](id:step1)
#### 手順1：TRTCアプリケーションの作成
[TRTCコンソール](https://console.cloud.tencent.com/trtc/app)の、左側ナビゲーションバーで【アプリケーション管理】>【アプリケーションの作成】をクリックしてアプリケーション名を入力し、【OK】をクリックするとTRTCアプリケーションが作成されます。作成が完了してから、SDKAPPIDを保存してください。

>?同時に、同じSDKAppIDを持つIMアプリケーションが自動的に作成されます。

#### 手順2：Auto-Relayed Push機能をオンにする
1. [TRTCコンソール](https://console.cloud.tencent.com/trtc/app)の、左側ナビゲーションバーで【アプリケーション管理】をクリックします。作成したTRTCアプリケーション上で、【機能設定】をクリックしてアプリケーション詳細に入ります。
2. 【Relayed Pushの有効化】をクリックして、Relayed Push方式でGlobal Auto-relayを選択します。Relayed Pushの起動後、TRTCルーム内の各チャネル画面に対し対応する再生アドレスが割り当てられます。
>?CDNライブストリーミングの視聴が必要ない場合、Relayed Pushを起動する手順を省略することができます。
3. 【クイックマスター】をクリックすると、キー情報を確認することができます。キーは保存してください。[](id:step2)
![](https://main.qcloudimg.com/raw/99f03c367c43416bd7c7e8c6d6ff5002.png)
4. [Tencent Cloud CSSコンソール](https://console.cloud.tencent.com/live/)で再生ドメイン名を設定し、CNAME設定を完了します。詳細な操作手順については、[CDN relayed live streamingの実装](https://intl.cloud.tencent.com/document/product/647/35242)ドキュメントをご参照ください。

>?CDNライブストリーミングの視聴が必要ない場合、再生ドメイン名を設定する手順を省略することができます。

### 手順3：Demoのダウンロードおよび設定

1. [Tencent Cloud TWebLiveライブストリーミングインタラクションコンポーネントのDemoプロジェクト]をダウンロードします(https://github.com/tencentyun/TWebLive)。
2.`TWebLive/dist/debug/GenerateTestUserSig.js`ファイルを開き、関連パラメータを設定します。
 - SDKAPPID：[手順1](#step1)で取得した実際のアプリケーションSDKAppIDを設定してください。
 - SECRETKEY：[手順2](#step2)で取得した実際のキー情報に設定してください。
 - PUSHDOMAIN：CDN視聴の場合、再生プッシュドメイン名を設定します。（CDNライブストリーミングの視聴が必要ない場合は、この設定を無視してかまいません。）
3. プロジェクトでnpmを介して最新版のtim-js-sdk、trtc-js-sdk、twebliveをインストールします。プロジェクトにtim-js-sdkまたはtrtc-js-sdkが統合済みの場合は、直接最新版にアップグレードしてください。
```javascript
npm install tim-js-sdk --save
npm install trtc-js-sdk --save
npm install tweblive --save
```
4. プロジェクトにTWebLiveをインポートします。
```javascript
import TWebLive from 'tweblive'
Vue.prototype.TWebLive = TWebLive
```
5. scriptタグの外部リンクを介してインポートする必要がある場合は、tim-js.js、trtc.js、tweblive.jsをプロジェクトにコピーし、それらを順番にインポートする必要があります。
```javascript
<script src="./trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tweblive.js"></script>
```
>!
>- UserSigをローカルで計算する方法は、ローカルの開発とデバッグにのみ使用されます。`SECRETKEY`が漏えいすると、攻撃者がTencent Cloudのトラフィックを盗用する可能性があるので、ネット上にそのまま公開しないでください。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

#### 手順4：Demoの実行
Chromeブラウザを使用して `dist`ディレクトリのindex.htmlファイルを開くと、Demoが実行されます。
>!
>- 通常の場合は、体験Demoは、サーバーにデプロイし、`https://ドメイン名/xxx`経由でアクセスするか、または直接ローカルにサーバーを構築して、`localhost:ポート経由で`アクセスする必要があります。
>
>- 現在デスクトップ版Chromeブラウザは、TRTC Web SDK関連機能のサポート状況がかなり整っていますので、Chromeブラウザを使用して体験することをお勧めします。
>
>- TWebLiveは、カメラとマイクを使用して、オーディオとビデオをキャプチャする必要があります。体験中、Chromeブラウザから関連プロンプトが表示されることがありますが、その場合は【許可】をクリックします。
> 
>:::
>::: 方法2：インスタントメッセージ\sIMの場合
#### 手順1：IMアプリケーションの作成
1. [IMコンソール](https://console.cloud.tencent.com/im)にログインし、【新しいアプリケーションの作成】をクリックするとダイアログボックスがポップアップします。
2. 自分のアプリケーション名を入力して、【確定】をクリックすると作成が完了します。
3. [IMコンソール](https://console.cloud.tencent.com/im)の概要画面で、新規作成したアプリケーションのステータス、サービスバージョン、SDKAppID、作成時間、有効期限を確認することができます。SDKAppID情報を記録してください。

#### 手順2：IMキーを取得してTRTC Video Serviceをアクティブにする
1. [IMコンソール](https://console.cloud.tencent.com/im)の概要ページで、自分で作成を完了したIMアプリケーションをクリックして、直ちにそのアプリケーションの基本設定ページにリダイレクトします。【基本情報】領域で、【キーの表示】をクリックして、キー情報をコピーし保存します。
>!キー情報を適切に保管して、漏えいしないようにしてください。
2. そのアプリケーションの基本設定ページで、Tencent Cloud TRTC Video Serviceをアクティブ化します。

### 手順3：Demoのダウンロードおよび設定
1. [Tencent Cloud TWebLiveライブストリーミングインタラクションコンポーネントのDemoプロジェクト]をダウンロードします(https://github.com/tencentyun/TWebLive)。
2.`TWebLive/dist/debug/GenerateTestUserSig.js`ファイルを開き、関連パラメータを設定します。
 - SDKAPPID：[手順1](#step1)で取得した実際のアプリケーションSDKAppIDを設定してください。
 - SECRETKEY：[手順2](#step2)で取得した実際のキー情報に設定してください。
 - PUSHDOMAIN：CDN視聴の場合、再生プッシュドメイン名を設定します。（CDNライブストリーミングの視聴が必要ない場合は、この設定を無視してかまいません。）
3. プロジェクトでnpmを介して最新版のtim-js-sdk、trtc-js-sdk、twebliveをインストールします。プロジェクトにtim-js-sdkまたはtrtc-js-sdkが統合済みの場合は、直接最新版にアップグレードしてください。
```javascript
npm install tim-js-sdk --save
npm install trtc-js-sdk --save
npm install tweblive --save
```
4. プロジェクトにTWebLiveをインポートします。
```javascript
import TWebLive from 'tweblive'
Vue.prototype.TWebLive = TWebLive
```
5. scriptタグの外部リンクを介してインポートする必要がある場合は、tim-js.js、trtc.js、tweblive.jsをプロジェクトにコピーし、それらを順番にインポートする必要があります。
```javascript
<script src="./trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tweblive.js"></script>
```
>!
>- UserSigをローカルで計算する方法は、ローカルの開発とデバッグにのみ使用されます。`SECRETKEY`が漏えいすると、攻撃者がTencent Cloudのトラフィックを盗用する可能性があるので、ネット上にそのまま公開しないでください。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

#### 手順4：Demoの実行
Chromeブラウザを使用して `dist`ディレクトリのindex.htmlファイルを開くと、Demoが実行されます。
>!
>- 通常の場合は、体験Demoは、サーバーにデプロイし、`https://ドメイン名/xxx`経由でアクセスするか、または直接ローカルにサーバーを構築して、`localhost:ポート経由で`アクセスする必要があります。
>- 現在デスクトップ版Chromeブラウザは、TRTC Web SDK関連機能のサポート状況がかなり整っていますので、Chromeブラウザを使用して体験することをお勧めします。
>- TWebLiveは、カメラとマイクを使用して、オーディオとビデオをキャプチャする必要があります。体験中、Chromeブラウザから関連プロンプトが表示されることがありますが、その場合は【許可】をクリックします。
>  
:::
</dx-tabs>

## アーキテクチャとプラットフォームのサポート

### TWebLiveアーキテクチャ

TWebLiveアーキテクチャの設計は下図に示すとおりです。
![](https://main.qcloudimg.com/raw/5d28f48be5c82c929acf46b05e02ebeb.png)
Webプッシュおよび低遅延Web視聴はWebRTC技術を用います。

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
| iOS 12.1.4+ |         WeChat Embedded Webページ          |         -          |     サポート     |    サポートなし    |
| iOS 14.3+   |        WeChat Embedded Webページ        |   6.5+（WeChatバージョン） |     サポート     |    サポート     |
|   Android   |       モバイル版QQブラウザ       |         -          |    サポートなし    |    サポートなし    |
|   Android   |       モバイル版UCブラウザ       |         -          |    サポートなし    |    サポートなし    |
|   Android   |  WeChat Embedded Webページ（TBSコア）   |         -          |     サポート     |     サポート     |
|   Android   |  WeChat Embedded Webページ（XWEBコア）   |         -          |     サポート     |    サポートなし    |

>! H.264の版権の制限により、HuaweiシステムのChromeブラウザおよびChrome WebViewをコアとするブラウザではTRTC Web SDKの正常な動作をサポートしていません。
>[](id:sos)



## よくあるご質問
<dx-accordion>
キーをクエリーするとき、公開鍵および秘密鍵の情報しか取得できませんが、キーはどうしたら取得できますか。
2019年8月より前に作成したTRTCおよびIMアプリケーション（SDKAppID）では、デフォルトで公開鍵と秘密鍵を区別するECDSA-SHA256署名アルゴリズムを使用しています。HMAC-SHA256署名アルゴリズムにアップグレードしてキーを使用することを強くお勧めします。
- TRTCのアップグレード方法については、[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。
- IMのアップグレード方法については、[基本設定](https://intl.cloud.tencent.com/document/product/1047/34540)をご参照ください。
:::
::: クライアントエラーの発生：「RtcError:\sno\svalid\sice\scandidate\sfound」にはどう対処すればよいでしょうか。
このエラーが発生したときは、TRTC Web SDKがSTUNトンネリングに失敗したことを意味しますので、環境要件にしたがってファイアウォール設定をチェックしてください。設定が完了した後、公式サイトの[Demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)にアクセスして体験し、設定が有効かどうかを検査することができます。
  - TCPポート：8687
  - UDPポート：8000、8080、8800、843、443、16285
  - ドメイン名：qcloud.rtc.qq.com
:::
::: クライアントエラーの発生：「RtcError:ICE/DTLS\sTransport\sconnection\sfailed」または「RtcError:DTLS\sTransport\sconnection\stimeout」にはどう対処すればよいでしょうか。
このエラーが発生したときは、TRTC Web SDKがSTUNトンネリングに失敗したことを意味しますので、環境要件にしたがってファイアウォール設定をチェックしてください。設定が完了した後、公式サイトの[Demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)にアクセスして体験し、設定が有効かどうかを検査することができます。
  - TCPポート：8687
  - UDPポート：8000、8080、8800、843、443、16285
  - ドメイン名：qcloud.rtc.qq.com
:::
::: \s10006\serror\sが発生したときはどう対処すればよいでしょうか。
`"Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it"`というエラーが出現した場合は、[TRTCコンソール](https://console.cloud.tencent.com/rav)にログインし、作成したアプリケーションをクリックして、【アカウント情報】をクリックし、アカウント情報パネルでお客様のTRTCアプリケーションのサービスが使用可能な状態かを確認してください。<img src="https://main.qcloudimg.com/raw/33bd04fe44f1a9b4163709f3c513643c.png">
:::
::: WebRTC\s低遅延再生で、iOS\sはプル再生できませんか。
1. TWebLive SDKを1.2.0にアップグレードします。
2. `player.startPlay()`メソッドを呼び出した後、ブラウザが自動再生を許可しない`PLAYER_AUTOPLAY_NOT_ALLOWED`を監視します。
3. 自動再生できないことを確認すると、再生ボタンが表示されます。再生ボタンを再びクリックすると[resumePlay()](https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/Player.html#resumePlay)メソッドが呼び出され、再生が再開します。
iOSは自動再生が制限されます。[制限された自動再生の処理に関するアドバイス](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-21-advanced-auto-play-policy.html)をご参照ください。
:::
</dx-accordion>



## 結び
ここでは、Tencent Cloudの新しいWebライブストリーミングインタラクションコンポーネントであるTWebLiveを紹介しました。このSDKによって、開発者は迅速かつ簡単にWebプッシュ、低遅延Web視聴、CDN視聴およびリアルタイムチャットインタラクション（または弾幕）などの機能を実装でき、従来のFlashプッシュソリューションとの置き換えが充分に可能です。

また、詳細なアクセス方法と[オンラインDemo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)体験も提供しています。現在、TWebLiveは主流のWeb上でのサポートもかなり良好です。

将来的には、プッシュ側での画面共有、画像メッセージのインタラクション、視聴者の複数のラインによる視聴（WebRTC低遅延回線とCDN回線）、キャスターと視聴者のマイク接続によるインタラクションといった機能のサポートなど、よりオールラウンドなライブストリーミング機能サービスを提供する予定です。

参考資料：

- <a href="https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/TWebLive.html">TWebLiveインターフェースマニュアル</a>
- [オンラインDemo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)


