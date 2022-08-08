TRTC Web SDKの画面共有のサポート状況については、[ブラウザサポート状況](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html)をご覧ください。また、SDK も[TRTC.isScreenShareSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.isScreenShareSupported)インターフェースを提供し、現在のブラウザが画面共有をサポートしているかどうかを判断できるようにしています。
ここでは、シ―ンごとの実装プロセスについてご説明します。

> !
> - Web端末では現時点ではサブストリームの公開をサポートしておらず、画面共有の公開はメインストリームの公開によって行います。リモートの画面共有ストリームがWebユーザーからの場合、[RemoteStream.getType()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getType)の戻り値は'main'となります。通常は、それがWeb端末からの画面共有ストリームであることはuserIdによって識別します。
> - Native（iOS、Android、Mac、Windowsなど）端末ではサブストリームの公開をサポートしており、画面共有の公開はサブストリームの公開によって行います。リモートの画面共有ストリームがNativeユーザーからの場合、[RemoteStream.getType()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getType)の戻り値は'auxiliary'となります。

## 画面共有ストリームの作成とリリース

[](id:step1)
### ステップ1：画面共有ストリームの作成
画面共有ストリームにはビデオストリームとオーディオストリームが含まれます。そのうちオーディオストリームはマイクオーディオとシステムオーディオに分けられます。
```javascript
// 通常は、userIdにプレフィックス`share_`を加え、これが画面共有用のクライアントオブジェクトだということを識別するために用いることが推奨されます。
const userId = 'share_userId';
const roomId = 'roomId';

// good 正しい用法
// 画面のビデオストリームのみをキャプチャ
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// or マイクオーディオおよび画面のビデオストリームをキャプチャ
const shareStream = TRTC.createStream({ audio: true, screen: true, userId });
// or システムオーディオおよび画面のビデオストリームをキャプチャ
const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });

// bad 間違った用法
const shareStream = TRTC.createStream({ camera: true, screen: true });
// or
const shareStream = TRTC.createStream({ camera: true, screenAudio: true });

```

>! 
>- audioとscreenAudioの属性を同時にtrueに設定することはできず、cameraとscreenAudioの属性を同時にtrueに設定することはできません。screenAudioについてのその他の情報は、このドキュメントのパート5でご説明します。
>- cameraとscreenの属性を同時にtrueに設定することはできません。

