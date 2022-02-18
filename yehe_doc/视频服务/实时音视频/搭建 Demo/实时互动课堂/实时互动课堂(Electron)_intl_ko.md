## Demo 체험
<input type="button" value="Windows 버전" style="height: 30px;width: 150px;min-width: 24px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;white-space: nowrap;margin-right:10px;"  onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education/TRTC_Education_Demo%20Setup%201.1.0.exe')" />

<input type="button" value="MacOS 버전" style="height: 30px;width: 150px;margin-top: 5px;min-width: 24px;background-color: #00a4ff;color: #fff;border: 1px solid #00a4ff;line-height: 30px;text-align: center;display: inline-block;cursor: pointer;outline: 0 none;box-sizing: border-box;text-decoration: none;font-size: 12px;white-space: nowrap;" onclick="window.open('https://web.sdk.qcloud.com/trtc/electron/download/solution/education/TRTC_Education_Demo-1.1.0.dmg')" />

## Demo UI 인터페이스 재사용
[](id:ui.step1)
### 1단계: 신규 애플리케이션 생성
1. TRTC 멀티미디어 콘솔에 로그인한 후, **개발 지원**>**[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)**을 선택합니다.
2. 애플리케이션 이름(예: `TestEduDemo`)을 입력한 후 **생성**을 클릭합니다.

>?본 기능은 기본 PAAS 서비스인 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078)과 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)을 동시에 사용하였으며, TRTC를 활성화하면 IM 서비스도 동시에 활성화됩니다. IM은 부가 서비스이며, 자세한 과금 규정은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.


[](id:ui.step2)
### 2단계: SDK와 Demo 소스 코드 다운로드
1. 실제 비즈니스 요구사항에 따라 SDK 및 관련 Demo 소스 코드를 다운로드합니다.
2. 다운로드 완료 후 **다운로드 완료, 다음 단계**를 클릭합니다.
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:ui.step3)
### 3단계: Demo 프로그래밍 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `Electron/js/GenerateTestUserSig.js` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.js` 파일에서 관련 매개변수를 설정합니다.
<ul>
 <li/>SDKAPPID: 0으로 기본 설정되어 있습니다. 실제 SDKAppID로 설정하십시오.
 <li/>SECRETKEY: 공백으로 기본 설정되어 있습니다. 실제 키 정보로 설정하십시오.</ul>
 <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png"/>
4. 붙여넣기 완료 후 **붙여넣기 완료, 다음 단계**를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 **콘솔 개요로 돌아가기**를 클릭합니다.

>!
>- 본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 것입니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로만 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

### 4단계: Demo 실행

```typescript
// yarn 설치, demo는 yarn 기반으로 관리
npm install yarn -g
// 필요한 종속 패키지 설치
yarn install
// 개발 디버깅
yarn dev
// 패키징
yarn package
```

