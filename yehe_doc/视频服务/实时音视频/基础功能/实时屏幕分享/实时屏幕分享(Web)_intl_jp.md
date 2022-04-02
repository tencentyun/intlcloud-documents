TRTC Web SDK画面共有のサポートレベルについて、[ブラウザのサポート状況](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html)をご参照ください。また、SDKは[TRTC.isScreenShareSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.isScreenShareSupported)インターフェースを提供し、現在のブラウザが画面共有をサポートしているかどうかを判断します。
このドキュメントでは、以下のような異なるシーンで実装プロセスを説明します。

> !
> - Web端末ではセカンダリストリームの公開が現時点でサポートされていません。画面共有の公開はプライマリストリームの公開によって実現されます。リモート画面共有ストリームがWebユーザーからのものである場合は、[RemoteStream.getType()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getType)は'main'を返し、通常、Web端末からの画面共有ストリームであることはuserIdによって識別されます。
> - Native（iOS、Android、Mac、Windowsなど）端末ではセカンダリストリームの公開をサポートし、画面共有の公開はセカンダリストリームの公開によって実現されます。リモート画面共有ストリームがNativeユーザーからのものである場合は、[RemoteStream.getType()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getType)は'auxiliary'を返します。

## 画面共有ストリームの作成と公開
>!画面共有ストリームを作成および公開するコードは、以下の順序で厳密に実行してください。

### ステップ1：画面共有を行うクライアントオブジェクトの作成
通常、画面共有のクライアントオブジェクトであることを示すために、userIdには`share_`というプレフィックスを付けることをお勧めします。

<dx-codeblock>
:::  javascript
const shareClient = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId, // 例：‘share_teacher’
  userSig
});
// クライアントオブジェクトがルームに参加します
try {
  await shareClient.join({ roomId });
  // ShareClient join room success
} catch (error) {
  // ShareClient join room failed
}

:::
</dx-codeblock>

### ステップ2：画面共有ストリームの作成
画面共有ストリームには、ビデオストリームとオーディオストリームが含まれます。このうち、オーディオストリームは、マイクオーディオまたはシステムオーディオに分けられます。
<dx-codeblock>
:::  javascript
// Goodの正しい使い方
// 画面ビデオストリームのみの収集
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// or マイクオーディオおよび画面ビデオストリームの収集
const shareStream = TRTC.createStream({ audio: true, screen: true, userId });
// or システムオーディオおよび画面ビデオストリームの収集
const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });

// Badの間違った使い方
const shareStream = TRTC.createStream({ camera: true, screen: true });
// or
const shareStream = TRTC.createStream({ camera: true, screenAudio: true });

:::
</dx-codeblock>

>! 
>- audio属性とscreenAudio属性を同時にtrueに設定することはできません。camera属性とscreenAudio属性を同時にtrueに設定することはできません。screenAudioの詳細については、このドキュメントのパート5で説明します。
>- camera属性とscreen属性を同時にtrueに設定することはできません。

### ステップ3：画面共有ストリームの初期化
初期化時にブラウザはユーザーに画面共有の内容と権限を要求します。ユーザーが許可を拒否した場合、またはシステムがブラウザに画面共有の権限を付与しなかった場合は、コードは`NotReadableError`または`NotAllowedError`のエラーをキャッチします。この場合、ユーザーがブラウザ設定またはシステム設定で画面共有の権限をオンにするように指示する必要があります。
<dx-codeblock>
:::  javascript
try {
  await shareStream.initialize();
} catch (error) {
  // 画面共有ストリームの初期化に失敗した場合、ユーザーに警告し、その後の入室公開プロセスを停止します
  switch (error.name) {
    case 'NotReadableError':
      // 現在のブラウザで画面の内容を取得できるようなシステムの確保にユーザーに通知します
      return;
    case 'NotAllowedError':
      if (error.message.includes('Permission denied by system')) {
        // 現在のブラウザで画面の内容を取得できるようなシステムの確保にユーザーに通知します
      }else{
        // ユーザーが画面共有を拒否/キャンセルします
      }
      return;
    default:
      // 画面共有ストリームの初期化中に不明なエラーが発生し、ユーザーにリトライを通知します
      return;
  }
}
:::
</dx-codeblock>

