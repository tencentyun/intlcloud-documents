trtc-electron-education 모듈은 실시간 인터랙션 강의실 시나리오에 초점을 맞춰 TRTC와 IM 기능을 이용한 2차 캡슐 모듈입니다. 해당 캡슐은 기본적인 멀티미디어 채팅, 화면 공유 기능 뿐만 아니라 온라인 교육 시나리오에 특화된 교사 질답 시작, 학생 손 들기, 교사 답변 요청, 답변 완료 등 관련 기능이 캡슐화되어 있습니다.
trtc-electron-education은 오픈 소스 npm 모듈로, Tencent Cloud의 두 가지 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 방법은 [실시간 인터랙션 강의실(Electron)](https://intl.cloud.tencent.com/document/product/647/37278)을 참조하십시오.
* TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647)를 사용하는 저 딜레이 영상 통화 모듈입니다.
* IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047)를 사용하여 신호 정보를 발송 및 처리합니다.

## 모듈 액세스
```
// yarn 방식 가져오기
yarn add trtc-electron-education
// npm 방식 가져오기
npm i trtc-electron-education --save
```

## 모듈 매개변수

필수 작성 매개변수는 다음과 같습니다.

| 매개변수 |유형|설명|
| ----- | ----- | ----- |
|sdkAppId|number|필수 작성 매개변수입니다. <a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.|
|userID|string|필수 작성 매개변수입니다. 사용자 ID로, 귀하의 계정 시스템에서 지정할 수 있습니다.|
|userSig|string|필수 작성 매개변수입니다. 자격 서명(로그인 비밀번호에 해당)으로, userID에서 계산하여 획득합니다. 자세한 계산 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.|

## 초기화 예시

```typescript
import TrtcElectronEducation from 'trtc-electron-education';
const rtcClient = new TrtcElectronEducation({
     sdkAppId: 1400***803,
     userID: '123'
     userSig: 'eJwtzM9****-reWMQw_'
 });
```

## 모듈 개요
### 기본 함수

#### on(EventCode, handler, context)
리스너 모듈에서 배포하는 이벤트에 사용됩니다.  
매개변수:

|매개변수 이름|	유형	|설명|
| ----- | ----- | ----- |
|EventCode|	String|	이벤트 코드|
|handler|	Function|	리스너 함수|
|context|	Object|	현재 실행 중인 콘텍스트 |

예시:
```typescript
const EVENT = rtcClient.EVENT
rtcClient.on(EVENT.MESSAGE_RECEIVED, onMessageReceived);
```

#### off(EventCode, handler)
리스너 취소 이벤트  
매개변수:

|매개변수 이름|	유형	|설명|
| ----- | ----- | ----- |
|EventCode|	String|이벤트 코드|
|handler|	Function|취소할 서명 리스너 함수|

예시:
```typescript
const EVENT = rtcClient.EVENT
rtcClient.off(EVENT.MESSAGE_RECEIVED, onMessageReceived);
```

[](id:createRoom)
#### createRoom(params: CreateRoomParams)
교사의 강의실 생성  
매개변수:

|매개변수 이름|	유형	|설명|
| ----- | ----- | ----- |
|classId|	number|	강의실 ID|
|nickName|	string|	닉네임|
|avatar|	string|	프로필 사진 주소, 선택 입력 사항|

예시:
```typescript
interface CreateRoomParams {
  classId: number; // 강의실 ID
  nickName: string; // 닉네임
  avatar?:string; // 프로필 사진 주소
}
rtcClient.createRoom(params).then(() => {
})
```

#### destroyRoom(classId: number)
교사 강의실 퇴장 시, 강의실 폐기
매개변수:

|매개변수 이름|	유형	| 설명|
| ----- | ----- | ----- |
|classId|	number|	 강의실 ID|

예시:
```typescript
rtcClient.destroyRoom(classId)
```

[](id:enterRoom)
#### enterRoom(params: EnterRoomParams)
교사가 수업을 시작하고 학생이 강의실에 입장하여 수업 준비
매개변수:

|매개변수 이름|	유형	| 설명|
| ----- | ----- | ----- |
|classId|	number|	 강의실 ID|
|nickName|	string| 닉네임|
|role|	string|	 역할. teacher: 교사, student: 학생|
|avatar|	string|	프로필 사진 주소, 선택 입력 사항|