>! 
>- 종속성 설치 중 Electron 다운로드 속도 저하 또는 랙 발생 등의 문제가 발생하면 [문의하기](https://intl.cloud.tencent.com/contact-us)를 참고하여 해결할 수 있습니다.
>- Mac에서만 Mac 패키지를 패키징할 수 있으며, Windows 컴퓨터에서만 Windows 패키지를 패키징할 수 있습니다.


### 5단계: Demo 소스 코드 수정
Demo에서 사용하는 프레임워크 기술은 다음과 같습니다.
- typescript
- react & react hooks
- electron & electron-react-boilerplate
- element-ui

다음 테이블에는 2차 수정을 위한 각 파일 및 해당 UI 인터페이스가 나열되어 있습니다.

| 파일 |기능 설명|
| ----- | ----- |
| app/containers/HomePage.tsx|강의실 입장 UI 구현 코드|
| app/containers/ClassRoomPage.tsx|강의실 UI 구현 코드|
| app/components/TeacherClass.tsx|강의실-교사용 UI 구현 코드|
| app/components/StudentClass.tsx|강의실-학생용 UI 구현 코드|
| app/components/Chat.tsx|강의실-채팅방 UI 구현 코드|
| app/components/UserList.tsx|강의실-참여자 리스트 UI 구현 코드|

## 사용자 정의 UI 인터페이스 구현
Demo에서 기본적으로 구현되는 UI가 사용자의 예상과 다른 경우, 필요에 따라 맞춤형 UI를 구현할 수 있습니다. 즉, Tencent Cloud에서 캡슐화한 [trtc-electron-education](https://www.npmjs.com/package/trtc-electron-education) 컴포넌트에서 제공하는 멀티미디어 기능을 사용해 직접 UI 부분을 구현할 수 있습니다.
![](https://main.qcloudimg.com/raw/cba4f331a811dd5dbf31cce80bd1d826.png)

### 1단계: SDK 통합

```
// yarn 가져오기
yarn add trtc-electron-education
// npm 가져오기
npm i trtc-electron-education --save
```

### 2단계: 컴포넌트 초기화
컴포넌트를 초기화합니다. 필수 입력 매개변수는 다음과 같습니다.

| 매개변수 |유형|설명|
| ----- | ----- | ----- |
|sdkAppId|number|필수 입력 매개변수입니다. <a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 조회할 수 있습니다.|
|userID|string|필수 입력 매개변수입니다. 사용자 ID로, 귀하의 계정 시스템에서 지정할 수 있습니다. 실제 비즈니스 계정 시스템에 따라 직접 설정하는 것을 권장합니다. |
|userSig|string|필수 입력 매개변수입니다. 자격 서명(로그인 비밀번호에 해당)으로, userID에서 계산하여 획득합니다. 자세한 계산 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.|

```typescript
import TrtcElectronEducation from 'trtc-electron-education';
const rtcClient = new TrtcElectronEducation({
   sdkAppId: 1400***803,
   userID: '123'
   userSig: 'eJwtzM9****-reWMQw_'
 });
```

### 3단계: 교사측 수업 시작 구현
1. 교사측에서 컴포넌트의 [createRoom](https://intl.cloud.tencent.com/document/product/647/37279#createRoom)을 호출하여 강의실을 생성합니다.
```typescript
const params = {
      classId, // 강의실 ID
      nickName // 닉네임
}
rtcClient.createRoom(params).then(() => {
  //강의실 생성 성공
})
```
2. 교사측에서 컴포넌트의 [enterRoom](https://intl.cloud.tencent.com/document/product/647/37279#enterRoom)을 호출하여 수업을 시작합니다.
```typescript
rtcClient.enterRoom({
      role: 'teacher', // 역할
      classId // 강의실 ID
})
```
3. 교사측에서 컴포넌트의 [openCamera](https://intl.cloud.tencent.com/document/product/647/37279#openCamera)를 호출하여 자신의 카메라를 켭니다.
```typescript
const domEle = document.getElementById('test');
rtcClient.openCamera(domEle)
```
4. 교사측에서 PPT, 강의 자료 등 자신의 화면을 학생에게 공유할 수 있습니다.
 a. 먼저 컴포넌트의 [getScreenShareList](https://intl.cloud.tencent.com/document/product/647/37279#getScreenShareList)를 호출하여 창 리스트를 가져옵니다.
```typescript
const screenList = rtcClient.getScreenShareList()
```
 b. 컴포넌트의 [startScreenCapture](https://intl.cloud.tencent.com/document/product/647/37279#startScreenCapture)를 호출하여 화면 공유 푸시 스트림을 시작합니다.
```typescript
rtcClient.startScreenCapture({
      type,// 수집 소스 유형
      sourceId,// 수집 소스 ID. 해당 필드는 창에서는 창 핸들을, 화면에서는 화면 ID를 의미함
      sourceName // 수집 소스 이름, UTF8 인코딩
 })
```
5. 수업 중, 교사가 질문을 통해 학생과 인터랙션하고 싶은 경우 컴포넌트의 [startQuestionTime](https://intl.cloud.tencent.com/document/product/647/37279#startQuestionTime)을 호출하여 질의응답 시간을 시작할 수 있습니다. 학생측에서 해당 명령어를 수신한 후 손 들기를 신청하여 문제에 답할 수 있습니다.
```typescript
rtcClient.startQuestionTime(classId) // classId: 강의실 ID
```
6. 학생이 손을 든 후, 교사측에서 컴포넌트의 [inviteToPlatform](https://intl.cloud.tencent.com/document/product/647/37279#inviteToPlatform)을 호출하여 학생에게 답변을 요청하면 요청 받은 학생의 마이크가 자동으로 켜집니다.
```typescript
rtcClient.inviteToPlatform(userID) // 답변을 요청 받은 학생의 userID
```
7. 교사측에서 컴포넌트의 [finishAnswering](https://intl.cloud.tencent.com/document/product/647/37279#finishAnswering)을 호출하여 학생의 마이크를 끌 수 있습니다.
```typescript
rtcClient.finishAnswering(userID)// 마이크를 비활성화할 학생의 userID
```

### 4단계: 학생측의 수업 듣기 구현
1. 학생측에서 컴포넌트의 [enterRoom](https://intl.cloud.tencent.com/document/product/647/37279#enterRoom)을 호출하여 강의실에 입장해 수업을 준비합니다.
```typescript
rtcClient.enterRoom({
      role: 'student', // 역할
      classId // 강의실 ID
})
```
2. 교사측에서 손 들기 문답을 시작하면, 학생측에서 컴포넌트의 [raiseHand](https://intl.cloud.tencent.com/document/product/647/37279#raiseHand)를 호출하여 발언을 신청합니다.
```typescript
rtcClient.raiseHand()
```

### 5단계: 채팅방 기능 구현

교사측과 학생측은 채팅방을 이용해 텍스트 메시지를 상호 전송할 수 있습니다.
```typescript
const params = {
   classId: classId, // 강의실 ID
   message: '안녕하세요.' // 메시지 텍스트
}
rtcClient.sendTextMessage(params) // 채팅방에 메시지 발송
```

## 기술 컨설팅
더 자세한 내용은 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하거나 colleenyu@tencent.com으로 이메일을 보내주십시오.

## 참고 문서

- [SDK API 매뉴얼](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/index.html)
- [SDK 업데이트 로그](https://intl.cloud.tencent.com/document/product/647/38702)
- [Simple Demo 소스 코드](https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTCSimpleDemo)
- [API Example 소스 코드](https://github.com/tencentyun/TRTCSDK/tree/master/Electron/TRTC-API-Example)
- [Electron FAQ](https://intl.cloud.tencent.com/document/product/647/43093)
