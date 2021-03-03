## Demo 체험
<table style="text-align:center;vertical-align:middle;width: 300px">
  <tr>
    <th width="150px">Mac OS</th>
    <th width="150px">Windows</th>
  </tr>
  <tr>
<td>
		<a href="https://trtc-1252463788.cos.ap-guangzhou.myqcloud.com/electron_sdk/solution/education/TRTC_Education_Demo-1.1.0.dmg" >
		<span style="width:125px;height: 125px;background-image:url(https://main.qcloudimg.com/raw/d03160ca4e5342a96464aaba1de97923.png);background-size: cover;display:block;">
</span></a></td>
<td>
<a href="https://trtc-1252463788.cos.ap-guangzhou.myqcloud.com/electron_sdk/solution/education/TRTC_Education_Demo%20Setup%201.1.0.exe">
<span style="width:125px;height: 125px;background-image:url(https://main.qcloudimg.com/raw/d03160ca4e5342a96464aaba1de97923.png);background-size: cover;display:block;">
</span></a></td>
  </tr>
</table>



## 효과
Tencent Cloud에서 제공하는 Demo를 다운로드 및 설치하여 실시간 인터랙션 수업 기능 효과를 체험해볼 수 있으며, 이에는 음성, 비디오, 화면 공유 등의 수업 방식이 포함되어 있으며, 이외에도 교사 질답 시작, 학생 손 들기, 교사 답변 요청, 답변 완료 등 관련 기능이 캡슐화되어 있습니다.