### ステップ4：画面共有ストリームの公開
ステップ1で作成されたクライアントオブジェクトにより公開されます。公開が成功すると、リモート端末で画面共有ストリームを受信できます。
<dx-codeblock>
:::  javascript
try {
  await shareClient.publish(shareStream);
} catch (error) {
  // ShareClient failed to publish local stream
}
:::
</dx-codeblock>

### 完全コード
<dx-codeblock>
:::  javascript
const shareClient = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId, // 例：‘share_teacher’
  userSig
});
// クライアントオブジェクトがルームに参加します
try {
  await shareClient.join({ roomId });
  // ShareClient join room success
} catch (error) {
  // ShareClient join room failed
}
// 画面ビデオストリームのみの収集
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// or マイクオーディオおよび画面ビデオストリームの収集
// const shareStream = TRTC.createStream({ audio: true, screen: true, userId });
// or システムオーディオおよび画面ビデオストリームの収集
// const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });
try {
  await shareStream.initialize();
} catch (error) {
  // 画面共有ストリームの初期化に失敗した場合、ユーザーに警告し、その後の入室公開プロセスを停止します
  switch (error.name) {
    case 'NotReadableError':
      // 現在のブラウザで画面の内容を取得できるようなシステムの確保にユーザーに通知します
      return;
    case 'NotAllowedError':
      if (error.message.includes('Permission denied by system')) {
        // 現在のブラウザで画面の内容を取得できるようなシステムの確保にユーザーに通知します
      }else{
        // ユーザーが画面共有を拒否/キャンセルします
      }
      return;
    default:
      // 画面共有ストリームの初期化中に不明なエラーが発生し、ユーザーにリトライを通知します
      return;
  }
}
try {
  await shareClient.publish(shareStream);
} catch (error) {
  // ShareClient failed to publish local stream
}
:::
</dx-codeblock>

## 画面共有パラメータの設定
設定可能なパラメータには、解像度、フレームレートおよびコードレートがあります。必要に応じて[setScreenProfile()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setScreenProfile)インターフェースを使用してprofileを指定できます。各profileは解像度、フレームレートおよびコードレートのセットに対応しています。SDKはデフォルトで'1080p'の構成を使用します。

<dx-codeblock>
:::  javascript
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// setScreenProfile()はinitialize()の前に呼び出す必要があります。
shareStream.setScreenProfile('1080p');
await shareStream.initialize();
:::
</dx-codeblock>

またはカスタマイズ解像度、フレームレートとビットレートを使用します。

<dx-codeblock>
:::  javascript
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// setScreenProfile()はinitialize()の前に呼び出す必要があります。
shareStream.setScreenProfile({ width: 1920, height: 1080, frameRate: 5, bitrate: 1600 /* kbps */});
await shareStream.initialize();
:::
</dx-codeblock>
画面共有属性推奨リスト：

| profile | 解像度（幅 × 高さ） | フレームレート（fps） | ビットレート (kbps) |
|:--------|:----------------|:----------|:------------|
| 480p    | 640 x 480       | 5         | 900         |
| 480p_2  | 640 x 480       | 30        | 1000        |
| 720p    | 1280 x 720      | 5         | 1200        |
| 720p_2  | 1280 x 720      | 30        | 3000        |
| 1080p   | 1920 x 1080     | 5         | 1600        |
| 1080p_2 | 1920 x 1080     | 30        | 4000        |

>! 想定外の問題の原因となる高すぎるパラメータ設定を避けるために、推奨されるパラメータで設定することをお勧めします。

## 画面共有の停止

<dx-codeblock>
:::  javascript
// 画面共有クライアントによるストリームの公開解除
await shareClient.unpublish(shareStream);
// 画面共有ストリームをオフにする
shareStream.close();
// 画面共有クライアントの退室
await shareClient.leave();

