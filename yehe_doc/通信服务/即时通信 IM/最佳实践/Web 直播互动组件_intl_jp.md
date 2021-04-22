## 一、TWebLiveの概要

[TWebLive](https://trtc.qcloud.com/tweblive/index.html#/) は、Tencent Cloud Web ILVBコンポーネントです。Tencent Cloud端末R&Dチームによって開発された新しい [SDK](https://www.npmjs.com/package/tweblive)であり、[Tencent Cloud TRTC](https://intl.cloud.tencent.com/product/trtc)、[Tencent Cloud IM](https://intl.cloud.tencent.com/product/im)、Tencent Cloud TCPlayerを統合し、Webライブストリーミングにおけるインタラクティブなシナリオの一般的な機能（プッシュ、マイク・オン/オフ、カメラ・オン/オフ、WeChatの共有と視聴、チャットのいいね！など）をカバーすると同時に、シンプルで使いやすい [API](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html)をカプセル化し、アクセス後、迅速にWebプッシュ、プル、リアルタイムチャットなどのインタラクティブな機能を実現できます。



## 二、TWebLiveの特長

次の例示説明のとおり、開発者はこのSDKを使用して、flashプッシュソリューションと完全に置き換えることができ、Webプッシュ、低遅延Web視聴、CDN視聴、リアルタイムチャットインタラクション（または弾幕）を実現するための複雑さと時間コストを最大限に削減できます。

### 1. プッシュ

プッシュする必要がある場合は、Pusher（プッシュ）オブジェクトを作成します。最も簡単なプッシュ操作は3ステップのみです。

```javascript
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
```

### 2. プル

プル再生が必要な場合は、Player（プレーヤー）オブジェクトを作成します。最も簡単なプル操作は3ステップのみです。

```javascript
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
```

### 3. ILVB

キャスターと視聴者がチャットをインタラクティブにする必要がある場合は、IMオブジェクトを作成します。最も簡単なメッセージの送受信の操作は3ステップのみです。

```javascript
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
```

開発者の開発コストと人件費を削減するため、TWebLive SDKをベースに、PCとモバイルブラウザの両方に適合するオープンソースの[Demo](https://github.com/tencentyun/TWebLive)をGithubで提供しています。開発者はプロジェクトをfork&cloneしてローカルデバイスに複製し、若干の変更を加えてDemoを実行できます。また、Demoを自身のプロジェクトに統合してデプロイや起動することができます。

## 三、アクセスと使用


 [Tencent Cloud TRTCコンソール](https://console.cloud.tencent.com/trtc/app) でTRTCアプリケーションを作成し `SDKAPPID` を保存します（同時に、同じ `SDKAppID` を持つIMアプリケーションが自動作成されます）。その後、【アプリケーション管理】>【機能設定】でAuto-Relayed Pushを有効にします。Auto-Relayed Push機能を有効にすると、TRTCルームの各画面に対応する再生アドレスが配置されます（CDN relayed live streamingの視聴が不要である場合は、Relayed Pushを有効にする手順をスキップできます）。

 [Tencent Cloud LVBコンソール](https://console.cloud.tencent.com/live/) で再生ドメイン名を設定し、CNAME設定を完了します。詳細な操作手順については、[CDN relayed live streamingの実装](https://intl.cloud.tencent.com/document/product/647/35242) ドキュメントをご参照ください（CDN relayed live streamingの視聴が不要である場合は、この手順をスキップできます）。

npmを介してTWebLiveをダウンロードします。
```javascript
npm i tweblive --save
```

## 四、アーキテクチャとプラットフォームのサポート

TWebLiveアーキテクチャの設計は下図に示すとおりです。
![](https://main.qcloudimg.com/raw/ab2b13a441da8b0631cc664f95ad18db.png)
Webプッシュと低遅延Web視聴には、WebRTC 技術が使用されています。現在主なデスクトップ版Chromeブラウザ、デスクトップ版およびモバイル版Safariブラウザで比較的完全なサポートを行っており、その他のプラットフォーム（Androidプラットフォームブラウザなど）では、サポート状況が整っていません。具体的には次のとおりです。

| 操作システム | ブラウザタイプ | ブラウザ最低バージョン要件 | 受信（再生）| 送信（マイク・オン）| 画面共有 |
|:-------:|:-------:|:-------:|:-------:|:-------:| :-------:|
| Mac OS  | デスクトップ版Safariブラウザ |  11+ | サポート | サポート | サポートなし|
| Mac OS  | デスクトップ版 Chromeブラウザ |  56+ | サポート | サポート | サポート（chrome72+ バージョンが必要） |
| Windows  | デスクトップ版Chromeブラウザ|  56+ | サポート | サポート | サポート（chrom72+ バージョンが必要） |
| Windows  | デスクトップ版QQブラウザ |  10.4 | サポート | サポート | サポートなし |
| iOS | モバイル版Safariブラウザ | 11.1.2 | サポート | サポート | サポートなし |
| iOS | WeChat Embedded Webページ　| 12.1.4 | サポート | サポートなし | サポートなし |
| Android | モバイル版QQブラウザ| - | サポートなし | サポートなし | サポートなし |
| Android | モバイル版UCブラウザ| - | サポートなし | サポートなし | サポートなし |
| Android | WeChat Embedded Webページ（TBS コア）| - | サポート | サポート | サポートなし |

モバイルでは [ミニプログラム](https://intl.cloud.tencent.com/document/product/647/35097) ソリューションの使用をお勧めします。ミニプログラムはWeChatとスマートフォンQQのいずれもサポートされ、各プラットフォームのネイティブ技術に基づいてより良いオーディオおよびビデオ性能を提供し、主流のスマートフォンブランドに対応しています。ユースケースが主に教育現場である場合、教師側ではより安定性の高い [Electron](https://intl.cloud.tencent.com/document/product/647/35097) ソリューションの使用をお勧めします。大小デュアル画面、より柔軟な画面共有ソリューション、弱いネットワーク状態でのより強力なのリカバリー機能をサポートします。

## 五、注意事項

- アカウントと認証を再利用するためには、TRTCアプリケーションとIMアプリケーションのSDKAppIDが一致している必要があります。
- IMアプリケーションは、テキストメッセージに対し、ベーシック版のセキュリティ対策機能を提供します。不適切な単語のカスタム機能を使用したい場合は、【アップグレード】をクリックします。
- UserSigをローカルで計算する方式は、ローカルでの開発とデバッグのみに使用されます。SECRETKEYが漏洩すると、攻撃者がTencent Cloudトラフィックを盗用する可能性があるので、オンラインで直接発行しないでください。UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出しダイナミックUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。
- H.264 版の権限の制限によって、HuaweiシステムのChromeブラウザおよびChrome WebViewをコアとするブラウザでは、 TRTCデスクトップ型ブラウザSDKの正常動作をサポートしていません。

## 六、結び

ここでは、Tencent Cloudの新しいWeb ILVBコンポーネントであるTWebLiveを紹介しました。このSDKによって、開発者は迅速かつ簡単にWebプッシュ、低遅延Web視聴、CDN視聴およびリアルタイムチャットインタラクション（または弾幕）などの機能を実装でき、従来のflashプッシュソリューションとの置き換えが充分に可能です。

また詳細なアクセスソリューションと [オンライン Demo](https://trtc.qcloud.com/tweblive/index.html#/) を提供しています。現在、TWebLiveは主流のデスクトップブラウザで良好に機能し、モバイルではミニプログラムのソリューションをサポートしています。

将来的には、プッシュ側での画面共有、画像メッセージの相互作用、視聴者の複数のラインによる視聴（WebRTC低遅延回線とCDN回線）、キャスターと視聴者のマイク接続によるインタラクティブな機能をサポートするなど、より全方位的なライブストリーミング機能サービスを提供する予定です。

参考資料：

- [TWebLive インターフェースマニュアル](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html)
- [TWebLiveクイックスタート](https://intl.cloud.tencent.com/document/product/1047/38174)
