ライブe-コマースストリーミングコンポーネントはライブコマースシナリオで使用されるIM機能の2次カプセル化であり、基本的なメッセージ送受信機能をカプセル化すると同時に、ライブコマースシナリオに基づき、いいね！、ギフト、商品のプッシュ、クーポンの受け取りなど関連機能をカプセル化しています。関連SDKのダウンロードについては、 [SDKダウンロード](https://intl.cloud.tencent.com/document/product/1047/33996)をご参照ください。

##  コンポーネント使用の前提条件

- **IMアプリケーションが作成されていること**
- **グループメンバーカスタムフィールドが作成されていること**
  - attent：自身がフォローしているキャスターが記録されていること
- **グループカスタムフィールドが作成されていること**
  - add_goods ：バックエンドに新しいライブストリーミングルーム商品リストが公開されていること
  - room_status：ライブストリーミングルームの状態が制御されていること

## SDKへのアクセス
-  IM SDKの統合
```
npm i tim-wx-sdk --save
```
- ライブコマースSDKの統合
```
npm i im-live-sells --save
```

##  コンポーネントのパラメータ

| パラメータ     | 説明                                                         |
| -------- | ------------------------------------------------------------ |
| SDKAppID | IMのアプリケーションID、SDKAppIDは [IMコンソール](https://console.cloud.tencent.com/im) で作成する必要があります。作成されたアプリケーションのデフォルトは体験版で、主に統合とテストに使用されます。製品が正式にリリースされる前に、フラッグシップ版またはプロフェッショナル版を購入することをお勧めします。 |
| userSig  | IMユーザーの署名。UserSigはIM SDKへのログインに必要なパラメータであり、ビジネスバックエンドで生成された後にフロントエンドに送信されることで使用できます。UserSig生成する方法とコードの詳細については、 [UserSigの生成](https://intl.cloud.tencent.com/document/product/1047/34385) をご参照ください|
| roomID   | ライブストリーミングルームグループのチャットルームID、このIDはIMによって作成されたライブストリーミンググループ（AVChatRoom）のグループIDであり、このルームには参加人数の制限はなく、[IMコンソール](https://console.cloud.tencent.com/im-detail/qun-manage)を介して作成され、または [REST API](https://intl.cloud.tencent.com/zh/document/product/1047/34620) を介して作成されます。 |
| TIM      | IM SDK、ミニプログラム環境では **tim-wx-sdk**を使用し、Web環境では **tim-js-sdk**をご使用ください。 |
| userName | 生成されたUserSigのuserNameと一致します。                            |



## 初期化例

```javascript
import TIMLiveSell from 'im-live-sell'
import TIM from 'tim-js-sdk' //Web環境
// import TIM from 'tim-wx-sdk' ミニプログラム環境
const tls = new TIMLiveSell({
      SDKAppID: 1400***803,
      roomID: '@TGS#E****NVLGE',
      userSig: 'eJwtzM9****-reWMQw_',
      userName: 'Ho***st',
      TIM: TIM
})
```

## コンポーネントのコールバック

### TLS.EVENT.SDK_READY

コンポーネントが初期化済みであり、IM SDKの `TIM.EVENT.SDK_READY`に対応する場合のみ、SDKのメソッドを呼び出すことができます。

```javascript
tls.on(TLS.EVENT.SDK_READY, async() => {
  
})
```

### TLS.EVENT.ROOM_STATUS_CHANGE

ルーム状態の変更。例えば、キャスターのオン（オフ）ライン、一時停止など。

```javascript
tls.on(TLS.EVENT.ROOM_STATUS_CHANGE, async(data) => {
  
}
```

### TLS.EVENT.JOIN_GROUP

誰かがグループチャットに参加したときにトリガーされます。

```javascript
tls.on(TLS.EVENT.JOIN_GROUP, async(data) => {
  const {nick,avatar,userID} = data
})
```

### TLS.EVENT.EXIT_GROUP

誰かがグループチャットから退出したときにトリガー―されます。

```javascript
tls.on(TLS.EVENT.EXIT_GROUP, async(data) => {
  const {nick,avatar,userID} = data
})
```

### TLS.EVENT.NOTIFACATION

公示が変更されたときにトリガーされます。

```javascript
tls.on(TLS.EVENT.NOTIFACATION, async(data) => {
  const { notification } = data
})
```

### TLS.EVENT.MESSAGE

誰かがグループメッセージを送信したときにトリガーされます。

> 自身が送信したメッセージはこのコールバックに含まれません。送信したメッセージを表示するには、sendMessage方法を使用して返されたデータを使用します。これはIM SDKと一致しています。

```javascript
tls.on(TLS.EVENT.MESSAGE, async(data) => {
  const { nick,avatar,message,userID } = data
})
```

### TLS.EVENT.LIKE

誰かがキャスターにいいね！したときにトリガーされます。

```javascript
tls.on(TLS.EVENT.LIKE, async(data) => {
  const { nick,avatar,value,userID } = data
})
```

### TLS.EVENT.SEND_GIFT

誰かがキャスターにギフトを贈ったときにトリガーされます。

```javascript
tls.on(TLS.EVENT.SEND_GIFT, async(data) => {
  const { nick,avatar,value,userID } = data
})
```

### TLS.EVENT.ATTENT

誰かがキャスターをフォローしたときにトリガーされます。

```javascript
tls.on(TLS.EVENT.ATTENT, async(data) => {
  const { nick,avatar,value,userID } = data
})
```

### TLS.EVENT.BUY_GOODS

誰かが商品を購入したときにトリガーされます。

```javascript
tls.on(TLS.EVENT.BUY_GOODS, async(data) => {
  const { nick,avatar,value,userID } = data
})
```

### TLS.EVENT.USE_COUPON

誰かがクーポンを受け取ったときにトリガーされます。

```javascript
tls.on(TLS.EVENT.USE_COUPON, async(data) => {
  const { nick,avatar,value,userID } = data
})
```

### TLS.EVENT.ADD_GOODS

このライブストリーミングでのお勧め商品が変更されたときにトリガーされます。

```javascript
tls.on(TLS.EVENT.ADD_GOODS, async(data) => {
  const { nick,avatar,value } = data
})
```

### TLS.EVENT.KICKED

アカウントが他のデバイスのログインに使用されたときにトリガーされます。

```javascript
tls.on(TLS.EVENT.KICKED, async() => {
  
})
```

### TLS.EVENT.NETWORK_CHANGE

ネットワークに変更が生じたときにトリガーされます。

```javascript
tls.on(TLS.EVENT.NETWORK_CHANGE, async() => {
  
})
```

### TLS.EVENT.SDK_NOT_READY

SDKが使用不能となったときにトリガーされます。

```javascript
tls.on(TLS.EVENT.SDK_NOT_READY, async() => {
  
})
```

### TLS.EVENT.PROFILE_UPDATE

個人プロファイルに変更が生じたときにトリガーされます。

```javascript
tls.on(TLS.EVENT.PROFILE_UPDATE, async() => {
  
})
```

### TLS.EVENT.ERROR

SDKにエラーが発生したときにトリガーされます。

```javascript
tls.on(TLS.EVENT.ERROR, async(error) => {
  
})
```

### ${type}

カスタムメッセージを呼び出す場合にトリガーされる同名のイベント。

```javascript
tls.on(`${type}`, async(error) => {
  
})
```



## コンポーネントメソッド

### sendMessage(message:string)

弾幕メッセージを送信するために使用されます。

```javascript
/**
 * このメソッドを呼び出して弾幕メッセージを送信すると、グループの全員がこのテキストメッセージを受信できます。
 * @method sendMessage
 * @for TLS
 * @param msg 入力必須 弾幕メッセージ
 * @returns Promise
 */
const {nick,avatar,message} = await tls.sendMessage(msg);

```

### like(extension?:string)

キャスターにいいね！をするために使用します。

> extension：いいね！した場合の追加情報。例えば、ユーザーレベルなど。

```javascript
/**
 * このメソッドを呼び出してキャスターにいいね！メッセージを送信すると、グループの全員がこのいいね！メッセージを受信できます。
 * @method like
 * @for TLS
 * @param extension オプションパラメータ。いいね！した場合の追加情報
 * @returns Promise
 */
const {nick,avatar} = await tls.like(extension);
```

### gift(extension?:string)

キャスターにギフトを贈るために使用します。

> extension：ギフトを贈った場合の追加情報。例えば、ギフト情報など。

```javascript
/**
 * このメソッドを呼び出してキャスターにギフトメッセージを送信すると、グループ内の全員がこのギフトメッセージを受信できます。
 * @method gift
 * @for TLS
 * @param msg オプションパラメータ。ギフトを贈った場合の追加情報
 * @returns Promise
 */
const {nick,avatar} = await tls.gift(extension);
```

### exitRoom()

ライブストリーミングルームから退出するために使用します。

```javascript
/**
 * ルームから退出。キャスター（グループマスター）はルームから退出できません
 * @method exitRoom
 * @for TLS
 * @param 
 * @returns Promise
 */
const {status} = await tls.exitRoom();
```

### joinRoom()

ライブストリーミングルームに入室するために使用します。

```javascript
/**
 * 入室
 * @method joinRoom
 * @for TLS
 * @param 
 * @returns Promise
 */
const {userInfo,groupInfo} = await tls.joinRoom();
const { ownerInfo } = groupInfo;//キャスター情報を取得
const { userID,nick,avatar } = ownerInfo
```

### getRoomInfo()

現在のルーム情報を取得するために使用します。

```javascript
/**
 * このチャットルームの基本情報を取得
 * @method getRoomInfo
 * @for TLS
 * @param 
 * @returns Promise
 */
const {...ownerInfo} = await tls.getRoomInfo();
//ownerInfo キャスターの関連情報
const { userID,nick,avatar } = ownerInfo
```

### attention()

キャスターをフォローするために使用します。

```javascript
/**
 * キャスターをフォロー
 * @method attention
 * @for TLS
 * @param 
 * @returns Promise
 */
const {nick,avatar} = await tls.attention();
```

### cancelAttention()

キャスターのフォローをキャンセルするために使用します。

```javascript
/**
 * フォローをキャンセル
 * @method cancelAttention
 * @for TLS
 * @param 
 * @returns Promise
 */
const {nick,avatar} = await tls.cancelAttention();
```

### destroy()

コンポーネントを廃棄するために使用します。

```javascript
/**
 * コンポーネントの廃棄
 * @method destroy
 * @for TLS
 * @param 
 * @returns Promise
 */
tls.destroy(); 
```

### sendCustomMsgAndEmitEvent(eventName: string, extension?: string)

カスタムメッセージを送信し、type型のコールバックイベントをトリガーするために使用します。

>
> - eventName：イベント名。
> - extension：カスタムメッセージ送信者の付属情報。

```javascript
/**
 * カスタムメッセージを送信し、同名のイベントをトリガー
 * @method destroy
 * @for TLS
 * @param eventName:イベント名、someExtension：追加情報
 * @returns Promise
 */
await tls.sendCustomMsgAndEmitEvent('eventName','someExtension')
```

## ビルトインオブジェクト

TIM が `TIM.create` で作成したオブジェクト、TIMのすべてのメソッドに使用できます。

## イベント

| EVENT                                                 | 説明                                                         |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| [TLS.EVENT.SDK_READY](#tls.event.sdk_ready)           | コンポーネントが初期化済みで、IM SDKの `TIM.EVENT.SDK_READY`に対応する場合に限り、SDKメソッドを呼び出すことができます。 |
| [TLS.EVENT.JOIN_GROUP](#tls.event.join_group)         | 誰かがグループチャットに参加したときにトリガーされます。                                         |
| [TLS.EVENT.EXIT_GROUP](#tls.event.join_group)         | 誰かがグループチャットから退出したときにトリガーされます。                                         |
| [TLS.EVENT.NOTIFACATION](#tls.event.notifacation)     | 公示が変更されたときにトリガーされます。                                         |
| [TLS.EVENT.MESSAGE](#tls.event.message)               | 誰かがグループメッセージを送信したときにトリガーされます。                                       |
| [TLS.EVENT.PROFILE_UPDATE](#tls.event.profile_update) | 個人プロファイルが修正されたときにトリガーされます。                                     |
| [TLS.EVENT.ERROR](#tls.event.error)                   | SDK にエラーが発生したときにトリガーされます。                                         |
| [TLS.EVENT.KICKED](#tls.event.kicked)                 | アカウントが別のデバイスにログインしたときにトリガーされます。                                     |
| [TLS.EVENT.NETWORK_CHANGE](#tls.event.network_change) | ネットワークに変更が生じたときにトリガーされます。                                         |
| [TLS.EVENT.SDK_NOT_READY](#tls.event.sdk_not_ready)   | SDKが使用不能であるときにトリガーされます。                                           |
| [TLS.EVENT.LIKE](#tls.event.like)                     | 誰かがキャスターにいいね！したときにトリガーされます。                                       |
 [TLS.EVENT.BUY_GOODS](#tls.event.buy_goods)           | 誰かが商品を購入したときにトリガーされます。                                         |
| [TLS.EVENT.SEND_GIFT](#tls.event.send_gift)           | 誰かがキャスターにギフトを贈ったときにトリガーされます。                                       |
| [TLS.EVENT.ATTENT](#tls.event.attent)                 | 誰かがキャスターをフォローしたときにトリガーされます。                                         |
| [TLS.EVENT.ADD_GOODS](#tls.event.add_goods)           | このライブブロードキャストでお勧めの商品が変更されたときにトリガーされます。                         |
| [TLS.EVENT.USE_COUPON](#tls.event.use_coupon)         | 誰かがクーポンを受け取ったときにトリガーされます。                                        |

