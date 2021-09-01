## デモンストレーション

このドキュメントでは、プッシュストリーム、プルストリーム、チャットルーム、インタラクティブマイク接続などのオンラインライブストリーミング機能を、Webブラウザだけで素早く実装する方法を説明します。

## 実装の原理

[**TWebLive**](https://intl.cloud.tencent.com)はTencent CloudがTRTC、IM、CDNなどのサービスに基づいて構築したWeb端末ライブストリーミングコンポーネントです。簡単なコードで、以下のようなプッシュストリーム、プルストリーム、チャットルームの機能を実装することができます。

### プッシュ
プッシュする必要がある場合は、Pusher（プッシュ）オブジェクトを作成します。最も簡単なプッシュ操作は3ステップのみです。
```
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

// 3、 sdkappid roomid等の情報を入力し、プッシュします
  // urlは`room://`から始まる必要があります
  let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}&livedomainname=${liveDomainName}&streamid=${streamID}`;
  pusher.startPush(url).then(() => {
    console.log('pusher | startPush | ok');
  });
}).catch(error => {
  console.error('pusher | setRenderView | failed', error);
});
</script>
```
### プルストリーム
プルストリーム再生が必要な場合は、Player（プレーヤー）オブジェクトを作成します。最も簡単なプル操作は3ステップのみです。

```
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
```
### チャットルーム
キャスターと視聴者がチャットをインタラクティブにする必要がある場合は、IMオブジェクトを作成します。最も簡単なメッセージの送受信の操作は3ステップのみです。

```
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
    case TWebLive.TYPES.ALREADY_IN_ROOM: // ライブストリーミングルームに入室済み
      break;
    default:
      break;
  }
}).catch((imError) => {
  console.warn('im | enterRoom | failed', imError); // ライブストリーミングルーム入室失敗の関連情報
});
```