신속한 실시간 인터랙션 수업 기능이 필요할 경우, Tencent Cloud의 Demo를 기반으로 직접 수정 및 모델링을 진행하거나 또는 [trtc-electron-education](https://intl.cloud.tencent.com/document/product/647/37279) 모듈을 사용하여 사용자 정의 UI 인터페이스를 구현할 수 있습니다.

## Demo UI 인터페이스 재사용
### 1단계: 신규 애플리케이션 생성
1. TRTC 콘솔에 로그인하여 [개발 보조]>[빠른 Demo 활성화](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. [시작하기]를 클릭하고 애플리케이션 이름(예: `TestEduDemo`)을 입력한 후 [애플리케이션 생성]을 클릭합니다.

>? 설명: 해당 기능은 Tencent Cloud의 [TRTC](https://intl.cloud.tencent.com/document/product/647/35078)와 [IM](https://intl.cloud.tencent.com/document/product/1047) 두 가지 기본 PAAS 서비스를 이용합니다. TRTC가 활성화 되면 인스턴트 메시징 IM 서비스도 동시에 활성화 됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [IM 가격 설명](https://intl.cloud.tencent.com/document/product/1047/34350)을 참조하십시오.

<span id="ui.step2"></span>
### 2단계: SDK와 Demo 소스 코드 다운로드
1. [Github](https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTCScenesDemo/TRTCEducation)를 클릭하여 Github로 이동한 후, 관련 SDK 및 함께 제공되는 Demo 소스 코드를 다운로드합니다.
2. 다운로드 완료 후 TRTC 콘솔로 돌아가 [다운로드 완료, 다음 단계]를 클릭하면 SDKAppID와 키 정보를 확인할 수 있습니다.

### 3단계: Demo 프로젝트 파일 설정
1. [2단계](#ui.step2)에서 다운로드한 소스 패키지를 압축 해제합니다.
2. `TRTCEducation/app/debug/GenerateTestUserSig.js` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.js` 파일에서 관련 매개변수를 설정합니다.
  <ul style="margin:0;"><li>SDKAPPID: 0으로 기본 설정되어 있으며 실제 SDKAppID로 설정하십시오.</li>
  <li>SECRETKEY: 공백으로 기본 설정되어 있으며 실제 키 정보로 설정하십시오.</li></ul> 
  <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. TRTC 콘솔로 돌아가 [붙여넣기 완료, 다음 단계]를 클릭합니다.
5. [가이드 닫기, 콘솔 관리 애플리케이션 열기]를 클릭합니다.

>!본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 방법입니다. 여기에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 귀하의 서버에 통합하고 App 지향의 인터페이스를 제공합니다. UserSig가 필요한 경우 귀하의 App이 비즈니스 서버에 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

### 4단계: Demo 실행

```typescript
// yarn 설치. demo는 yarn 기반으로 관리
npm install yarn -g
// 필요한 종속 패키지 설치
yarn install
// 개발 디버깅
yarn dev
// 패키징
yarn package
```

>!
>- Mac에서만 Mac 패키지를 패키징할 수 있으며, Windows 컴퓨터에서만 Windows 패키지를 패키징할 수 있습니다.


### 5단계: Demo 소스 코드 수정
Demo에서 사용하는 프레임워크 기술은 다음과 같습니다.
- typescript
- react & react hooks
- electron & electron-react-boilerplate
- element-ui

다음 테이블에는 2차 수정을 위한 각 파일 및 해당 UI 인터페이스가 나열되어 있습니다.

| 파일 이름 |기능 설명|
| ----- | ----- |
| app/containers/HomePage.tsx|강의실 입장 UI 구현 코드|
| app/containers/ClassRoomPage.tsx|강의실 UI 구현 코드|
| app/components/TeacherClass.tsx|강의실-교사용 UI 구현 코드|
| app/components/StudentClass.tsx|강의실-학생용 UI 구현 코드|
| app/components/Chat.tsx|강의실-채팅방 UI 구현 코드|
| app/components/UserList.tsx|강의실-참여자 리스트 UI 구현 코드|

## 사용자 정의 UI 인터페이스 구현
Demo에서 기본적으로 구현되는 UI가 귀하의 예상과 다른 경우, 필요에 따라 사용자 인터페이스를 구현할 수 있습니다. 즉, Tencent Cloud에서 캡슐화한 [trtc-electron-education](https://www.npmjs.com/package/trtc-electron-education) 모듈에서 제공하는 멀티미디어 기능을 사용해 직접 UI 부분을 구현할 수 있습니다.
![](https://main.qcloudimg.com/raw/cba4f331a811dd5dbf31cce80bd1d826.png)

### 1단계: SDK 통합

```
// yarn 방식 가져오기
yarn add trtc-electron-education
// npm 방식 가져오기
npm i trtc-electron-education --save
```

### 2단계: 모듈 초기화
모듈을 초기화합니다. 여기에서 필수 작성 매개변수는 다음과 같습니다.

| 매개변수 |유형|설명|
| ----- | ----- | ----- |
|sdkAppId|number|필수 작성 매개변수입니다. <a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.|
|userID|string|필수 작성 매개변수입니다. 사용자 ID로, 귀하의 계정 시스템에서 지정할 수 있습니다.|
|userSig|string|필수 작성 매개변수입니다. 자격 서명(로그인 비밀번호에 해당)으로, userID에서 계산하여 획득합니다. 자세한 계산 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.|

```typescript
import TrtcElectronEducation from 'trtc-electron-education';
const rtcClient = new TrtcElectronEducation({
   sdkAppId: 1400***803,
   userID: '123'
   userSig: 'eJwtzM9****-reWMQw_'
 });
```

### 3단계: 교사 측 수업 시작 구현
1. 교사 측에서 모듈 [createRoom](https://intl.cloud.tencent.com/document/product/647/37279#createRoom)을 호출하여 강의실을 생성합니다.
```typescript
const params = {
      classId, // 강의실 ID
      nickName // 닉네임
}
rtcClient.createRoom(params).then(() => {
	//강의실 생성 성공
})
```
2. 교사 측에서 모듈의 [enterRoom](https://intl.cloud.tencent.com/document/product/647/37279#enterRoom)을 호출하여 수업을 시작합니다.
```typescript
rtcClient.enterRoom({
      role: 'teacher', // 역할
      classId // 강의실 ID
})
```
3. 교사 측에서 모듈의 [openCamera](https://intl.cloud.tencent.com/document/product/647/37279#openCamera)를 호출하여 자신의 카메라를 켭니다.
```typescript
const domEle = document.getElementById('test');
rtcClient.openCamera(domEle)
```
4. 교사 측에서 PPT 및 코스웨어 재생 등 자신의 화면을 학생에게 공유할 수 있습니다.
 a. 먼저 모듈의 [getScreenShareList](https://intl.cloud.tencent.com/document/product/647/37279#getScreenShareList)를 호출하여 창 리스트를 가져옵니다.
```typescript
const screenList = rtcClient.getScreenShareList()
```
b. 모듈의[startScreenCapture](https://intl.cloud.tencent.com/document/product/647/37279#startScreenCapture)를 호출하여 화면 공유 푸시 스트림을 시작합니다.
```typescript
rtcClient.startScreenCapture({
      type,// 수집 소스 유형
      sourceId,//수집 소스 ID. 해당 필드는 창에서 창 핸들 의미, 화면에서는 화면 ID 의미
      sourceName // 수집 소스 이름, UTF8 인코딩
 })
```
5. 수업 중, 교사가 질문을 통해 학생과 인터랙션하고 싶은 경우 모듈의 [startQuestionTime](https://intl.cloud.tencent.com/document/product/647/37279#startQuestionTime)을 호출하여 질답 시간을 시작할 수 있습니다. 학생 측에서 해당 이벤트를 수신한 후 손 들기를 신청하여 문제에 답할 수 있습니다.
```typescript
rtcClient.startQuestionTime(classId) // classId: 강의실 ID
```
6. 학생이 손을 든 후, 교사 측에서 모듈의 [inviteToPlatform](https://intl.cloud.tencent.com/document/product/647/37279#inviteToPlatform)을 호출하여 학생에게 답변을 요청하면 요청 받은 학생의 마이크가 자동으로 켜집니다.
```typescript
rtcClient.inviteToPlatform(userID) // 요청 받은 학생의 userID
```
7. 교사 측에서 모듈의 [finishAnswering](https://intl.cloud.tencent.com/document/product/647/37279#finishAnswering)을 호출하여 학생의 마이크를 끌 수 있습니다.
```typescript
rtcClient.finishAnswering(userID)// 마이크를 비활성화할 학생의 userID
```

### 4단계: 학생 측의 수업 듣기 구현
1. 학생 측에서 모듈의 [enterRoom](https://intl.cloud.tencent.com/document/product/647/37279#enterRoom)을 호출하여 강의실에 입장해 수업을 준비합니다.
```typescript
rtcClient.enterRoom({
      role: 'student', // 역할
      classId // 강의실 ID
})
```
2. 교사 측에서 손 들기 질답을 시작하면, 학생 측에서 모듈의 [raiseHand](https://intl.cloud.tencent.com/document/product/647/37279#raiseHand)를 호출하여 발언을 신청합니다.
```typescript
rtcClient.raiseHand()
```

### 5단계: 채팅방 기능 구현

교사 측과 학생 측은 채팅방을 이용해 텍스트 메시지를 상호 전송할 수 있습니다.
```typescript
const params = {
   classId: classId, // 강의실 ID
   message: '안녕하세요.' // 메시지 텍스트
}
rtcClient.sendTextMessage(params) // 채팅방에 메시지 발송
```