예시:
```typescript
interface EnterRoomParams {
  role: string; // 역할
  classId: number; // 강의실 ID
  nickName?: string; // 닉네임
  avatar?:string; // 프로필 사진 주소
}
rtcClient.enterRoom(params).then(() => {
})
```

#### exitRoom(role:string, classId: number)
교사가 수업을 종료하고 학생들 강의실 퇴장
매개변수:

|매개변수 이름|	유형	| 	설명|
| ----- | ----- | ----- |
|classId|	number|	 강의실 ID|
|role|	string| 역할. teacher: 교사, student: 학생|

예시:
```typescript
rtcClient.exitRoom(role, classId);
```

### 손 들기 프로세스 함수
<span id="startQuestionTime"></span>
#### startQuestionTime(classId: number)
교사가 질답 시간을 시작하면 교사 측에서 공지가 발송되고, 학생이 질답 이벤트를 수신하면 손 들기 기능이 활성화됩니다. 
매개변수:

|매개변수 이름|	유형	| 설명|
| ----- | ----- | ----- |
|classId|	number|	 강의실 ID|

예시:
```typescript
rtcClient.startQuestionTime(classId)
```

[](id:raiseHand)
#### raiseHand()
학생이 손 들기를 하면, 학생 측에서 손 들기를 통지하고 교사 측에서 학생의 손 들기 알림을 수신합니다.  
매개변수: 없음
예시:
```typescript
rtcClient.raiseHand()
```

[](id:inviteToPlatform)
#### inviteToPlatform(userID: string)
교사가 학생의 답변을 요청하면 교사 측은 손 들기 리스트에서 학생의 userID를 선택하여 요청 알림을 발송하고, 학생 측에서 답변 요청 이벤트를 수신한 후 수락하면 학생의 마이크가 켜집니다. 손 들기를 한 학생이 없을 경우 교사는 직접 답변할 학생을 직접 지목할 수 있으며, 학생 측에서 답변 요청 이벤트를 수신하면 지목된 학생의 마이크가 켜집니다.
매개변수:

|매개변수 이름|	유형	|설명|
| ----- | ----- |  ----- |
|userID|	string| 사용자 ID|

예시:
```typescript
rtcClient.inviteToPlatform(userID).then(() => {
})
```

[](id:finishAnswering)
#### finishAnswering(userID: string)
답변이 끝나면 교사 측에서 학생 측의 답변을 종료하고, 학생이 답변 종료 알림을 수신하면 지정한 학생의 마이크 연결이 종료됩니다.
매개변수:

|매개변수 이름|	유형	| 설명|
| ----- | ----- |   ----- |
|userID|	string|	 사용자 ID|

예시:
```typescript
rtcClient.finishAnswering(userID).then(() => {
})
```

#### stopQuestionTime(classId: number)
질문 시간 종료 시 교사 측에서 질답 시간을 종료하면 학생 측에서 질답 시간 종료 알림을 수신합니다. 마이크가 연결된 학생이 마이크 연결을 종료하고 싶은 경우 손 들기 기능을 끕니다.
매개변수:

|매개변수 이름|	유형	|설명|
| ----- | ----- | ----- |
|classId|	number|	강의실 ID|

예시:
```typescript
rtcClient.stopQuestionTime(classId)
```

### 푸시/풀 스트림 작업 관련 함수
[](id:getScreenShareList)
#### getScreenShareList()
화면 공유 창 리스트 획득
매개변수: 없음
예시:
```typescript
rtcClient.getScreenShareList();
```


[](id:startScreenCapture)
#### startScreenCapture(source: SourceParam)
화면 공유를 선택하면 푸시 스트림이 시작됩니다.
매개변수:

|매개변수 이름|	유형	|설명|
| ----- | ----- | ----- |
|type|	number|	수집 소스 유형|
|sourceId|string|	수집 소스 ID. 해당 필드는 창에서 창 핸들 의미, 화면에서는 화면 ID 의미|
|sourceName|string|수집 소스 이름, UTF8 인코딩|

예시:
```typescript
interface SourceParam {
  type: number; // 수집 소스 유형
  sourceId: string; // 수집 소스 ID
  sourceName: string; // 수집 소스 이름, UTF8 인코딩
}
rtcClient.startScreenCapture({
   type,
   sourceId,
   sourceName
 })
```

[](id:startRemoteView)
#### startRemoteView(params: RemoteParams) 
원격 비디오 화면 또는 화면 공유 화면 표시 시작
매개변수:

