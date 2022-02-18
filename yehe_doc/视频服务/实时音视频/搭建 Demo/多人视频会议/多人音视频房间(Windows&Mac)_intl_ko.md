본 문서는 효율적인 레이아웃과 강력한 적용성을 갖춘 멀티미디어 커뮤니케이션 및 협업 툴인 PC TUIRoom 모듈을 소개합니다. 협업 업무, 원격 채용, 원격 진료, 보험 청구, 온라인 고객 서비스, 화상 면접, 디지털 정부 업무, 금융 디지털화, 온라인 회의 및 온라인 교육과 같은 시나리오에서 사용할 수 있습니다. 다양한 산업 시나리오와의 긴밀한 통합을 통해, 기업은 비용을 절감하고 효율성을 높이며, 디지털 혁신을 가속화하고, 경쟁력을 향상할 수 있습니다.
당사 App을 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 설치하여 체험할 수 있습니다.

## 솔루션 장점
- 초저지연 음성 및 영상 통화, 채팅방, 화면 공유, 뷰티필터, 장치 점검, 데이터 통계 등과 같은 기능을 통합하여 다중 사용자 멀티미디어 방의 공통 기능을 다룹니다.
- 수요의 2차 개발에 따라 사용자 정의 UI 인터페이스 및 레이아웃을 빠르게 실현할 수 있으며 비즈니스가 빠르게 런칭 되도록 도울 수 있습니다.
- TRTC 및 IM 기본 SDK를 캡슐화하여 기본 로직 제어를 구현하며, 편리한 호출을 위한 인터페이스를 제공합니다.

## 연결 가이드
그룹 멀티미디어 룸 기능에 빠르게 액세스하려면 당사에서 제공하는 App을 기반으로 직접 수정 및 조정하거나 App의 Module을 사용하여 사용자 정의 UI 인터페이스를 구현할 수 있습니다.

[](id:step1_1)
### 1단계: App 소스 코드 다운로드
[RoomApp](https://github.com/tencentyun/TUIMeeting)을 클릭하여 Clone하거나 소스 코드를 다운로드합니다.

[](id:step1_2)
### 2단계: App 파일 설정
<dx-tabs>
::: Windows 설정
1. `Windows\RoomApp\utils\usersig\win\GenerateTestUserSig.h` 파일을 찾아 엽니다.
2. `GenerateTestUserSig.h`의 매개변수를 설정합니다.
	- **SDKAPPID**: 0으로 기본 설정되어 있습니다. 실제 SDKAPPID로 설정하십시오.
	- **SECRETKEY**: 기본적으로 비어 있으며 실제 SECRETKEY로 설정하십시오.
![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
:::
::: Mac 설정
1. `Windows\RoomApp\utils\usersig\mac\UserSigConfig.h` 파일을 찾아 엽니다.
2. `UserSigConfig.h` 의 매개변수를 설정합니다.
	- **SDKAPPID_**: 0으로 기본 설정되어 있습니다. 실제 SDKAPPID로 설정하십시오.
	- **SecretKey_**: 기본적으로 비어 있으며 실제 SECRETKEY로 설정하십시오.
:::
</dx-tabs>

>!
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 App 실행 및 기능 디버깅용으로 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:step1_3)
### 3단계: App 설정 및 실행
<dx-tabs>
::: Windows 설정
1. 컴파일 환경은 Virtual Studio(최소 2015 버전)를 사용합니다.
2. App의 UI는 현재 주요 QT 프레임워크 버전 5.9를 사용합니다. QT를 다운로드하여 설치하고 VS에서 QT 툴을 설정하세요. 또는 버전에 따라 App 프로젝트에서 QT 설정을 수정하여 설정을 완료합니다.
3. RoomApp에서 RoomApp.vcxproj 소스 코드 프로젝트를 열고 프로그램을 컴파일하고 실행합니다.

:::
::: Mac 설정
1. 컴파일 환경은 QtCreator를 사용합니다. QT를 설치할 때 QtCreator를 동시에 설치하도록 선택할 수 있습니다. 버전은 공식 QT 설치 패키지를 따릅니다.
2. App의 UI는 현재 주요 QT 프레임워크 버전 5.9를 사용합니다. QT 5.9를 다운로드하여 설치하고 QT의 설치 디렉터리를 가리키도록 시스템 환경 변수 QTDIR을 설정하십시오.
3. RoomApp에서 RoomApp.pro 소스 코드 프로젝트를 열고 프로그램을 컴파일하고 실행합니다.
:::
</dx-tabs>

[](id:step1_4)
### 4단계: App 소스 코드 수정
-  Module 계층은 TRTC 및 IM을 캡슐화하고 기본 논리 제어를 구현하며 UI 계층 호출을 용이하게 하는 기능적 인터페이스를 제공합니다.
- App 모듈은 인터페이스의 기능 구현을 포함하는 UI 모듈로, 필요에 따라 2차 개발을 수행하거나 전체 UI를 교체할 수 있습니다.

## 애플리케이션 체험
>! 애플리케이션 체험 시 최소 2대의 디바이스가 필요합니다.
### 로그인 인터페이스
다음과 같이 사용자 이름을 입력하고 로그인합니다. 사용자 이름은 유일해야 하며 다른 사용자 이름과 중복되어서는 안 됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/22cbaa8ac1d47cfc39076fa6149649c2.png)

