ここでは、主にTencent Cloud TRTC デスクトップブラウザ SDK の基本作業フローおよびTencent Real-Time Communication通話機能を実装する方法を紹介します。

TRTC デスクトップブラウザ SDK には、以下のオブジェクトがよく現れます。
- Client オブジェクトは、ローカルクライアントを意味します。[Client](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html) クラスのメソッドは、チャットルームの追加、ローカルストリーミングの公開、リモートストリーミングの閲覧などの機能を提供します。
- Stream オブジェクトは、音声ビデオストリーミングオブジェクトを意味しています。ローカルオーディオ・ビデオストリーミングオブジェクト [LocalStream](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html) およびリモートオーディオ・ビデオストリーミングオブジェクト[RemoteStream](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html)を含みます。Stream クラスのメソッドは、オーディオ・ビデオストリーミングオブジェクトの動作を主に提供し、音声およびビデオのプレイバックコントロールを含みます。

基本のオーディオビデオ通話のAPIコールフローは下図に示すとおりです。
![](https://main.qcloudimg.com/raw/9f246e5a88e5a8176290eb6070a0ecb6.jpg)

## 手順1： Client オブジェクトの新規作成

 [TRTC.createClient()](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.createClient) メソッドによって、 [Client](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html) オブジェクトを作成します。パラメータの設定は以下のとおりです。
- `mode`：TRTC通話モードのこと。`rtc`に設定
- `sdkAppId`：Tencent Cloudから申請した sdkAppId
- `userId`：ユーザー ID
- `userSig`：ユーザー署名。計算方式は [ UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください

```javascript
const client = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId,
  userSig
});
```

## 手順2：オーディオビデオ通話ルームへの参加

 [Client.join()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#join) をコールして、オーディオビデオ通話ルームに参加します。
パラメータ`roomId`：ルーム ID

```javascript
client
  .join({ roomId })
  .catch(error => {
    console.error('入室失敗 ' + error);
  })
  .then(() => {
    console.log('入室成功');
  });
```

## 手順3：ローカルストリーミングの公開およびリモートストリーミングの閲覧

1.  [TRTC.createStream()](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.createStream) メソッドを使用して、ローカルオーディオ・ビデオストリーミングを作成します。
 以下のインスタンスは、カメラおよびマイクからオーディオ・ビデオストリーミングを採集しています。パラメータは以下のとおり設定します。
 - `userId`：ローカルストリーミング所属のユーザー ID
 - `audio`：オーディオの起動の有無
 - `video`：ビデオの起動の有無

 ```javascript
const localStream = TRTC.createStream({ userId, audio: true, video: true });
 ```

2.  [LocalStream.initialize()](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#initialize) をコールして、ローカルオーディオ・ビデオストリーミングを初期化します。
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

3. ローカルストリーミングの初期化が成功した後、 [Client.publish()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#publish) メソッドをコールして、ローカルストリーミングを公開します。
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

4. リモートストリーミングは、[Client.on('stream-added')](https://trtc-1252463788.file.myqcloud.com/web/docs/module-Event.html#.STREAM_ADDED)イベントのモニタによって取得され、そのイベントを受信した後は、 [Client.subscribe()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#subscribe) によってリモートオーディオ・ビデオストリーミングを閲覧します。

>?
>-  [Client.join()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#join) で入室する前に [Client.on('stream-added')](https://trtc-1252463788.file.myqcloud.com/web/docs/module-Event.html#.STREAM_ADDED) イベントを登録し、リモートユーザーの入室通知を見落とすことがないようにしてください。
>- リモートストリーミングから退出するなどその他の イベントは、[API 詳細ドキュメント](https://trtc-1252463788.file.myqcloud.com/web/docs/module-Event.html) から表示できます。

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

5. ローカルストリーミングの初期化成功のコールバック中、またはリモートストリーミングの閲覧成功のコールバック中では、 [Stream.play()](https://trtc-1252463788.file.myqcloud.com/web/docs/Stream.html#play) メソッドをコールすることで、Webページで音声ビデオを再生します。`play`メソッドは1個の div エレメント ID をパラメータとして受け入れて、SDK の内部はその div エレメントの下で該当する音声ビデオタグを自動作成し、その上で音声ビデオを再生します。
 - ローカルストリーミングの初期化が成功したとき、ローカルストリーミングを再生します
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

通話終了時に [Client.leave()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#leave) メソッドをコールし、オーディオビデオ通話ルームを退出すると、すべてのオーディオビデオ通話によるセッションが終了します。

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