|매개변수 이름|	유형	| 설명|
| ----- | ----- |  ---- |
|userID|	string|	 사용자 ID|
|streamType|number|	 화면 유형. 1: 대형 화면, 2: 소형 화면, 3: 화면 공유|
|view|HTMLElement|	 화면 표시 DOM|

예시:
```typescript
interface RemoteParams {
  userID: string; // 사용자 ID
  streamType: number; // 화면 유형. 1 - 대형 화면, 2 - 소형 화면, 3 - 화면 공유
  view: HTMLElement; //화면 표시 DOM
}
const view = document.getElementById('localVideo');
rtcClient.startRemoteView({
  userID: userID,
  streamType: 1,//1 - 대형 화면, 2 - 소형 화면, 3 - 화면 공유
  view: view
});
```

#### stopRemoteView(params: StopRemoteParams)
원격 비디오 화면 또는 화면 공유 화면 표시를 종료함과 동시에 해당 원격 사용자의 데이터 스트림을 다시 풀링하지 않습니다.
매개변수:

|매개변수 이름|	유형	| 설명|
| ----- | ----- |  ----- |
|userID|	string|	 사용자 ID|
|streamType|number|	 화면 유형. 1: 대형 화면, 2: 소형 화면, 3: 화면 공유|

예시:
```typescript
interface StopRemoteParams {
  userID: string; // 사용자 ID
  streamType: number; // 화면 유형. 1 - 대형 화면, 2 - 소형 화면, 3 - 화면 공유
}
rtcClient.stopRemoteView({
   userID: userID,
   streamType: 1 //1 - 대형 화면, 2 - 소형 화면, 3 - 화면 공유
 });
```

### 메시지 수신/발신 관련 함수
#### sendTextMessage(params: MessageParams) 
채팅방 메시지 발송
매개변수:

|매개변수 이름|	유형	| 설명|
| ----- | ----- |  ----- |
|classId|number| 강의실 ID|
|message|string| 메시지 텍스트|

예시:
```typescript
interface MessageParams {
  classId: number; // 강의실 ID
  message: string; // 메시지 텍스트
}
rtcClient.sendTextMessage(params).then(() => {
})
```

#### sendCustomMessage(userID: string, data: string)
사용자 정의 C2C 메시지 발송 
매개변수:

|매개변수 이름|	유형	|	설명|
| ----- | ----- | ----- |
|userID|string| 사용자 ID |
|data|string|	 사용자 정의 메시지|

예시:
```typescript
rtcClient.sendCustomMessage(userID, JSON.stringify(params)
```

#### sendGroupCustomMessage(classId: number, data: string)
사용자 정의 그룹 메시지 발송  
매개변수:

|매개변수 이름|	유형	| 설명|
| ----- | ----- | ----- |
|classId|number| 강의실 ID|
|data|string| 사용자 정의 메시지|

예시:
```typescript
rtcClient.sendGroupCustomMessage(classId, JSON.stringify(params))
```

### 디바이스 작업 관련 함수
[](id:openCamera)
#### openCamera(view: HTMLElement)
카메라 켜기
매개변수:

|매개변수 이름|	유형	| 설명|
| ----- | ----- | ----- |
|view|HTMLElement|	 화면 표시 DOM|

예시:
```typescript
const domEle = document.getElementById('localVideo');
rtcClient.openCamera(domEle);
```

#### closeCamera()
카메라 끄기 
매개변수: 없음
예시:
```typescript
rtcClient.closeCamera();
```

[](id:getCameraList)
#### getCameraList()
카메라 리스트 획득
매개변수: 없음
예시:
```typescript
rtcClient.getCameraList()
```

[](id:setCurrentCamera)
#### setCurrentCamera(deviceId:string)
카메라 설정. 매개변수는 getCameraDevicesList에서 획득한 디바이스 ID
매개변수:

|매개변수 이름|	유형	| 설명|
| ----- | ----- |  ---- |
|deviceId|string| 디바이스 ID|

예시:
```typescript
rtcClient.setCurrentCamera(deviceId)
```

[](id:openMicrophone)
#### openMicrophone()
마이크 켜기
매개변수: 없음
예시:
```typescript
rtcClient.openMicrophone();
```

[](id:closeMicrophone)
#### closeMicrophone()
마이크 끄기
매개변수: 없음
예시:
```typescript
rtcClient.closeMicrophone();
```