### 장치 점검 페이지
여기에서 필요에 따라 장치 점검을 수행하거나 방에서 사용할 장치를 설정하고 뷰티필터 효과 등을 설정할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e5aed81f7ad0c07193c5506ebe0466d1.png)

### 메인 인터페이스
방에 가장 먼저 입장하는 사람은 호스트이며 메인 인터페이스에는 마이크 목록, 하단 툴 모음, 상단 툴 모음 등이 포함됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/33d901c254c6c37c8afa4bce759b0bb3.png)

### 마이크 목록
마이크 목록은 현재 방에 있는 참석자를 표시할 수 있으며, 상대방이 카메라와 마이크를 켜면 상대방의 사진을 보고 상대방의 음성을 들을 수 있습니다.

### 하단 툴 모음
자신의 마이크/카메라 제어, 화면 공유 열기, 참석자 목록, 채팅방 등의 기능을 구현했습니다.

### 상단 컨트롤 바
마이크에서 네트워크 정보, 설정 페이지, 목록 레이아웃의 기능을 구현합니다.

### 설정 창
설정 창에서 장치를 선택하고 뷰티필터 매개변수 등 기타 매개변수를 설정할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9eb20c81799dddc5be3f3fa7ef88dbac.png)

### 채팅방
- 채팅방은 그룹 참석자와 채팅할 수 있습니다.
- 호스트는 모든 참석자를 음소거/음소거 해제할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9d927c98a595667d9f3f16d597abc77e.png)

### 방 퇴장
호스트가 방을 나갈 때 두 가지 옵션이 있습니다.
- **방 해산**:  모든 사람이 방에서 모두 나가야 합니다.
- **방 퇴장**: 방 호스트 권한을 다른 사용자에게 호스트로 양도합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/e2485085cdb43de94ef9d8bc6851a436.png)

## 사용자 정의 UI 인터페이스 구현
소스 코드의 Module에는 TRTC SDK 및 IM SDK의 캡슐화가 포함되어 있습니다. 이 모듈에서 제공하는 인터페이스 기능 및 기타 정의는 `TUIRoomCore.h`, `TUIRoomCoreCallback.h`, `TUIRoomDef.h` 및 기타 파일에서 볼 수 있습니다. 그리고 해당 인터페이스를 사용하여 사용자 정의 UI 인터페이스를 구현합니다.

