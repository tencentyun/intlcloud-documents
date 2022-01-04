IM 라이브 방송 그룹(AVChatRoom)은 다음과 같은 특징이 있습니다.
-**인원 제한이 없으며, 천만 규모의 인터랙티브 라이브 방송 시나리오를 구현할 수 있습니다**.
- 모든 온라인 사용자 대상 푸시 메시지(그룹 시스템 알림)를 지원합니다.
- Web 및 WeChat 미니프로그램을 사용하여 로그인 하지 않고 게스트 신분으로 메시지를 수신할 수 있습니다. 
- 그룹 참여 신청 후 관리자의 승인 없이 바로 참여할 수 있습니다.

>?본문은 Web 및 WeChat 미니프로그램 SDK를 예로 들며, 다른 단말의 SDK 구현 프로세스는 이와 대동소이합니다.

## 적용 시나리오

#### 라이브 방송 댓글 자막
 AVChatRoom은 댓글 자막, 선물하기, 좋아요 등 다양한 메시지 유형을 지원하며 우수한 라이브 채팅 인터랙션 체험을 간편 구현합니다. 댓글 자막 콘텐츠 심사 기능을 제공하여, 귀하의 라이브 방송을 불건전 언어로부터 보호합니다.
#### 인플루언서(왕홍) 라이브 커머스
 AVChatRoom과 비즈니스 라이브 방송을 결합하여 좋아요, 가격 문의, 바우처와 같은 특정 메시지 유형을 제공하여 트래픽 수익 창출을 돕습니다.

#### 강의 화이트보드 
 AVChatRoom은 온라인 강의, 텍스트 메시지, 펜 등의 기능을 제공하여, 교사-학생 커뮤니케이션, 필기 기록 저장, ​​대규모 강의 및 소규모 강의와 같은 교육 시나리오를 손쉽게 구현합니다.