[](id:getMicrophoneList)
#### getMicrophoneList()
마이크 디바이스 리스트 획득  
매개변수: 없음
예시:
```typescript
rtcClient.getMicrophoneList()
```
#### setCurrentMicDevice(micId:string)
마이크 설정. 매개변수는 getMicDevicesList에서 획득한 디바이스 ID
매개변수:

|매개변수 이름|	유형	| 	설명|
| ----- | ----- | ----- |
|micId|string|	 디바이스 ID|

예시:
```typescript
rtcClient.setCurrentMicDevice(micId)
```

[](id:setBeautyStyle)
#### setBeautyStyle(params: BeautyParams) 
뷰티 필터, 미백, 안색 보정 효과 단계 설정 
매개변수:

|매개변수 이름|	유형	| 설명|
| ----- | ----- |  ----- |
|beautyStyle|number| 1: 매끄럽게. 뷰티 쇼에 적합하며 효과가 비교적 뚜렷합니다.<br>2: 자연스럽게. 잡티 제거 알고리즘에서 얼굴의 디테일을 더 많이 유지하기 때문에 더 자연스러운 느낌입니다.|
|beauty|number|	 뷰티 필터 단계. 0 - 9로 설정 가능합니다. 0으로 설정 시 비활성화되고, 1 - 9의 숫자가 클수록 효과가 더욱 선명해집니다.|
|white|number|	 미백 단계. 0 - 9로 설정 가능합니다. 0으로 설정 시 비활성화되고, 1 - 9의 숫자가 클수록 효과가 더욱 선명해집니다.|
|ruddiness|number|	 안색 보정 단계. 0 - 9로 설정 가능합니다. 0으로 설정 시 비활성화되고, 1 - 9의 숫자가 클수록 효과가 더욱 선명해집니다. 해당 매개변수는 현재 Windows 플랫폼에서는 지원되지 않습니다.|

예시:
```typescript
interface BeautyParams {
  beautyStyle: number;//매끄럽게, 자연스럽게
  beauty: number; //뷰티 필터 단계
  white: number; //미백 단계
  ruddiness: number; //안색 보정 단계
}
rtcClient.setBeautyStyle({
	beautyStyle: 1,
	beauty: 5,
	white: 5,
	ruddiness: 5
})
```

## 모듈 이벤트
### 예시
```typescript
const EVENT = rtcClient.EVENT
rtcClient.on(EVENT.STUDENT_RAISE_HAND, () => {
   //학생 손 들기
})
```
### 이벤트 상세

| CODE |설명|
| ----- | ----- |
|ENTER_ROOM_SUCCESS|방 입장 성공|
|LEAVE_ROOM_SUCCESS|방 퇴장 성공|
|TEACHER_ENTER|교사 입장 성공|
|TEACHER_LEAVE|교사 퇴장 성공|
|STUDENT_ENTER|학생 입장 성공|
|STUDENT_LEAVE|학생 퇴장 성공|
|SCREEN_SHARE_ADD|교사 화면 공유 활성화|
|SCREEN_SHARE_REMOVE|교사 화면 공유 종료|
|REMOTE_VIDEO_ADD|원격 비디오 스트림에서 이벤트 추가, 원격 사용자가 비디오 스트림을 배포한 후 해당 알림 수신|
|REMOTE_VIDEO_REMOVE|원격 비디오 스트림에서 이벤트 삭제, 원격 사용자가 비디오 스트림 배포 취소 후 해당 알림 수신|
|REMOTE_AUDIO_ADD|원격 오디오 스트림에서 이벤트 추가|
|REMOTE_AUDIO_REMOVE|원격 오디오 스트림에서 이벤트 삭제|
|ROOM_DESTROYED|폐기된 방|
|QUESTION_TIME_STARTED|질답 시간 시작|
|QUESTION_TIME_STOPPED|질답 시간 종료|
|STUDENT_RAISE_HAND|학생 손 들기|
|BE_INVITED_TO_PLATFORM|질문 답변 요청 받음, 지명|
|ANSWERING_FINISHED|답변 종료, 오디오 꺼짐|
|MESSAGE_RECEIVED|메시지 수신|
|KICKED_OUT|같은 계정으로 다른 곳에서 로그인하여 연결 끊김|
|ERROR|오류|
|WARNING|경고|