>? 開発者の開発コストと人件費を削減するため、TWebLive SDKをベースに、PCとモバイルブラウザの両方に適合するオープンソースの[Demo](https://github.com/tencentyun/TWebLive)をGithubで提供しています。開発者はプロジェクトをfork&cloneしてローカルデバイスに複製し、若干の変更を加えてDemoを実行できます。また、Demoを自身のプロジェクトに統合してデプロイや起動することができます。

## アクセスのヒント

<span id="step1"></span>
### 手順1：アプリケーションの作成
まず、TRTCコンソールでTRTCアプリケーションを作成する必要があります。Tencent Cloudは、デフォルトでTRTCアプリケーションに、同じSDKAppIDを持つIMアプリケーションを関連付けます。

1. [TRTCコンソール](https://console.cloud.tencent.com/trtc)にログインします。
2. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】に進み、【アプリケーションの作成】をクリックしてアプリケーション名を入力し、【OK】をクリックして、TRTCアプリケーションを作成します。

<span id="step2"></span>
### 手順2：SDKAppIDとキーの取得
1. [アプリケーションリスト](https://console.cloud.tencent.com/trtc/app) の中で、ターゲットのアプリケーションを選択し、右側の【アプリケーション情報】をクリックして詳細画面に入ります。
2. 【アプリケーション情報】モジュールを確認し、コピーボタンをクリックし、SDKAppIDの情報を記録します。
![](https://main.qcloudimg.com/raw/a65b6631553159ce553620e40f9c2040.png)
3.【クイックマスター】タブを選択し、【ステップ2 UserSigを発行するためのキーを取得】タグを表示し、【キーのコピー】をクリックします。
    ![](https://main.qcloudimg.com/raw/99f03c367c43416bd7c7e8c6d6ff5002.png)

>!
>- UserSigのローカル計算方法は、ローカル開発とデバッグにのみ使用されます。ネット上にそのまま公開しないでください。 `SECRETKEY`が漏えいすると、攻撃者がTencent Cloudのトラフィックを盗用する可能性があります。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

<span id="step3"></span>
### 手順3：CDNライブストリーミングサービスの開始（オプション）
CDNライブストリーミングプルストリーム機能を有効化する場合は、Tencent Cloud CSSサービスを開始する必要があります。以下の手順で開始することができます。
1. 【アプリケーション管理】>【機能設定】の中の[Auto Relayed Pushを有効にする](https://intl.cloud.tencent.com/document/product/647/39080)にします。Relayed Push機能を有効にすると、TRTCルーム内の各チャンネル画面に、対応する再生アドレスが配布されます。
2. [Tencent Cloud CSSコンソール](https://console.cloud.tencent.com/live/) で再生ドメイン名を設定し、CNAME設定を完了します。詳細な操作手順については、[CDN relayed live streamingの実装](https://intl.cloud.tencent.com/document/product/647/35242) ドキュメントをご参照ください。


<span id="step4"></span>

### 手順4： Demoソースコードのダウンロードおよび設定
1. [Tencent Cloud TWebLIVEコンポーネントのDemoプロジェクト]をダウンロードします(https://github.com/tencentyun/TWebLive)。
2. `TWebLive/dist/debug/GenerateTestUserSig.js`ファイルを開き、関連パラメータを設定します：<ul style="margin:0">
   <li/>SDKAPPID：<a href="#step2">手順1</a>の中で取得した実際のアプリケーションSDKAppIDを設定してください。
    <li/>SECRETKEY：<a href="#step2">手順2</a>の中で取得した実際のキー情報を設定してください。
    <li/>PLAYDOMAIN：CDN視聴の場合、再生ドメイン名を設定します。（CDN relayed live streamingが必要ない場合は、この設定を無視してかまいません。）
    </ul>
3. Demoソースコードの統合：
#### npmパッケージによるインストール
1. プロジェクトでnpmを介して最新版の `tim-js-sdk`、`trtc-js-sdk`、`tweblive`をインストールします。
```javascript
npm install tim-js-sdk --save
npm install trtc-js-sdk --save
npm install tweblive --save
```
>? プロジェクトに`tim-js-sdk`または`trtc-js-sdk`がすでに統合されている場合は、直接、最新版にアップグレードしてください。
2. プロジェクトにTWebLiveをインポートします。
```javascript
import TWebLive from 'tweblive'
Vue.prototype.TWebLive = TWebLive
```

#### scriptタグによる外部リンク
外部チェーンのスクリプトタグを介してインポートする必要がある場合は、`tim-js.js`、`trtc.js`、`tweblive.js`をプロジェクトにコピーし、それらを順番にインポートする必要があります。
```
<script src="./trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tweblive.js"></script>
```

<span id="step5"></span>

### 手順5：Demoの実行

Chromeブラウザを使用して `dist`ディレクトリのindex.htmlファイルを開くと、Demoが実行されます。

>!
>
>- 通常の場合は、体験Demoは、サーバーにデプロイし、`https://ドメイン名/xxx`経由でアクセスするか、または直接ローカルにサーバーを構築して、`localhost:ポート経由で`アクセスする必要があります。
>- 現在、デスクトップのChromeブラウザはTRTCデスクトップブラウザSDKをサポートしており、関連特性は比較的万全です。従って、Chromeブラウザを使用して体験することをお勧めします。
>- TWebLiveは、カメラとマイクを使用して、オーディオとビデオを収集する必要があります。体験中、Chromeブラウザから関連プロンプトが表示されることがありますが、その場合、【許可】をクリックします。

### サポートプラットフォーム

WebプッシュとWeb低遅延視聴にはWebRTC技術が使われています。WebRTCのテクノロジーはGoogleが初めて提唱し、現在、デスクトップ版Chromeブラウザ、デスクトップ版Edgeブラウザ、デスクトップ版Firefoxブラウザ、デスクトップ版Safariブラウザ及びモバイル版Safariブラウザでは比較的万全なサポートが提供されています。その他のプラットフォーム（Androidプラットフォームブラウザなど）のサポート状況は未だ不十分です。

- お客様のユースケースが主に教育シーンである場合、教師用端末はより安定性の高い[Electron](https://intl.cloud.tencent.com/document/product/647/35097) ソリューションを使用することをお勧めします。このソリューションは、大小のデュアルチャネル画面、より柔軟性の高い画面共有ソリューション及び脆弱なネットワークに対する高い回復力をサポートしています。

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

>! H.264版の権限の制限によって、HuaweiシステムのChromeブラウザおよびChrome WebViewをコアとするブラウザでは、TRTCデスクトップブラウザSDKの正常動作をサポートしていません。

## よくあるご質問
**1.キーをクエリーするとき、公開鍵および秘密鍵の情報しか取得できませんが、キーはどうしたら取得できますか。**

TRTC SDK 6.6バージョン（2019年08月）では新しい署名アルゴリズムのHMAC-SHA256の使用を始めています。その前に作成済のアプリケーションは、署名アルゴリズムをアップグレードしないと暗号化したキーを取得できません。

**2.クライアントエラーの発生：“RtcError:no valid ice candidate found”にはどう対処すればよいでしょうか。**

このエラーが発生した場合、TRTCデスクトップブラウザSDKがSTUNトンネリングに失敗したことを意味しますので、環境要件に従ってファイアウォールのコンフィグレーションを確認してください。

**3.クライアントエラーの発生：「RtcError: ICE/DTLS Transport connection failed」または 「RtcError: DTLS Transport connection timeout」にはどう対処すればよいでしょうか。**

このエラーが発生した場合、TRTCデスクトップブラウザSDKがSTUNトンネリングに失敗したことを意味しますので、環境要件に従ってファイアウォールのコンフィグレーションを確認してください。

**4.10006 errorが発生したときはどう対処すればよいでしょうか。**

`「Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it」`というエラーが出現した場合は、[TRTCコンソール](https://console.cloud.tencent.com/rav)にログインし、作成したアプリケーションをクリックして、【アカウント情報】をクリックし、アカウント情報パネルでお客様のTRTCアプリケーションのサービスが使用可能な状態かを確認してください。
![](https://main.qcloudimg.com/raw/33bd04fe44f1a9b4163709f3c513643c.png)

## 参考資料

- [TWebLive API マニュアル](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html)
- [オンラインDemo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)


