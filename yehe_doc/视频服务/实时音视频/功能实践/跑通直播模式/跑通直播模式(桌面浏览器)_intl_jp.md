ここでは主に、視聴者としてライブルームに入室し、マイク接続して双方向通信を行うシナリオをご紹介します。キャスターとして入室してライブストリーミングを行うシナリオは、TRTCの通話シナリオと同様です。[Tencent Real-Time Communication通話](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-01-basic-video-call.html)をご参照ください。

## 手順1： Client オブジェクトの新規作成

[TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)メソッドを使用して、[Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html)オブジェクトを作成します。パラメータの設定は以下のとおりです。

- `mode`：インタラクティブストリーミングモードの場合、`live`に設定します
- `sdkAppId`：Tencent Cloudから申請した sdkAppId
- `userId`：ユーザー ID
- `userSig`：ユーザー署名

```javascript
const client = TRTC.createClient({
  mode: 'live',
  sdkAppId,
  userId,
  userSig
});
```

## 手順2：視聴者としてライブストリーミングルームに入室

 [Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join) をコールして、オーディオビデオ通話ルームに参加します。
パラメータ：

- `roomId`：ルームID
- `role`：ユーザーロール：
  - `anchor`：キャスター、キャスターのロールには、ローカルストリームを公開し、リモートストリームを受信する権限があります。デフォルトはキャスターロールです。
  - `audience`：視聴者、視聴者のロールには、リモートストリームを受信する権限のみがあり、ローカルストリームを公開する権限はありません。視聴者がキャスターとマイク接続して双方向通信を行いたい場合、[Client.switchRole()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#switchRole)を介してロールを`anchor`キャスターロールに切り替えた上で、ローカルストリームを公開する必要があります。

```javascript
// 視聴者ロールで入室して視聴します
client
  .join({ roomId, role: 'audience' })
  .catch(error => {
    console.error('入室失敗 '+ error);
  })
  .then(() => {
    console.log('入室成功');
  });
```

## 手順3：ライブストリーミングの視聴
1. リモートストリーミングは、`client.on('stream-added')`イベントのモニタによって取得され、そのイベントを受信した後は、 [Client.subscribe()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#subscribe)によってリモートオーディオ・ビデオストリーミングを閲覧します。
>?[Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join) で入室する前に`client.on('stream-added')`イベントを登録し、リモートユーザーの入室通知を見落とすことがないようにしてください。
>
```javascript
client.on('stream-added', event => {
  const remoteStream = event.stream;
  console.log('リモートストリーミングの増加: ' + remoteStream.getId());
  //リモートストリーミングの閲覧
  client.subscribe(remoteStream);
});
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('リモートストリーミングの閲覧成功: ' + remoteStream.getId());
  // リモートストリーミングの再生
  remoteStream.play('remote_stream-' + remoteStream.getId());
});
```
2.リモートストリームの閲覧成功イベントのコールバックにおいて、[Stream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#play)メソッドをコールすることで、Webページで音声ビデオを再生します。`play`メソッドは1個の div エレメント ID をパラメータとして受け入れて、SDK の内部はその div エレメントの下で該当する音声ビデオタグを自動作成し、その上で音声ビデオを再生します。

```javascript
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('リモートストリーミングの閲覧成功: ' + remoteStream.getId());
  // リモートストリーミングの再生
  remoteStream.play('remote_stream-' + remoteStream.getId());
});
```

## 手順4：キャスターとのマイク接続・双方向通信

### 手順4.1：ロールの切り替え

[Client.switchRole()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#switchRole)を使用して、ロールを`anchor`キャスターのロールに切り替えます。

```javascript
client
  .switchRole('anchor')
  .catch(error => {
    console.error('ロールの切り替えに失敗しました' + error);
  })
  .then(() => {
    // ロールの切り替えに成功しました。現在のロールはキャスターです
  });
```

### 手順4.2：マイク接続・双方向通信

1.  [TRTC.createStream()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream) メソッドを使用して、ローカルオーディオ・ビデオストリーミングを作成します。
 以下のインスタンスは、カメラおよびマイクからオーディオ・ビデオストリーミングを採集しています。パラメータは以下のとおり設定します。
 - `userId`：ローカルストリーミング所属のユーザー ID
 - `audio`：オーディオの起動の有無
 - `video`：ビデオの起動の有無

 ```javascript
const localStream = TRTC.createStream({ userId, audio: true, video: true });
```
2.  [LocalStream.initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize) をコールして、ローカルオーディオ・ビデオストリーミングを初期化します。
```javascript
localStream
  .initialize()
  .catch(error => {
    console.error('ローカルストリーミング初期化の失敗 ' + error);
  })
  .then(() => {
    console.log('ローカルストリーミング初期化の成功');
  });
```
3.ローカルストリーミングの初期化に成功すると、ローカルストリーミングが再生されます。
```javascript
localStream
  .initialize()
  .catch(error => {
    console.error('ローカルストリーミング初期化の失敗 ' + error);
  })
  .then(() => {
    console.log('ローカルストリーミング初期化の成功');
    localStream.play('local_stream');
  });
```
4. ローカルストリーミングの初期化が成功した後、[Client.publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish)メソッドをコールしてローカルストリーミングを公開し、視聴者とのマイク接続・双方向通信を起動します。
```javascript
client
  .publish(localStream)
  .catch(error => {
    console.error('ローカルストリーミング公開の失敗 ' + error);
  })
  .then(() => {
    console.log('ローカルストリーミング公開の成功');
  });
```

## 手順5：ライブルームからの退出

ライブストリーミングが終了したら、[Client.leave()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#leave) メソッドをコールし、オーディオビデオ通話ルームを退出すると、すべてのオーディオビデオ通話によるセッションが終了します。

```javascript
client
  .leave()
  .catch(error => {
    console.error('退室失敗 ' + error);
  })
  .then(() => {
    // 退室に成功しました
  });

```