[](id:step2)
### ステップ2：画面共有ストリームの初期化
初期化の際、ブラウザはユーザーに対し画面共有の内容と権限をリクエストします。ユーザーが権限承認を拒否した場合、またはシステムがブラウザに画面共有の権限を与えなかった場合、コードは`NotReadableError`または`NotAllowedError`のエラーをキャッチします。このとき、ブラウザの設定またはシステムの設定を行って画面共有の権限を有効化し、画面共有ストリームの初期化を再度行うよう、ユーザーに対して促す必要があります。
>! Safariの制限により、 画面共有ストリームの初期化操作は必ずクリックしたイベントのコールバック内で完了しなければなりません。この問題についての詳細な説明は、[よくあるご質問](#よくあるご質問)をご参照ください

```javascript
try {
  await shareStream.initialize();
} catch (error) {
  // 画面共有ストリームの初期化に失敗したとき、ユーザーに通知してその後の入室と公開のプロセスを停止させる
  switch (error.name) {
    case 'NotReadableError':
      // ユーザーに通知して、システムが現在のブラウザによる画面内容取得を許可するよう確認させる
      return;
    case 'NotAllowedError':
      if (error.message.includes('Permission denied by system')) {
        // ユーザーに通知して、システムが現在のブラウザによる画面内容取得を許可するよう確認させる
      } else {
        // ユーザーが画面共有を拒否/キャンセル
      }
      return;
    default:
      // 画面共有ストリームの初期化の際の不明なエラーが発生したため、リトライするようユーザーに通知する
      return;
  }
}
```

[](id:step3)
### ステップ3：画面共有を担うクライアントオブジェクトの作成
通常は、userIdにプレフィックス`share_`を加え、これが画面共有用のクライアントオブジェクトだということを識別するために用いることが推奨されます。

```javascript
const shareClient = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId, // ‘share_teacher’など
  userSig
});
// クライアントオブジェクトの入室
try {
  await shareClient.join({ roomId });
  // ShareClient join room success
} catch (error) {
  // ShareClient join room failed
}

```
[](id:step4)
### ステップ4：画面共有ストリームの公開
ステップ1で作成したクライアントオブジェクトを通じて公開します。公開に成功すると、画面共有ストリームをリモートで受信できます。
```javascript
try {
  await shareClient.publish(shareStream);
} catch (error) {
  // ShareClient failed to publish local stream
}
```

### 完全なコード
```javascript
// 通常は、userIdにプレフィックス`share_`を加え、これが画面共有用のクライアントオブジェクトだということを識別するために用いることが推奨されます。
const userId = 'share_userId';
const roomId = 'roomId';
// 画面のビデオストリームのみをキャプチャ
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// or マイクオーディオおよび画面のビデオストリームをキャプチャ
// const shareStream = TRTC.createStream({ audio: true, screen: true, userId });
// or システムオーディオおよび画面のビデオストリームをキャプチャ
// const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });
try {
  await shareStream.initialize();
} catch (error) {
  // 画面共有ストリームの初期化に失敗したとき、ユーザーに通知してその後の入室と公開のプロセスを停止させる
  switch (error.name) {
    case 'NotReadableError':
      // ユーザーに通知して、システムが現在のブラウザによる画面内容取得を許可するよう確認させる
      return;
    case 'NotAllowedError':
      if (error.message.includes('Permission denied by system')) {
        // ユーザーに通知して、システムが現在のブラウザによる画面内容取得を許可するよう確認させる
      } else {
        // ユーザーが画面共有を拒否/キャンセル
      }
      return;
    default:
      // 画面共有ストリームの初期化の際の不明なエラーが発生したため、リトライするようユーザーに通知する
      return;
  }
}
const shareClient = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId, // ‘share_teacher’など
  userSig
});
// クライアントオブジェクトの入室
try {
  await shareClient.join({ roomId });
  // ShareClient join room success
} catch (error) {
  // ShareClient join room failed
}
try {
  await shareClient.publish(shareStream);
} catch (error) {
  // ShareClient failed to publish local stream
}
```

### 画面共有パラメータ設定
設定可能なパラメータには解像度、フレームレート、ビットレートがあります。必要に応じ、[setScreenProfile()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setScreenProfile)インターフェースでprofileを指定することができ、各profileは1組の解像度、フレームレート、ビットレートに対応します。SDKはデフォルトで'1080p'の設定を使用します。

```javascript
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// setScreenProfile()はinitialize()の前に呼び出す必要があります。
shareStream.setScreenProfile('1080p');
await shareStream.initialize();
```

あるいは、カスタマイズした解像度、フレームレート、ビットレートを使用します。

```javascript
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// setScreenProfile()はinitialize()の前に呼び出す必要があります。
shareStream.setScreenProfile({ width: 1920, height: 1080, frameRate: 5, bitrate: 1600 /* kbps */});
await shareStream.initialize();
```
画面共有属性推奨リスト：

| profile | 解像度（幅 x 高） | フレームレート（fps） | ビットレート (kbps) |
|:--------|:----------------|:----------|:------------|
| 480p    | 640 x 480       | 5         | 900         |
| 480p_2  | 640 x 480       | 30        | 1000        |
| 720p    | 1280 x 720      | 5         | 1200        |
| 720p_2  | 1280 x 720      | 30        | 3000        |
| 1080p   | 1920 x 1080     | 5         | 1600        |
| 1080p_2 | 1920 x 1080     | 30        | 4000        |

>! 高すぎるパラメータを設定することで予測不可能な問題が発生することを避けるため、推奨するパラメータに従って設定することをお勧めします。

## 画面共有の停止

```javascript
// 画面共有クライアントがストリーム公開をキャンセルする
await shareClient.unpublish(shareStream);
// 画面共有ストリームを閉じる
shareStream.close();
// 画面共有クライアントが退室
await shareClient.leave();

// 上記の3ステップは必須ではなく、シーンのニーズに応じて必要なコードを実行します。通常は、入室済みかどうか、ストリームを公開済みかどうかの判断を追加する必要があります。より詳細なコードの例については、[demoソースコード](https://github.com/LiteAVSDK/TRTC_Web/blob/main/base-js/js/share-client.js)をご参照ください。
```

また、ユーザーがブラウザ付属のボタンで画面共有を停止する可能性もあるため、画面共有ストリームでは画面共有停止イベントを監視し、それに応じた処理を行う必要があります。
<img src="https://qcloudimg.tencent-cloud.cn/raw/bb9d93106c1d22f819e905ea3196d866.png" width="600px">

```javascript
// 画面共有ストリームの画面共有停止イベント監視
shareStream.on('screen-sharing-stopped', event => {
  // 画面共有クライアントがプッシュを停止する
  await shareClient.unpublish(shareStream);
  // 画面共有ストリームを閉じる
  shareStream.close();
  // 画面共有クライアントが退室
  await shareClient.leave();
});
```

## カメラからのビデオと画面共有の同時公開
1つのClientは1つのオーディオと1つのビデオまでしか同時に公開できません。カメラからのビデオと画面共有を同時に公開する場合は、 2つのClientを作成し、それぞれの用途に用いる必要があります。
例えば2つのClientを作成し、それぞれ次のようにします。
- **client**：ローカルオーディオビデオストリーミングの公開を担い、shareClient以外のすべてのリモートストリームを閲覧します。
- **shareClient**：画面共有ストリームの公開を担い、どのリモートストリームも閲覧しません。

>! 
>- 画面共有を担うshareClientでは自動サブスクリプションを無効にしておかなければ、リモートストリームのサブスクリプションの重複が生じます。[APIの説明](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createClient)をご参照ください。
>- ローカルオーディオビデオストリーミングの公開を担うclientでは、shareClientが公開するストリームのサブスクリプションをキャンセルする必要があります。そうしなければ、自分で自分を閲覧するという状況が発生してしまいます。

サンプルコード：
```javascript
const client = TRTC.createClient({ mode: 'rtc', sdkAppId, userId, userSig });
// shareClientでリモートストリームの自動サブスクリプションを無効化、すなわちautoSubscribe: falseとする必要があります
const shareClient = TRTC.createClient({ mode: 'rtc', sdkAppId, `share_${userId}`, userSig, autoSubscribe: false,});

// ローカルオーディオビデオストリーミングの公開を担うclientでは、shareClientが公開するストリームのサブスクリプションをキャンセルする必要があります。
client.on('stream-added', event => {
  const remoteStream = event.stream;
  const remoteUserId = remoteStream.getUserId();
  if (remoteUserId === `share_${userId}`) {
    // 自身の画面共有ストリームのサブスクリプションをキャンセル
    client.unsubscribe(remoteStream);
  } else {
    //その他一般的なリモートストリームのサブスクリプション
    client.subscribe(remoteStream);
  }
});

await client.join({ roomId });
await shareClient.join({ roomId });

const localStream = TRTC.createStream({ audio: true, video: true, userId }); 
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });

// ... 初期化および関連コードの公開を省略し、必要に応じてストリームを公開します。

```

## 画面共有のシステム音声キャプチャ

**システム音声キャプチャはChrome M74+のみサポートしています。WindowsおよびChrome OS上ではシステム全体のオーディオをキャプチャすることができ、LinuxおよびMacではオプションタブのオーディオのみキャプチャできます。その他のChromeのバージョン、その他のシステム、その他のブラウザはいずれもサポートしていません。**

```javascript
// 画面共有ストリームを作成する際、screenAudioはtrueに設定してください、システム音声とマイク音声の同時キャプチャはサポートしていないため、audio属性を同時にtrueに設定しないでください
const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });
await shareStream.initialize();
...
```

ポップアップしたダイアログボックスで「オーディオ共有」にチェックを入れると、公開されるstreamにはシステム音声が入ります。



## よくあるご質問
1. **Safariの画面共有で`getDisplayMedia must be called from a user gesture handler`というエラーが表示されます。**
これは、Safariが`getDisplayMedia`スクリーンキャプチャインターフェースを制限しているためであり、ユーザーがイベントのコールバック関数をクリックして実行してから1秒以内でなければ呼び出すことができません。詳細については、[webkit issue](https://bugs.webkit.org/show_bug.cgi?id=198040)をご参照ください。
```javascript
// good
async function onClick() {
  // onClickで実行する場合は、先にキャプチャロジックを実行することをお勧めします
  const screenStream = TRTC.createStream({ screen: true });
  await screenStream.initialize();
  await client.join({ roomId: 123123 });
}

// bad
async function onClick() {
  await client.join({ roomId: 123123 });
  // 入室には1秒以上かかることがあり、キャプチャに失敗する可能性があります
  const screenStream = TRTC.createStream({ screen: true });
  await screenStream.initialize();
}
```

2. **Mac Chromeで、スクリーンレコーディングの権限が得られている状況で画面共有に失敗し、"NotAllowedError: Permission denied by system"または"NotReadableError: Could not start video source"というエラーメッセージが表示されましたが、[Chrome bug](https://bugs.chromium.org/p/chromium/issues/detail?id=1306876)ですか。**
対処方法：**設定**> **セキュリティとプライバシー**をクリック> **プライバシー**をクリック> **スクリーンレコーディング**をクリック > Chromeのスクリーンレコーディング権限を無効化 > Chromeのスクリーンレコーディング権限を再度有効化 > Chromeブラウザを無効化 > Chromeブラウザを再度有効化。

3. **[WebRTC画面共有の既知の問題と回避策](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-02-info-webrtc-issues.html#h2-9)**

4. **[ElectronによるTRTC Web SDK画面共有の使用](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-33-advanced-electron-screen-share.html)**

5. **ユーザーが選択した画面共有のタイプの判断：画面全体、ウィンドウ、Chromeタブ。**
```javascript
// 画面共有キャプチャの成功後
const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });
await shareStream.initialize();

// displaySurfaceによってキャプチャのタイプを判断します。
const { displaySurface } = shareStream.getVideoTrack().getSettings();
// 例えば、monitorは画面全体、windowはあるアプリケーションのウィンドウ、browserはChromeのあるタブ
```
詳細については、[displaySurface](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackSettings/displaySurface)をご参照ください。