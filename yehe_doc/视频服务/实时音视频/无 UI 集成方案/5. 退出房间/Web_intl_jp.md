ここでは主に、現在のTRTCルームから自主的に退出する方法と、どのような状況下で強制的に退出させられるかについてご説明します。
![](https://qcloudimg.tencent-cloud.cn/raw/ea39f08a98dc41195ae63a6ecae803b8.png)

TRTC Web SDKの使用中には、以下のオブジェクトが頻繁に登場します。
- Client オブジェクト。ローカルクライアントを表します。[Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html)クラスのメソッドにより、通話ルームへの参加、ローカルストリーミングの公開、リモートストリーミングの閲覧などの機能を提供します。
- Streamオブジェクト。オーディオビデオストリーミングオブジェクトを表し、ローカルのオーディオビデオストリーミングオブジェクト[LocalStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html)、およびリモート側のオーディオビデオストリーミングオブジェクト[RemoteStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html)が含まれます。Streamクラスのメソッドでは主に、オーディオビデオストリーミングオブジェクトのアクションを提供し、これにはオーディオおよびビデオの再生コントロールが含まれます。

[](id:step1)
## ステップ1：前のステップの完了
ドキュメント[入室](https://intl.cloud.tencent.com/document/product/647/48424)を参照し、clientを作成して入室します。

[](id:step2)
## ステップ2：現在のルームから自主的に退出する

通話終了時は、[Client.leave()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#leave)メソッドを呼び出して、オーディオビデオ通話ルームを退出し、すべてのオーディオビデオ通話によるセッションが終了します。

```javascript
await client.leave(); 
```

[](id:step3)
## ステップ3：現在のルームから退出させられる
ユーザーが自主的に退室する以外に、次のような場合、ユーザーは[`CLIENT_BANNED`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.CLIENT_BANNED)イベントを受信します。これは、そのユーザーが退室させられたことを表します。

```javascript
client.on('client-banned', error => {
  console.error('client-banned observed: ' + error.message);
  // client-banned observed: client was banned because of duplicated userId joining the room.
  // client-banned observed: client was banned because of you got banned by account admin
});
```

- **状況1：同名のユーザーによって現在のルームから強制退出させられる**
1つのルーム内に、userIdが同じで、ロールがどちらもキャスターであるユーザーが同時に現れた場合、先に入室していたユーザーがルームから強制退出させられます。
例えば、2名のユーザーA、Bが、同一の`userId`で相次いで入室した場合、AはBによって退室させられます。
同名ユーザーによる同一ルームへの同時入室は許可されない行為であり、双方のオーディオビデオ通話に異常を起こすおそれがあるため、このような状況を避けなければなりません。

- **状況2：サーバーAPIによって現在のルームから強制退出させられる、または現在のルームが解散される**
サーバー側の[RemoveUser](https://intl.cloud.tencent.com/document/product/647/34268) | [RemoveUserByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39630)インターフェースによって、あるユーザーをあるTRTCルームから強制退出させることができます。このユーザーは退室させられると、[`CLIENT_BANNED`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.CLIENT_BANNED)イベントを受信します。あるいは、サーバー側の[DismissRoom](https://intl.cloud.tencent.com/document/product/647/34269) | [DismissRoomByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39631)インターフェースによって、あるTRTCルームを解散させることができます。ルームの解散後、このルームのすべてのユーザーは[`CLIENT_BANNED`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.CLIENT_BANNED)イベントを受信します。