// 上記の3つのステップは必須ではなく、シーンのニーズに応じて必要なコードを実行すればよい。通常は、入室したかどうか、ストリームを開示したかどうかの判断を追加する必要があります。より詳細なコード例については、[demoソースコード](https://github.com/LiteAVSDK/TRTC_Web/blob/main/base-js/js/share-client.js)をご参照ください。
:::
</dx-codeblock>

またユーザーはブラウザに付属のボタンで画面共有を停止することもあるため、画面共有ストリームは画面共有停止イベントを傍受し、それに応じた処理を行う必要があります。


<dx-codeblock>
:::  javascript
// 画面共有ストリームが画面共有停止イベントを傍受します
shareStream.on('screen-sharing-stopped', event => {
  // 画面共有クライアントがプッシュを停止します
  await shareClient.unpublish(shareStream);
  // 画面共有ストリームをオフにする
  shareStream.close();
  // 画面共有クライアントの退室
  await shareClient.leave();
});
:::
</dx-codeblock>

## カメラ動画と画面共有の同時公開
1つのClientでは、最大1チャネルのオーディオと1チャネルのビデオを同時に公開することができます。カメラビデオと画面共有を同時に公開するには、2つのClientを作成して、それらを「それぞれの役割」に任せる必要があります。
例えば、次のように2つのClientを作成します。
- **client**：ローカルのオーディオビデオストリームを公開し、shareClientを除くすべてのリモートストリームをサブスクライブします。
- **shareClient**：画面共有ストリームを公開し、リモートストリームをサブスクライブしません。

>! 
>- 画面共有を行うshareClientは、自動サブスクリプションをオフにする必要があります。そうしないと、リモートストリームの重複サブスクリプションが発生します。[APIの説明](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#createClient)をご参照ください。
>- ローカルのオーディオビデオストリームを公開するclientは、shareClientが公開するストリームのサブスクリプションを取り消す必要があります。そうしないと自分で自分をサブスクリプションするケースが発生する可能性があります。

サンプルコード：
<dx-codeblock>
:::  javascript
const client = TRTC.createClient({ mode: 'rtc', sdkAppId, userId, userSig });
// shareClientのリモートストリーム自動サブスクリプションをオフにすると設定する必要があります。すなわちautoSubscribe：false
const shareClient = TRTC.createClient({ mode: 'rtc', sdkAppId, `share_${userId}`, userSig, autoSubscribe: false,});

// ローカルのオーディオビデオストリームの公開を行うclientは、shareClientが公開するストリームのサブスクリプションを取り消す必要があります。
client.on('stream-added', event => {
  const remoteStream = event.stream;
  const remoteUserId = remoteStream.getUserId();
  if (remoteUserId === `share_${userId}`) {
    // 自身の画面共有ストリームのサブスクリプションをキャンセル
    client.unsubscribe(remoteStream);
  }else{
    //その他一般的なリモートストリームのサブスクリプション
    client.subscribe(remoteStream);
  }
});

await client.join({ roomId });
await shareClient.join({ roomId });

const localStream = TRTC.createStream({ audio: true, video: true, userId }); 
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });

// ... 関連コードの初期化や公開を省略し、必要に応じてストリームを公開すればよい。

:::
</dx-codeblock>

## 画面共有のシステムサウンド収集

**現時点でシステム音声のキャプチャはChrome M74+のみサポートしており、WindowsおよびChrome OS上ではシステム全体のオーディオをキャプチャすることができ、LinuxおよびMacではタブのオーディオのみキャプチャできます。その他のChromeのバージョン、その他のシステム、その他のブラウザはいずれもサポートしていません。**

<dx-codeblock>
:::  javascript
// 画面共有ストリームの作成screenAudioはtrueに設定してください。システムとマイクの音量の同時収集がサポートされていませんので、同時にaudio属性をtrueに設定しないでください
const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });
await shareStream.initialize();
...
:::
</dx-codeblock>

表示されるダイアログで「オーディオ共有」にチェックを入れると、公開されたストリームにシステムサウンドが付きます。