[](id:step2_1)
### 1단계: SDK 통합
공식 웹사이트에서 [TRTC SDK](https://intl.cloud.tencent.com/document/product/647/34615) 및 [IM SDK](https://intl.cloud.tencent.com/document/product/1047/33996)를 다운로드하고 외부 SDK 디렉터리의 IM SDK 및 LiteAVSDK 디렉터리에 있는 파일을 교체합니다.
>! IM SDK는 C++ 버전을 사용합니다.

|SDK|다운로드 페이지|통합 가이드|
|--|--|--|
|TRTC SDK|[DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615)|[통합 가이드 문서](https://intl.cloud.tencent.com/document/product/647/35095)|
|IM SDK|[DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996)|[통합 가이드 문서](https://intl.cloud.tencent.com/document/product/1047/34310)|

[](id:step2_2)
### 2단계: 프로젝트 구성 SDK 디렉터리 및 라이브러리 파일
- **Windows**: VS에서 헤더 파일 디렉터리, 정적 라이브러리 디렉터리 및 종속 정적 라이브러리 파일을 설정합니다.
- **Mac**: pro 및 pri 파일에 종속 라이브러리 및 파일 디렉터리를 추가합니다.

[](id:step2_3)
### 3단계: 생성 및 로그인
1. `IUIRoomCore::Instance` 인터페이스를 사용하여 IUIRoomCore 싱글톤을 만들고 사용합니다.
2. AddCallback 인터페이스를 호출하여 콜백 클래스를 설정하고 SDK의 콜백 알림을 수락합니다.
3. Login 인터페이스를 호출하여 로그인합니다.
<table>
<thead><tr><th>매개변수 이름</th><th>설명</th></tr></thead>
<tbody><tr>
<td>sdk_appid</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.</td>
</tr>
<tr>
<td>user_id</td>
<td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시 부호(-), 언더바(_)만 허용됩니다. 사업체의 실제 계정 시스템에 맞게 설정할 것을 권장합니다.</td>
</tr>
<tr>
<td>user_sig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명입니다. 가져오는 방법은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법 및 사용</a>을 참고하십시오.</td>
</tr>
</tbody></table>

[](id:step2_4)
### 4단계: 대화명 설정
로그인 성공 후 SetSelfProfile을 호출하여 사용자 정보를 설정합니다.

[](id:step2_5)
### 5단계: 방 생성
1. 참석자는 CreateRoom 인터페이스를 호출하여 새로운 방을 생성하고, 성공적으로 방이 생성되면 채팅방과 TRTC방을 포함한 방에 호스트로 입장합니다.
2. 참석자는 StartCameraPreview API를 호출하여 로컬 비디오 캡처 및 표시를 시작합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/485afdb0dc5218a03410de86b215004d.png)

[](id:step2_6)
### 6단계: 방 삭제
1. 호스트가 DestoryRoom 인터페이스를 호출하여 방을 삭제하고 IM 그룹 채팅을 닫고 TRTC 방을 종료합니다.
2. 참석자 단말은 OnExitRoom 콜백 메시지를 수신하여 그룹을 해산하고 TRTC 방을 나가도록 알립니다.

[](id:step2_7)
### 7단계: 방 양도
1. 호스트는 TransferRoomMaster 인터페이스를 호출하여 방을 나가는 작업을 위해 다른 사람에게 방을 양도합니다.
2. 참석자는 OnRoomMasterChanged 콜백 메시지를 수신하여 방 호스트에게 변경 사항을 알립니다.
3. 변경된 호스트는 호스트 권한을 획득했으며 그룹 참석자를 제어할 수 있습니다.

[](id:step2_8)
### 8단계: 방 입장
1. 방에 입장하는 과정은 기본적으로 방 생성 과정과 동일하며, 참석자가 방에 입장할 때는 먼저 방을 생성해야 하며, 생성에 실패하면 참석자로 방에 입장합니다.
2. 방 생성에 실패할 경우 방 정보를 먼저 획득한 후 방에 입장합니다.
3. 다른 참석자는 OnRemoteUserEnter 콜백을 수신하여 참석자가 방에 입장했음을 알립니다.

![](https://qcloudimg.tencent-cloud.cn/raw/89d63df3ad5243e3b45386777fbb07e5.png)

[](id:step2_9)
### 9단계: 방 퇴장
1. 참석자가 IM 방과 TRTC 방에서 나가기 위해 LeaveRoom 인터페이스를 호출합니다.
2. 다른 그룹은 OnRemoteUserLeave 콜백을 수신하고 일반 참석자는 방을 나갑니다.

[](id:step2_10)
### 10단계: 화면 공유
1. 화면 공유를 위해 StartScreenCapture API를 호출합니다.
2. 다른 참석자는 OnRemoteUserScreenVideoAvailable 콜백을 수신하여 참석자가 화면을 공유하고 있음을 알립니다.

>? 화면 공유 모듈은 창 선택 로직을 수행해야 하며, 구체적인 구현은 App 내 'ScreenShareWindow.h' 구현을 참고하십시오.

[](id:step2_11)
### 11단계: 텍스트 채팅 및 발언 금지 메시지 구현
1. SendChatMessage 인터페이스를 호출하여 문자를 보내면 방의 참석자가 OnRecevieChatMessage 콜백 메시지를 수신하고 채팅 메시지를 가져와 표시할 수 있습니다.
2. 호스트는 MuteChatRoom 인터페이스를 호출하여 채팅을 음소거 또는 음소거 해제할 수 있으며, 참석자는 OnChatRoomMuted 콜백을 수신하고 UI 계층은 이에 따라 처리합니다.