## 사용 제한
-[메시지 회수](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#revokeMessage)는 지원되지 않습니다.
- 그룹 소유자는 그룹에서 퇴장할 수 없으며, 그룹을 해산해야만 그룹에서 탈퇴할 수 있습니다.
- 그룹 구성원 제거는 지원되지 않습니다.


## 관련 문서
- [그룹 관리](https://intl.cloud.tencent.com/document/product/1047/33530)
- [그룹 시스템](https://intl.cloud.tencent.com/document/product/1047/33529)
- [SDK 다운로드](https://intl.cloud.tencent.com/document/product/1047/33996)
- [로그 업데이트(Web&미니프로그램)](https://intl.cloud.tencent.com/document/product/1047/34281)
- [SDK 매뉴얼](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/TIM.html)
- [SDK 통합(Web&미니프로그램)](https://intl.cloud.tencent.com/document/product/1047/34309)
- [초기화 및 로그인(Web&미니프로그램)](https://intl.cloud.tencent.com/document/product/1047/34314)
- [메시지 수발신(Web&미니프로그램)](https://intl.cloud.tencent.com/document/product/1047/34322)
- [그룹 관리(Web&미니프로그램)](https://intl.cloud.tencent.com/document/product/1047/34330)

## 사용 안내
<span id="Step1"></span>
### 1단계: 애플리케이션 생성

1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인합니다.
 >? 이미 애플리케이션이 있는 경우 SDKAppID를 기록하고 [2단계](#step2)를 실행합니다.
 >동일한 Tencent Cloud 계정으로 최대 300개의 IM 애플리케이션을 만들 수 있습니다. 이미 300개의 애플리케이션이 있는 경우 신규 애플리케이션 생성 전에 사용하지 않는 애플리케이션을 [비활성화 및 삭제](https://intl.cloud.tencent.com/document/product/1047/34540)합니다. **애플리케이션 삭제 후에는 SDKAppID에 해당하는 모든 데이터 및 서비스를 복구할 수 없으므로 주의하시기 바랍니다. **
 >
2. [신규 애플리케이션 추가]를 클릭합니다.
3. [애플리케이션 생성] 대화 상자에서 애플리케이션 이름을 입력한 후 [확인]을 클릭합니다. 애플리케이션 생성 완료 후, 콘솔 전체보기 페이지에서 새로 생성된 애플리케이션의 상태, 서비스 버전, SDKAppID, 생성 시간 및 만료 시간을 확인할 수 있습니다.
4. 애플리케이션의 SDKAppID를 기록해둡니다.

<span id="Step2"></span>
### 2단계: AVChatRoom 생성
콘솔을 통해 그룹을 생성할 수 있고, [그룹 생성 API](https://intl.cloud.tencent.com/document/product/1047/34895) 호출을 통해 그룹을 생성할 수도 있습니다. 본문에서는 콘솔을 통해 그룹을 생성합니다.


1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인하여 대상 애플리케이션 카드를 클릭합니다.
2. 왼쪽 사이드바에서 [그룹 관리]를 선택하고, [그룹 추가]를 클릭합니다.
3. 그룹 이름을 입력하고, 그룹 소유자 ID(선택 사항)를 입력한 후 [그룹 유형]을 [라이브 방송 그룹]으로 선택합니다.
4. [확인]을 클릭하고 그룹이 성공적으로 생성된 후 [그룹 ID]를 기록해둡니다(본문은 `@TGS#aC72FIKG3`을 예로 듦).


<span id="Step3"></span>
### 3단계: SDK 통합
NPM 또는 Script를 통해 SDK를 통합할 수 있으며, NPM 통합 사용을 권장합니다. 이 문서에서는 NPM 통합을 예로 듭니다.

-  Web 프로젝트
```javascript
// Web 프로젝트
npm install tim-js-sdk --save-dev
```
-  미니프로그램 프로젝트
```javascript
// WeChat 미니프로그램 프로젝트
npm install tim-wx-sdk --save-dev
```

>?동기화 종속성 프로세스 중 문제가 발생하면 npm 소스를 전환하고 다시 시도하십시오.
```
// cnpm 소스 전환
npm config set registry http://r.cnpmjs.org/
```

<span id="Step4"></span>
### 4단계: SDK 인스턴스 생성

<pre><code><span class="hljs-comment">// SDK 인스턴스 생성. TIM.create() 메소드는 SDKAppID에 동일한 인스턴스만 반환합니다.</span>
<span class="hljs-keyword">let</span> options = {
  SDKAppID: <span class="hljs-number">0</span> <span class="hljs-comment">// 연결 시 0을 IM 애플리케이션의 SDKAppID로 바꿉니다.</span>
}
<span class="hljs-keyword">let</span> tim = TIM.create(options) <span class="hljs-comment">// SDK 인스턴스는 일반적으로 tim으로 표시됩니다.</span>
<span class="hljs-comment">// SDK 로깅 레벨을 설정합니다. 자세한 내용은 <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html?_ga=1.43970405.1562552652.1542703643#setLogLevel">setLogLevel 인터페이스의 설명을 참고하십시오.</a></span>
tim.setLogLevel(<span class="hljs-number">0</span>) <span class="hljs-comment">// 일반 레벨. 연결 시 이 레벨을 사용하시길 권장합니다.</span>

tim.<span class="hljs-keyword">on</span>(TIM.EVENT.SDK_READY, function (<span class="hljs-keyword">event</span>) {
  <span class="hljs-comment">// SDK ready 후 액세스 측에서 sendMessage 등 인증이 필요한 인터페이스를 호출할 수 있습니다. 그렇지 않으면 실패 메시지가 표시됩니다!</span>
  <span class="hljs-comment">// event.name - TIM.EVENT.SDK_READY</span>
})

tim.<span class="hljs-keyword">on</span>(TIM.EVENT.MESSAGE_RECEIVED, function(<span class="hljs-keyword">event</span>) {
  <span class="hljs-comment">// 1:1 채팅, 그룹 채팅, 그룹 프롬프트, 그룹 시스템 알림의 새 푸시 메시지 수신. event.data를 탐색하여 메시지 목록 데이터를 가져와 페이지에 렌더링할 수 있습니다.</span>
  <span class="hljs-comment">// event.name - TIM.EVENT.MESSAGE_RECEIVED</span>
  <span class="hljs-comment">// event.data - Message 객체를 저장할 배열 - [Message]</span>
  <span class="hljs-keyword">const</span> length = <span class="hljs-keyword">event</span>.data.<span class="hljs-function">length
  <span class="hljs-keyword">let</span> message
  <span class="hljs-title">for</span> (<span class="hljs-params"><span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i &lt; length; i++</span>)</span> {
    <span class="hljs-comment">// Message 인스턴스의 자세한 데이터 구조는 <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html">Message를 참고하십시오.</a></span>
    <span class="hljs-comment">// type 및 payload 속성에 주의를 기울여야 합니다.</span>
    <span class="hljs-comment">// v2.6.0부터 AVChatRoom 내 그룹 채팅 메시지, 그룹 입장 및 퇴장 알림 메시지에 nick(닉네임) 및 avatar(프로필 사진 URL) 속성이 추가되어, 액세스측에서 더 나은 디스플레이 경험을 제공할 수 있게 되었습니다.</span>
    <span class="hljs-comment">// 이를 위해, 먼저 updateMyProfile을 호출하여 자신의 nick(닉네임) 및 avatar(프로필 사진 URL)을 설정하십시오. <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateMyProfile">updateMyProfile 인터페이스의 설명을 참고하십시오.</a></span>
    message = <span class="hljs-keyword">event</span>.data[i]
    <span class="hljs-keyword">switch</span> (message.type) {
      <span class="hljs-keyword">case</span> TIM.TYPES.MSG_TEXT:
        <span class="hljs-comment">// 텍스트 메시지 수신</span>
        <span class="hljs-keyword">this</span>._handleTextMsg(message)
        <span class="hljs-keyword">break</span>
      <span class="hljs-keyword">case</span> TIM.TYPES.MSG_CUSTOM:
        <span class="hljs-comment">// 사용자 정의 메시지 수신</span>
        <span class="hljs-keyword">this</span>._handleCustomMsg(message)
        <span class="hljs-keyword">break</span>
      <span class="hljs-keyword">case</span> TIM.TYPES.MSG_GRP_TIP:
        <span class="hljs-comment">// 구성원 그룹 입/퇴장 등 그룹 알림 메시지 수신</span>
        <span class="hljs-keyword">this</span>._handleGroupTip(message) 
        <span class="hljs-keyword">break</span>
      <span class="hljs-keyword">case</span> TIM.TYPES.MSG_GRP_SYS_NOTICE:
        <span class="hljs-comment">// 그룹 시스템 알림 수신. REST API를 통해 그룹에 전송된 시스템 알림은 <a href="https://intl.cloud.tencent.com/document/product/1047/34958">그룹에서 시스템 알림 메시지 발송 API를 참고하십시오.</a></span>
        <span class="hljs-keyword">this</span>._handleGroupSystemNotice(message)
        <span class="hljs-keyword">break</span>
      <span class="hljs-keyword">default</span>:
         <span class="hljs-keyword">break</span>
    }
  }
})

_handleTextMsg(message) {
  <span class="hljs-comment">// 자세한 데이터 구조는 <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.TextPayload">TextPayload 인터페이스의 설명을 참고하십시오.</a></span>
  console.log(message.payload.text) <span class="hljs-comment">// 텍스트 메시지 내용</span>
}

_handleCustomMsg(message) {
  <span class="hljs-comment">// 자세한 데이터 구조는 <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.CustomPayload">CustomPayload 인터페이스의 설명을 참고하십시오.</a></span>
  console.log(message.payload)
}

_handleGroupTip(message) {
  <span class="hljs-comment">// 자세한 데이터 구조는 <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload">GroupTipPayload 인터페이스의 설명을 참고하십시오.</a></span>
  <span class="hljs-keyword">switch</span> (message.payload.operationType) {
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_JOIN: <span class="hljs-comment">// 그룹에 참여한 사용자가 있음</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_QUIT: <span class="hljs-comment">// 그룹에서 퇴장한 사용자가 있음</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_KICKED_OUT: <span class="hljs-comment">// 내보내기된 구성원이 있음</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_SET_ADMIN: <span class="hljs-comment">// 관리자가 된 구성원이 있음</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_CANCELED_ADMIN: <span class="hljs-comment">// 관리자 해제된 구성원이 있음</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_GRP_PROFILE_UPDATED: <span class="hljs-comment">// 그룹 정보가 변경됨</span>
      <span class="hljs-comment">//v2.6.0부터 그룹 사용자 정의 필드 변경 지원</span>
      <span class="hljs-comment">// message.payload.newGroupProfile.groupCustomField </span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">case</span> TIM.TYPES.GRP_TIP_MBR_PROFILE_UPDATED: <span class="hljs-comment">// 그룹 구성원 정보가 변경됨(예: 음소거 처리됨)</span>
      <span class="hljs-keyword">break</span>
    <span class="hljs-keyword">default</span>:
      <span class="hljs-keyword">break</span>
  }
}

_handleGroupSystemNotice(message) {
  <span class="hljs-comment">// 자세한 데이터 구조는  <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload">GroupSystemNoticePayload 인터페이스의 설명을 참고하십시오.</a></span>
  console.log(message.payload.userDefinedField) <span class="hljs-comment">// 사용자 정의 필드. RESTAPI를 사용하여 그룹 시스템 알림을 보낼 때 이 속성 값에서 사용자 정의 알림의 내용을 가져올 수 있습니다.</span>
  <span class="hljs-comment">// REST API를 사용하여 그룹 시스템 알림을 보내는 방법에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/34958">그룹에서 시스템 알림 메시지 발송 API를 참고하십시오.</a></span>
}</code></pre>

<span id="Step5"></span>
### 5단계: SDK 로그인

```javascript
let promise = tim.login({userID: 'your userID', userSig: 'your userSig'});
promise.then(function(imResponse) {
  console.log(imResponse.data); // 로그인 성공
}).catch(function(imError) {
  console.warn('login error:', imError); // 로그인 실패 관련 정보
});
```

<span id="Step6"></span>
### 6단계: 닉네임 및 프로필 사진 설정
v2.6.0 이후 SDK 버전부터 AVChatRoom 내 그룹 채팅 메시지 및 그룹 알림 메시지(예: 그룹 입/퇴장 등) 에 nick(닉네임) 및 avatar(프로필 사진 URL) 속성이 추가되었습니다. [updateMyProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateMyProfile) 인터페이스를 호출하여 자신의 nick(닉네임) 및 avatar(프로필 사진 URL)를 설정할 수 있습니다.

```javascript
// v2.6.0부터 AVChatRoom 내 그룹 채팅 메시지, 그룹 입장 및 퇴장 알림 메시지에 nick(닉네임) 및 avatar(프로필 사진 URL) 속성이 추가되어, 액세스측에서 더 나은 디스플레이 경험을 제공할 수 있게 되었습니다. 이를 위해, 먼저 updateMyProfile을 호출하여 개인 정보를 설정하십시오.
// 개인 표준 프로필을 수정합니다.
let promise = tim.updateMyProfile({
  nick: '나의 닉네임',
  avatar: 'http(s)://url/to/image.jpg'
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // 정보 업데이트 완료
}).catch(function(imError) {
  console.warn('updateMyProfile error:', imError); // 정보 업데이트 실패 관련 정보
});
```

<span id="Step7"></span>
### 7단계: 그룹 참여
```javascript
// 익명 사용자 참여(로그인 필요 없음, 그룹 참여 후 메시지 수신만 가능)
let promise = tim.joinGroup({ groupID: 'avchatroom_groupID'});
promise.then(function(imResponse) {
  switch (imResponse.data.status) {
    case TIM.TYPES.JOIN_STATUS_WAIT_APPROVAL: // 관리자 승인 대기 중
      break
    case TIM.TYPES.JOIN_STATUS_SUCCESS: // 참여 성공
      console.log(imResponse.data.group) // 참여한 그룹 정보
      break
    case TIM.TYPES.JOIN_STATUS_ALREADY_IN_GROUP: // 이미 그룹에 있음
      break
    default:
      break
  }
}).catch(function(imError){
  console.warn('joinGroup error:', imError) // 그룹 참여 신청 실패 관련 정보
});
```

### 8단계: 메시지 인스턴스 생성 및 메시지 발송
본문은 텍스트 메시지 발송을 예로 듭니다.

<pre><code class="language-javascript"><span class="hljs-comment">// 텍스트 메시지 발송. Web은 미니프로그램과 동일</span>
<span class="hljs-comment">// 1. 메시지 인스턴스 생성. 인터페이스에서 반환된 인스턴스를 화면에 표시할 수 있습니다.</span>
<span class="hljs-keyword">let</span> message = tim.createTextMessage({
  <span class="hljs-attr">to</span>: <span class="hljs-string">'avchatroom_groupID'</span>,
  <span class="hljs-attr">conversationType</span>: TIM.TYPES.CONV_GROUP,
  <span class="hljs-comment">// 메시지 우선 순위. 그룹 채팅에 사용됨(v2.4.2부터 지원됨). 그룹의 메시지가 빈도 제한을 초과하면 백그라운드에서 우선순위가 높은 메시지를 우선적으로 처리합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/1047/33526">메시지 우선순위 및 빈도 제어를 참고하십시오.</a></span>
  <span class="hljs-comment">// 유효 값: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL(디폴트), TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST</span>
  <span class="hljs-attr">priority</span>: TIM.TYPES.MSG_PRIORITY_NORMAL,
  <span class="hljs-attr">payload</span>: {
    <span class="hljs-attr">text</span>: <span class="hljs-string">'Hello world!'</span>
  }
})
<span class="hljs-comment">// 2. 메시지 발송</span>
<span class="hljs-keyword">let</span> promise = tim.sendMessage(message)
promise.then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imResponse</span>) </span>{
  <span class="hljs-comment">// 발송 성공</span>
  <span class="hljs-built_in">console</span>.log(imResponse)
}).catch(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">imError</span>) </span>{
  <span class="hljs-comment">// 발송 실패</span>
  <span class="hljs-built_in">console</span>.warn(<span class="hljs-string">'sendMessage error:'</span>, imError)
})</code></pre>


## FAQ

### 1. 발송한 'Message.nick', 'Message.avatar' 메시지가 모두 비어 있습니다. 어떻게 해야 인터페이스에 닉네임과 프로필 사진이 정상적으로 표시됩니까?

[getMyProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getMyProfile) 호출을 통해 닉네임과 프로필 사진을 가져오기할 수 있습니다.

### 2. 라이브 방송 그룹에서 음소거 기능은 어떻게 구현합니까?

음소거(발언 금지) 기능은 사용자 정의 메시지를 통해 구현될 수 있으며, 사용자 정의 메시지에 음소거 대상 Members_Account, 음소거 시간이 포함되어 있어야 합니다. [그룹 내 발언 전 콜백](https://intl.cloud.tencent.com/document/product/1047/34374)을 통해 해당 사용자 정의 메시지를 비즈니스 백엔드에 발송하고, 비즈니스 백엔드에서 [일괄 음소거 및 음소거 취소](https://intl.cloud.tencent.com/document/product/1047/34951) 인터페이스를 호출하여 지정 사용자에 대한 음소거 기능을 구현할 수 있습니다.

### 3. 라이브 방송 그룹에서 내보내기 기능은 어떻게 구현합니까?

내보내기 기능은 사용자 정의 메시지를 통해 구현할 수 있으며, 사용자 정의 메시지에는 내보내기 대상자의 Members_Account가 포함되어 있어야 합니다. 해당 메시지의 우선순위를 High로 설정하여, 메시지 빈도 제한(40개/초)에 걸려 백엔드로부터 폐기되지 않도록 합니다. 내보내기 대상자 SDK가 해당 메시지를 수신한 후, [kickGroupMember](https://intl.cloud.tencent.com/document/product/1047/36169) API를 호출하여 라이브 방송 그룹에서 내보내기 기능을 구현합니다.
<span id="p4"></span>
### 4. 미니프로그램/Web에서 그룹 퇴장 API를 호출하면, Android/iOS/PC에서도 동시에 그룹 퇴장되는데, 반대로 Android/iOS/PC에서 그룹 퇴장 API를 호출하면 미니프로그램/Web에서는 그룹 퇴장이 되지 않는 이유는 무엇입니까?

미니프로그램/Web은 사용자가 게스트 신분으로 액세스하는 것을 허용하기 때문에, Android/iOS/PC에서 그룹 퇴장한 후에도 미니프로그램/Web에서는 그룹 퇴장 작업이 자발적으로 트리거되지 않습니다.

-모든 클라이언트단에서 동기화된 그룹 퇴장을 구현하려면, [그룹 구성원 퇴장 후 콜백](https://intl.cloud.tencent.com/document/product/1047/34373) 을 구성하고, OptPlatform 필드를 통해 퇴장 플랫폼을 판단합니다. 퇴장 플랫폼이 Android/iOS/PC인 경우, [1:1 채팅 메시지 발송](https://intl.cloud.tencent.com/document/product/1047/34919) API를 호출하여 시스템 메시지 방식으로 그룹 퇴장 구성원에게 사용자 정의 메시지를 발송하면 프론트 엔드는 대화를 차단하고 UI에 표시하지 않습니다. 미니프로그램/Web은 해당 메시지를 수신한 후, [quitGroup](https://intl.cloud.tencent.com/document/product/1047/33999) API를 호출합니다.
- 단일 클라이언트 퇴장을 구현하려면, [그룹 구성원 퇴장 후 콜백](https://intl.cloud.tencent.com/document/product/1047/34373)을 구성하고, OptPlatform 필드를 통해 퇴장 플랫폼을 판단한 후, [1:1 채팅 메시지 발송](https://intl.cloud.tencent.com/document/product/1047/34919) API를 호출하여 시스템 메시지 방식으로 그룹 퇴장 구성원에게 사용자 정의 메시지를 발송하면 프론트 엔드는 대화를 차단하고 UI에 표시하지 않습니다. 퇴장하지 않는 플랫폼은 해당 메시지를 수신한 후, [joinGroup](https://intl.cloud.tencent.com/document/product/1047/36169) API를 호출하여 그룹에 입장합니다. 그룹 입/퇴장 대한 시스템 알림을 중단하려면, 티켓을 제출하여 그룹 입/퇴장 시스템 알림을 비활성화할 수 있습니다.

### 5. 메시지가 손실되는 원인은 무엇입니까?

메시지가 손실되는 가능한 원인은 다음과 같습니다.

- 라이브 방송 그룹의 메시지 전송 빈도 제한은 초당 40개입니다. 메시지 발송 전/후 콜백을 통해 빈도 제한으로 인한 메시지 폐기 여부를 판단할 수 있습니다. 메시지가 그룹 메시지 발송 전 콜백을 수신하지만 발송 후 콜백은 수신하지 않는 경우, 해당 메시지는 빈도 제한에 걸린 것입니다.
- 미니프로그램/Web단에서의 그룹 퇴장으로 인하여 Android/iOS/PC에서 퇴장이 되었는지에 대한 판단은 [FAQ 4](#p4)를 참고하시기 바랍니다.
- 미니프로그램/Web에 문제가 있는 경우, 사용 중인 SDK 버전을 확인하고 V2.7.6 이전 버전이면 최신 버전으로 업그레이드 하시기 바랍니다.

상기 원인에 해당되지 않는 경우, 티켓 제출을 통해 문의주시기 바랍니다.

### 6. 좋아요/팔로우 수는 어떻게 알 수 있습니까?

먼저 사용자 정의 메시지를 통해 좋아요/팔로우 메시지 유형을 생성합니다. 사용자가 프론트 엔드의 좋아요/팔로우 icon을 클릭하여 사용자 정의 메시지 전달을 트리거하면, 좋아요/팔로우 메시지는 [그룹 내 발언 전 콜백](https://intl.cloud.tencent.com/document/product/1047/34374)을 통해 비즈니스 측에 전달됩니다. 비즈니스 측은 수신된 좋아요/팔로우 메시지 수를 합산하여 3초~5초마다 [그룹 기본 정보 수정](https://intl.cloud.tencent.com/document/product/1047/34962) API를 통해 해당 데이터를 그룹 정보 필드에 업데이트하고, SDK는 [getGroupsInfo](https://intl.cloud.tencent.com/document/product/1047/36169) API를 통해 좋아요/팔로우 수를 통계합니다.

### 7. 메시지 우선순위를 합리적으로 설정하는 방법은 무엇입니까?

라이브 방송 그룹은 중요한 메시지가 폐기되는 것을 방지하기 위해 모든 메시지에 대해 3가지 우선순위 옵션을 제공합니다. SDK는 우선순위가 높은 메시지를 먼저 받게 되며, 사용자 지정 메시지 우선 순위 설정에 대한 권장 방법은 다음과 같습니다.

- High: 홍바오, 선물, 내보내기 메시지.
- Normal: 일반 텍스트 메시지.
- Low: 좋아요, 팔로우 메시지.

### 8. 영상 시청과 채팅에 바로 사용이 가능한 라이브 방송 오픈 소스 컴포넌트가 있습니까?

있습니다. 코드 또한 오픈 소스입니다. 자세한 사항은 [Tencent Cloud TWebLive](https://github.com/tencentyun/TWebLive)를 참고하십시오.



