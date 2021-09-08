라이브 방송 전자상거래 솔루션 컴포넌트는 라이브 커머스 시나리오에서 사용되는 Instant Messaging (IM) 기능의 2차 캡슐화에서 비롯됩니다. 기본 메시지 송수신 기능을 캡슐화하는 동시에, 라이브 커머스 시나리오에 좋아요, 선물하기, 상품 푸시 및 바우처 등 관련 기능을 캡슐화하였습니다. 관련 SDK 다운로드는 [SDK 다운로드](https://intl.cloud.tencent.com/document/product/1047/33996)를 참고하십시오.

## 시나리오 효과
<img src="https://main.qcloudimg.com/raw/5f9c19773bcfc22334f3d6cbf4f9e13f.png" width="450px"></img>

##  컴포넌트 사용 전제조건

-** IM 애플리케이션 생성**
-**그룹 구성원 사용자 정의 필드 생성**
  -attent: 팔로우한 호스트 기록
-**그룹 사용자 정의 필드 생성**
  -add_goods: 라이브 룸의 백엔드에 신상품 리스트 나열
  -room_status: 라이브 룸 상태 제어합니다.

## SDK 연결
- IM SDK 연결
```
npm i tim-wx-sdk --save
```
- 라이브 커머스 SDK 연결
```
npm i im-live-sells --save
```

## 컴포넌트 매개변수

| 매개변수     | 설명                                                         |
| -------- | ------------------------------------------------------------ |
| SDKAppID | IM 애플리케이션 ID. SDKAppID는 [IM 콘솔](https://console.cloud.tencent.com/im)에서 생성해야 하며, 새로 생성된 애플리케이션은 기본적으로 체험판으로, 통합 및 테스트 단계에 사용됩니다. 제품 정식 출시 전, 울티메이트 또는 프로 버전 구매를 권장합니다. |
| userSig | IM 사용자 서명. UserSig는 IM SDK에 로그인하기 위한 필수 매개변수로, 비즈니스 백엔드에서 생성하여 프론트 엔드로 반환하여 사용할 수 있습니다. 생성 문서 및 코드는 [UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오. |
| roomID | 라이브 방송 그룹 채팅방 ID. 이 ID는 IM이 생성한 라이브 방송 그룹(AVChatRoom)의 그룹 ID입니다. 채팅방에는 인원 제한이 없으며 [IM 콘솔](https://console.cloud.tencent.com/im-detail/qun-manage) 또는 [REST API](https://intl.cloud.tencent.com/zh/document/product/1047/34620)를 통해 생성할 수 있습니다. |
| TIM      | IM SDK. 미니프로그램 환경에서는 **tim-wx-sdk**를, Web 환경에서는 **tim-js-sdk**를 사용하십시오. |
| userName | 생성된 UserSig의 userName과 일치함.                            |



## 초기화 예시

```javascript
import TIMLiveSell from 'im-live-sell'
import TIM from 'tim-js-sdk' //Web 환경
// import TIM from 'tim-wx-sdk' 미니프로그램 환경
const tls = new TIMLiveSell({
      SDKAppID: 1400***803,
      roomID: '@TGS#E****NVLGE',
      userSig: 'eJwtzM9****-reWMQw_',
      userName: 'Ho***st',
      TIM: TIM
})
```

## 컴포넌트 콜백

### TLS.EVENT.SDK_READY

이 콜백은 컴포넌트 초기화가 완료되면 트리거됩니다. 이 이벤트는 IM SDK의 `TIM.EVENT.SDK_READY`에 해당합니다. 이 콜백이 트리거된 후에만 SDK 메소드를 호출할 수 있습니다.

```javascript
tls.on(TLS.EVENT.SDK_READY, async() => {
  
})
```

### TLS.EVENT.ROOM_STATUS_CHANGE

이 콜백은 호스트 온라인/오프라인, 스트림 일시 중지 등 방 상태가 변경될 때 트리거됩니다.

```javascript
tls.on(TLS.EVENT.ROOM_STATUS_CHANGE, async(data) => {
  
}
```

### TLS.EVENT.JOIN_GROUP

이 콜백은 누군가가 그룹에 입장하면 트리거됩니다.

```javascript
tls.on(TLS.EVENT.JOIN_GROUP, async(data) => {
  const {nick,avatar,userID} = data
})
```

### TLS.EVENT.EXIT_GROUP

이 콜백은 누군가가 그룹에서 퇴장하면 트리거됩니다.

```javascript
tls.on(TLS.EVENT.EXIT_GROUP, async(data) => {
  const {nick,avatar,userID} = data
})
```

### TLS.EVENT.NOTIFACATION

이 콜백은 그룹 알림이 변경되면 트리거됩니다.

```javascript
tls.on(TLS.EVENT.NOTIFACATION, async(data) => {
  const { notification } = data
})
```

### TLS.EVENT.MESSAGE

이 콜백은 누군가가 그룹 메시지를 보내면 트리거됩니다.

> 자신이 보낸 메시지는 이 콜백을 통해 찾을 수 없습니다. 전송한 메시지를 화면에 표시하려면 sendMessage 메소드에서 반환된 데이터를 사용하십시오. 이는 IM SDK와 일치합니다.

```javascript
tls.on(TLS.EVENT.MESSAGE, async(data) => {
  const { nick,avatar,message,userID } = data
})
```

### TLS.EVENT.LIKE

이 콜백은 누군가가 호스트 좋아요를 누르면 트리거됩니다.

```javascript
tls.on(TLS.EVENT.LIKE, async(data) => {
  const { nick,avatar,value,userID } = data
})
```

### TLS.EVENT.SEND_GIFT

이 콜백은 누군가가 호스트에게 선물을 보내면 트리거됩니다.

```javascript
tls.on(TLS.EVENT.SEND_GIFT, async(data) => {
  const { nick,avatar,value,userID } = data
})
```

### TLS.EVENT.ATTENT

이 콜백은 누군가가 호스트에게 선물을 보니면 트리거됩니다.

```javascript
tls.on(TLS.EVENT.ATTENT, async(data) => {
  const { nick,avatar,value,userID } = data
})
```

### TLS.EVENT.BUY_GOODS

이 콜백은 누군가가 상품을 구매하면 트리거됩니다.

```javascript
tls.on(TLS.EVENT.BUY_GOODS, async(data) => {
  const { nick,avatar,value,userID } = data
})
```

### TLS.EVENT.USE_COUPON

이 콜백은 누군가가 바우처를 수령하면 트리거됩니다.

```javascript
tls.on(TLS.EVENT.USE_COUPON, async(data) => {
  const { nick,avatar,value,userID } = data
})
```

### TLS.EVENT.ADD_GOODS

이 콜백은 라이브 방송에서 추천한 상품이 변동되면 트리거됩니다.

```javascript
tls.on(TLS.EVENT.ADD_GOODS, async(data) => {
  const { nick,avatar,value } = data
})
```

### TLS.EVENT.KICKED

이 콜백은 계정이 다른 장소에서 로그인되면 트리거됩니다.

```javascript
tls.on(TLS.EVENT.KICKED, async() => {
  
})
```

### TLS.EVENT.NETWORK_CHANGE

이 콜백은 네트워크 변경 발생 시 트리거됩니다.

```javascript
tls.on(TLS.EVENT.NETWORK_CHANGE, async() => {
  
})
```

### TLS.EVENT.SDK_NOT_READY

이 콜백은 SDK 사용 불가 시 트리거됩니다.

```javascript
tls.on(TLS.EVENT.SDK_NOT_READY, async() => {
  
})
```

### TLS.EVENT.PROFILE_UPDATE

이 콜백은 개인 정보가 수정되면 트리거됩니다.

```javascript
tls.on(TLS.EVENT.PROFILE_UPDATE, async() => {
  
})
```

### TLS.EVENT.ERROR

이 콜백은 SDK에 오류 발생 시 트리거됩니다.

```javascript
tls.on(TLS.EVENT.ERROR, async(error) => {
  
})
```

### ${type}

사용자 정의 메시지가 호출될 때 트리거되는 동일한 이름의 이벤트입니다.

```javascript
tls.on(`${type}`, async(error) => {
  
})
```



## 컴포넌트 메소드

### sendMessage(message:string)

이 메소드는 댓글 자막 메시지 발송에 사용됩니다.

```javascript
/**
 * 이 메소드를 호출하여 댓글 자막을 발송하면 그룹의 모든 사용자가 해당 텍스트 메시지를 받을 수 있습니다.
 * @method sendMessage
 * @for TLS
 * @param msg 필수 입력. 댓글 자막 메시지.
 * @returns Promise
 */
const {nick,avatar,message} = await tls.sendMessage(msg);

```

### like(extension?:string)

이 메소드는 호스트 좋아요에 사용됩니다.

> extension: 좋아요 부가 정보(예: 사용자 레벨).

```javascript
/**
 * 이 메소드를 호출하여 호스트 좋아요 메시지를 발송하면 그룹의 모든 사용자가 이 좋아요 메시지를 받을 수 있습니다.
 * @method like
 * @for TLS
 * @param extension 선택 입력. 좋아요 부가 정보.
 * @returns Promise
 */
const {nick,avatar} = await tls.like(extension);
```

### gift(extension?:string)

이 메소드는 호스트에게 선물주기에 사용됩니다.

> extension: 선물 보내기 부가 정보(예: 선물 정보 등)

```javascript
/**
 * 이 메소드를 호출하여 호스트에게 선물주기 메시지를 발송하면 그룹의 모든 사용자가 이 선물 메시지를 받을 수 있습니다.
 * @method gift
 * @for TLS
 * @param msg 선택 입력. 선물 보내기 부가 정보.
 * @returns Promise
 */
const {nick,avatar} = await tls.gift(extension);
```

### exitRoom()

이 메소드는 라이브 룸 퇴장에 사용됩니다.

```javascript
/**
 * 호스트(그룹 소유자)는 라이브 룸을 나갈 수 없습니다.
 * @method exitRoom
 * @for TLS
 * @param 
 * @returns Promise
 */
const {status} = await tls.exitRoom();
```

### joinRoom()

이 메소드는 라이브 룸 입장에 사용됩니다.

```javascript
/**
 * 라이브 룸 입장
 * @method joinRoom
 * @for TLS
 * @param 
 * @returns Promise
 */
const {userInfo,groupInfo} = await tls.joinRoom();
const { ownerInfo } = groupInfo;//호스트 정보 가져오기
const { userID,nick,avatar } = ownerInfo
```

### getRoomInfo()

이 메소드는 라이브 룸 정보 가져오기에 사용됩니다.

```javascript
/**
 * 라이브 룸에 대한 기본 정보 가져오기.
 * @method getRoomInfo
 * @for TLS
 * @param 
 * @returns Promise
 */
const {...ownerInfo} = await tls.getRoomInfo();
//ownerInfo: 호스트 관련 정보
const { userID,nick,avatar } = ownerInfo
```

### attention()

이 메소드는 호스트 팔로우에 사용됩니다.

```javascript
/**
 * 호스트 팔로우
 * @method attention
 * @for TLS
 * @param 
 * @returns Promise
 */
const {nick,avatar} = await tls.attention();
```

### cancelAttention()

이 메소드는 호스트 언팔로우에 사용됩니다.

```javascript
/**
 * 언팔로우
 * @method cancelAttention
 * @for TLS
 * @param 
 * @returns Promise
 */
const {nick,avatar} = await tls.cancelAttention();
```

### destroy()

이 메소드는 컴포넌트 폐기에 사용됩니다.

```javascript
/**
 * 컴포넌트 폐기
 * @method destroy
 * @for TLS
 * @param 
 * @returns Promise
 */
tls.destroy(); 
```

### sendCustomMsgAndEmitEvent(eventName: string, extension?: string)

이 메소드는 사용자 지정 메시지를 보내고, type 유형의 콜백 이벤트를 트리거하는 데 사용됩니다.

>
> - eventName: 이벤트 이름.
> - extension: 사용자 정의 메시지 발송자 부가 정보.

```javascript
/**
 * 사용자 정의 메시지 발송, 같은 이름의 이벤트 트리거
 * @method destroy
 * @for TLS
 * @param eventName: 이벤트 이름. someExtension: 부가 정보
 * @returns Promise
 */
await tls.sendCustomMsgAndEmitEvent('eventName','someExtension')
```

## 빌트인 객체

빌트인 객체는 TIM이 `TIM.create`을 통해 생성하며, 모든 TIM 메소드를 사용할 수 있습니다. 

## 이벤트

| EVENT                                                 | 설명                                                         |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| [TLS.EVENT.SDK_READY](#tls.event.sdk_ready)           | 이 이벤트는 컴포넌트 초기화가 완료되면 트리거됩니다. 이 이벤트는 IM SDK의 `TIM.EVENT.SDK_READY`에 해당합니다. 이 이벤트가 트리거된 후에만 SDK 메소드를 호출할 수 있습니다. |
| [TLS.EVENT.JOIN_GROUP](#tls.event.join_group)         | 누군가가 그룹에 입장하면 트리거됨.                                         |
| [TLS.EVENT.EXIT_GROUP](#tls.event.join_group)         | 누군가가 그룹에서 퇴장하면 트리거됨.                                         |
| [TLS.EVENT.NOTIFACATION](#tls.event.notifacation)     | 알림에 변경 발생 시 트리거됨.                                         |
| [TLS.EVENT.MESSAGE](#tls.event.message)               | 누군가가 그룹 메시지를 발송하면 트리거됨.                                       |
| [TLS.EVENT.PROFILE_UPDATE](#tls.event.profile_update) | 개인 정보가 수정되면 트리거됨.                                     |
| [TLS.EVENT.ERROR](#tls.event.error)                   | SDK에 오류 발생 시 트리거됨.                                         |
| [TLS.EVENT.KICKED](#tls.event.kicked)                 | 계정이 다른 장소에서 로그인되면 트리거됨.                                     |
| [TLS.EVENT.NETWORK_CHANGE](#tls.event.network_change) | 네트워크 변경 발생 시 트리거됨.                                         |
| [TLS.EVENT.SDK_NOT_READY](#tls.event.sdk_not_ready)   | SDK 사용 불가 시 트리거됨.                                           |
| [TLS.EVENT.LIKE](#tls.event.like)                     | 누군가가 호스트 좋아요를 누르면 트리거됨.                                       |
| [TLS.EVENT.BUY_GOODS](#tls.event.buy_goods)           | 누군가가 상품을 구매하면 트리거됨.                                         |
| [TLS.EVENT.SEND_GIFT](#tls.event.send_gift)           | 누군가가 호스트에게 선물하기하면 트리거됨.                                       |
| [TLS.EVENT.ATTENT](#tls.event.attent)                 | 누군가가 호스트를 팔로우하면 트리거됨.                                         |
| [TLS.EVENT.ADD_GOODS](#tls.event.add_goods)           | 라이브 방송에서 추천한 상품에 변동 발생 시 트리거됨.                         |
| [TLS.EVENT.USE_COUPON](#tls.event.use_coupon)         | 누군가가 바우처를 수령하면 트리거됨.                                        |

