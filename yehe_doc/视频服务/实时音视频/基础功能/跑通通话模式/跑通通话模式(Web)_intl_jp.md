ここでは、主にTencent Cloud TRTC Web SDKの基本ワークフロー、およびリアルタイムなオーディオビデオ通話機能を実装する方法を紹介します。

TRTC Web SDKの使用中には、以下のオブジェクトが頻繁に登場します。
- Client オブジェクト。ローカルクライアントを表します。[Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html)クラスのメソッドにより、通話ルームへの参加、ローカルストリーミングの公開、リモートストリーミングの閲覧などの機能を提供します。
- Streamオブジェクト。オーディオビデオストリーミングオブジェクトを表し、ローカルのオーディオビデオストリーミングオブジェクト[LocalStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html)、およびリモート側のオーディオビデオストリーミングオブジェクト[RemoteStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html)が含まれます。Streamクラスのメソッドでは主に、オーディオビデオストリーミングオブジェクトのアクションを提供し、これにはオーディオおよびビデオの再生コントロールが含まれます。

基本のオーディオビデオ通話のAPIコールフローは下図に示すとおりです。
![](https://main.qcloudimg.com/raw/9f246e5a88e5a8176290eb6070a0ecb6.jpg)

## 手順1： Clientオブジェクトの新規作成

[TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)メソッドによって、[Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html)オブジェクトを作成します。パラメータの設定は以下のとおりです。
- `mode`：TRTC通話モードのこと。`rtc`に設定
- `sdkAppId`：Tencent Cloudから申請したsdkAppId
- `userId`：ユーザーID
- `userSig`：ユーザー署名。計算方式は[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください

```javascript
const client = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId,
  userSig
});
```

## 手順2：オーディオビデオ通話ルームへの参加

[Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)を呼び出して、オーディオビデオ通話ルームに参加します。
パラメータ`roomId`：ルームID

```javascript
client
  .join({ roomId })
  .then(() => {
    console.log('入室成功');
  })
  .catch(error => {
    console.error('入室失敗 '+ error);
  });
```

## 手順3：ローカルストリーミングの公開およびリモートストリーミングの閲覧

1. [TRTC.createStream()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream)メソッドを使用して、ローカルのオーディオビデオストリーミングを作成します。
 以下のインスタンスは、カメラおよびマイクからオーディオビデオストリーミングを採集しています。パラメータは以下のとおり設定します。
 - `userId`：ローカルストリーミング所属のユーザーID
 - `audio`：オーディオの起動の有無
 - `video`：ビデオの起動の有無

 ```javascript
const localStream = TRTC.createStream({ userId, audio: true, video: true });
 ```

2. [LocalStream.initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize)を呼び出して、ローカルのオーディオビデオストリーミングを初期化します。
```javascript
localStream
  .initialize()
  .then(() => {
    console.log('ローカルストリーミング初期化の成功');
  })
  .catch(error => {
    console.error('ローカルストリーミング初期化の失敗 ' + error);
  });
```

3. ローカルストリーミングの初期化に成功したら、[Client.publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish)メソッドを呼び出して、ローカルストリーミングを公開します。
```javascript
client
  .publish(localStream)
  .then(() => {
    console.log('ローカルストリーミング公開の成功');
  })
  .catch(error => {
    console.error('ローカルストリーミング公開の失敗 ' + error);
  });
```

4. リモートストリーミングは、[Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html#.STREAM_ADDED)のイベント監視によって取得され、このイベントを受信した後、[Client.subscribe()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#subscribe)を介して、リモート側のオーディオビデオストリーミングを閲覧します。
>?
>- [Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)で入室する前に、[Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html#.STREAM_ADDED)イベントを登録し、リモートユーザーの入室通知を見落とすことがないようにしてください。
>- リモートストリーミングから退出するなどその他のイベントは、[API詳細ドキュメント](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html)で確認できます。
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

5. ローカルストリーミングの初期化成功のコールバック、またはリモートストリーミングの閲覧成功イベントのコールバックでは、[Stream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#play)メソッドを呼び出すことで、Webページ上で音声ビデオを再生します。`play`メソッドがdivエレメントのIDをパラメータとして受け入れると、SDKの内部で、そのdivエレメント下に対応する音声ビデオタグを自動作成し、その上で音声ビデオを再生します。
 - ローカルストリーミングの初期化が成功したとき、ローカルストリーミングを再生します
```javascript
localStream
  .initialize()
  .then(() => {
    console.log('ローカルストリーミング初期化の成功');
    localStream.play('local_stream');
  })
  .catch(error => {
    console.error('ローカルストリーミング初期化の失敗 ' + error);
  });
```
 - リモートストリーミングの閲覧が成功したとき、リモートストリーミングを再生
```javascript
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('リモートストリーミングの閲覧成功: ' + remoteStream.getId());
  // リモートストリーミングの再生
  remoteStream.play('remote_stream-' + remoteStream.getId());
});
```

## 手順4：オーディオビデオ通話ルームからの退出

通話終了時は、[Client.leave()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#leave)メソッドを呼び出して、オーディオビデオ通話ルームを退出し、すべてのオーディオビデオ通話によるセッションが終了します。

```javascript
client
.leave()
.then(() => {
  // 退室成功。再度client.joinをコールして再入室し、新たに通話することもできます。
})
.catch(error => {
  console.error('退室失敗 ' + error);
  // このエラーは回復不可能です。ページを更新する必要があります。
});
```

>! 各端末のユースケースappSceneについては、統一する必要があります。統一していない場合、想定外のトラブルが生じる恐れがあります。
