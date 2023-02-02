본문은 GME UnrealEngine Sample Project를 빠르게 실행하고 예시 코드를 프로젝트에 통합하는 방법을 설명합니다.

## UnrealEngine Sample Project 실행 

### 환경 요건

- Unreal Engine 4.22 이상.
- Microsoft Visual Studio. 
- UnrealEngine 프로젝트를 실행할 수 있는 구성 환경.

### 전제 조건

Tencent Cloud에 [Signing Up](https://intl.cloud.tencent.com/document/product/378/17985)하고 [Identity Verification](https://intl.cloud.tencent.com/document/product/378/3629)을 완료해야 합니다.

### 1. GME 서비스 신청[](id:step1)

GME 음성 채팅 서비스를 신청하고 [서비스 활성화](https://www.tencentcloud.com/document/product/607/10782)의 안내에 따라 음성 채팅 Appid 및 Key를 받으십시오.

### 2. 프로젝트 다운로드

[SDK 다운로드 가이드](https://www.tencentcloud.com/document/product/607/18521)의 안내에 따라 Unreal Engine Demo를 다운로드합니다. UE5와 UE4의 Demo 구성이 다르기 때문에 해당 엔진 버전에 대한 Sample Project를 다운로드해야 합니다.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/jeet801_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16753202244651.png)


### 3. 프로젝트 구성

다운로드 후 프로젝트 디렉터리를 열고 Source\UEDemo1 경로에서 UserConfig.cpp를 찾아 아래와 같이 파란색 상자의 appID 및 appKey를 [1단계](#step1)에서 얻은 GME 실시간 음성 채팅 서비스의 Appid 및 key로 변경합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/e82b3bf515b0cc8ff2055dff7ac0b1e8.png)

### 4. 컴파일 및 실행

#### 1. 프로그램 실행

편집기에서 <img src="https://qcloudimg.tencent-cloud.cn/raw/302e95d032818ed9e463a0b3b3417ce4.png" width="30">![]()을(를) 클릭하여 Demo로 이동하고 프로그램을 실행합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/fe22948ae13046f4f8db953a6ee34e57.png)

#### 2. 초기화

- UserId: 각 터미널에서 고유해야 하는 openid와 동일합니다.
- Voice Chat: 실시간 음성 채팅 기능 UI입니다.
- Voice Message: 음성 메시지 기능 UI입니다.

**Login**을 클릭하여 초기화한 후 **Voice Chat** 을 클릭하여 실시간 음성 채팅방 설정 페이지로 이동합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/b872b21122c244b443f7ff651048ca5b.jpg)

#### 3. 실시간 음성 채팅방 입장

- RoomId: 방 ID입니다. 같은 방에 있는 사용자는 음성으로 서로 통신할 수 있습니다.
- RoomType: Fluency를 사용하여 방에 입장합니다.
- JoinRoom: 음성 채팅 방에 입장합니다.
- Back: 이전 페이지로 돌아갑니다.

실시간 음성 채팅방 ID를 설정한 후, **JoinRoom**를 클릭하여 방에 입장합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/4df80f35962207dcc5435eb78dd95138.jpg)

#### 4. 실시간 음성 채팅 기능
페이지에 방 입장을 위한 Roomid와 로컬 openid가 표시됩니다.

- Mic: 마이크를 켜려면 선택합니다.
- Speaker: 스피커를 켜려면 선택합니다.
- 3D Voice Effect: 3D 사운드 효과를 활성화하려면 선택합니다.
- Voice Change: 음성 변조 효과를 활성화하려면 선택합니다.

로컬에서 Mic와 Speaker를 선택한 후, 다른 기기에서 위의 과정을 반복하여 같은 방에 들어가 Mic와 Speaker를 선택하면 서로 통신이 가능합니다.
두 터미널 모두 3D Voice Effect를 선택한 경우, 키보드 [A] [S] [D] [W] 키를 사용하여 방향을 변경하여 음성의 3D 스테레오 효과를 경험해 보십시오.

![](https://qcloudimg.tencent-cloud.cn/raw/3c34c7be421a1569cb47807990ae4d07.jpg)

#### 5. 음성 메시지 사용

- Language: 텍스트 변환 대상 언어를 선택합니다. 예를 들어 중국어를 사용하는 경우 중국어를 선택합니다.
- Audio: 녹음 후 클릭하면 들을 수 있습니다.
- Audio-to-Text: 텍스트로 변환된 음성 메시지 내용입니다.
- Push To Talk: 길게 누르면 녹음됩니다.
- Back: 이전 페이지로 돌아갑니다.

**Push to Talk**를 길게 누르고 마이크에 대고 말합니다. 버튼을 놓으면 음성 메시지가 텍스트로 변환되어 UI에 표시됩니다.

![](https://qcloudimg.tencent-cloud.cn/raw/a6634573204ad4df2820357a247e8677.jpg)

## 프로젝트 예시 코드 개요

GME 실시간 음성 채팅을 사용하는 주요 프로세스는 Init > EnterRoom > EnableMic > EnableSpeaker입니다. Demo의 주요 코드는 BaseViewController.cpp 및 ExperientialDemoViewController.cpp에 있습니다.


### 초기화

초기화 코드는 BaseViewController.cpp 파일의 InitGME 함수에 있습니다. 초기화, 음성 메시지 인증 초기화, TMGDelegate 콜백 설정이 포함됩니다.

```
int UBaseViewController::InitGME(std::string sdkAppId, std::string sdkAppKey, std::string userId) {

	int nAppid = atoi(sdkAppId.c_str());
	int ret = ITMGContextGetInstance()->Init(sdkAppId.c_str(), userId.c_str());
	ITMGContextGetInstance()->SetTMGDelegate(this);

	int RetCode = (int) ITMGContextGetInstance()->CheckMicPermission();
	FString msg = FString::Printf(TEXT("check Permission retcode =%d"), RetCode);
	GEngine->AddOnScreenDebugMessage(INDEX_NONE, 10.0f, FColor::Yellow, *msg);

	char strSig[128] = {0};
	unsigned int nLength = 128;
	nLength = QAVSDK_AuthBuffer_GenAuthBuffer(nAppid, "0", userId.c_str(), sdkAppKey.c_str(), (unsigned char *)strSig, nLength);
	ITMGContextGetInstance()->GetPTT()->ApplyPTTAuthbuffer(strSig, nLength);
   
	m_appId = sdkAppId;
	m_appKey = sdkAppKey;
	m_userId = userId;
	m_isEnableTips = false;
	m_tipsMark = 0;
	return ret;
}
```

GME를 사용하려면 UEDemoLevelScriptActor.cpp 스크립트의 Tick에 있는 Poll 함수를 주기적으로 호출해야 합니다.

```
void AUEDemoLevelScriptActor::Tick(float DeltaSeconds) {
	Super::Tick(DeltaSeconds);	

	m_pTestDemoViewController->UpdateTips();
	m_pCurrentViewController->UpdatePosition();
	ITMGContextGetInstance()->Poll();
}
```

### 방 입장
방 입장 코드는 BaseViewController.cpp 파일의 EnterRoom 함수에 있습니다.

```
void UBaseViewController::EnterRoom(std::string roomID, ITMG_ROOM_TYPE roomType) {
	int nAppid = atoi(m_appId.c_str());
	UserConfig::SetRoomID(roomID);

	char strSig[128] = {0};
	unsigned int nLength = 128;
	nLength = QAVSDK_AuthBuffer_GenAuthBuffer(nAppid, roomID.c_str(), m_userId.c_str(), m_appKey.c_str(), (unsigned char *)strSig, nLength);
	GEngine->AddOnScreenDebugMessage(INDEX_NONE, 10.0f, FColor::Yellow, TEXT("onEnterRoom"));
	ITMGContextGetInstance()->EnterRoom(roomID.c_str(), roomType, strSig, nLength);
}
```

방 입장 콜백은 동일한 스크립트의 OnEvent 함수에 있습니다.

```
if (eventType == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM) {
		int32 result = JsonObject->GetIntegerField(TEXT("result"));
		FString error_info = JsonObject->GetStringField(TEXT("error_info"));
		if (result == 0) {
			GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, TEXT("Enter room success."));
		}
		else{
			FString msg = FString::Printf(TEXT("Enter room failed. result=%d, info = %ls"), result, *error_info);
			GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, *msg);
		}
		onEnterRoomCompleted(result, error_info);
```

### 장치 활성화
방 입장 성공 후 장치 활성화 코드는 ExperientialDemoViewController.cpp에 있습니다.

```
void UExperientialDemoViewController::onCheckMic(bool isChecked) {
	//GEngine->AddOnScreenDebugMessage(INDEX_NONE, 10.0f, FColor::Yellow, L"onCheckMic");
	ITMGContext *pContext = ITMGContextGetInstance();
	if (pContext) {
		ITMGAudioCtrl *pTmgCtrl = pContext->GetAudioCtrl();
		if (pTmgCtrl) {
			pTmgCtrl->EnableMic(isChecked);
		}
	}
}

void UExperientialDemoViewController::onCheckSpeaker(bool isChecked) {
	//GEngine->AddOnScreenDebugMessage(INDEX_NONE, 10.0f, FColor::Yellow, L"onCheckSpeaker");
	ITMGContext *pContext = ITMGContextGetInstance();
	if (pContext) {
		ITMGAudioCtrl *pTmgCtrl = pContext->GetAudioCtrl();
		if (pTmgCtrl) {
			pTmgCtrl->EnableSpeaker(isChecked);
		}
	}
}
```

### 3D 음향 효과

3D 음향 효과 연결에 대해서는 [3D 음향 효과](https://www.tencentcloud.com/document/product/607/18218)를 참고하십시오. Demo에서는 먼저 ExperientialDemoViewController.cpp의 코드를 사용하여 3D 음향 효과 기능을 초기화합니다.

```
void UExperientialDemoViewController::onCheckSpatializer(bool isChecked) {
    char buffer[256]={0};
//    snprintf(buffer, sizeof(buffer), "%s3d_model", getFilePath().c_str());
    snprintf(buffer, sizeof(buffer), "%sgme_2.8_3d_model.dat", getFilePath().c_str());
	int ret1 = ITMGContextGetInstance()->GetAudioCtrl()->InitSpatializer(buffer);
	int ret2 = ITMGContextGetInstance()->GetAudioCtrl()->EnableSpatializer(isChecked, false);
	FString msg = FString::Printf(TEXT("InitSpatializer=%d, EnableSpatializer ret=%d"), ret1, ret2);
	GEngine->AddOnScreenDebugMessage(INDEX_NONE, 10.0f, FColor::Yellow, msg);
}
```

UEDemoLevelScriptActor.cpp 스크립트의 Tick에서 UpdatePosition 함수를 호출합니다.

```
void AUEDemoLevelScriptActor::Tick(float DeltaSeconds) {
	Super::Tick(DeltaSeconds);	

	m_pTestDemoViewController->UpdateTips();
	m_pCurrentViewController->UpdatePosition();
	ITMGContextGetInstance()->Poll();
}


void UBaseViewController::UpdatePosition() {
	if (!m_isCreated)
		return;

	ITMGRoom *pTmgRoom = ITMGContextGetInstance()->GetRoom();
	if (!pTmgRoom)
	{
		return;
	}

	int nRange = GetRange();
	pTmgRoom->UpdateAudioRecvRange(nRange);

	FVector cameraLocation = UGameplayStatics::GetPlayerCameraManager(m_pActor->GetWorld(), 0)->GetCameraLocation();
	FRotator cameraRotation = UGameplayStatics::GetPlayerCameraManager(m_pActor->GetWorld(), 0)->GetCameraRotation();

	FString msg = FString::Printf(TEXT("location(x=%.2f,y=%.2f,z=%.2f),  rotation(pitch=%.2f,yaw=%.2f,roll=%.2f)"),
		cameraLocation.X, cameraLocation.Y, cameraLocation.Z, cameraRotation.Pitch, cameraRotation.Yaw, cameraRotation.Roll);

	int position[] = { (int)cameraLocation.X,(int)cameraLocation.Y, (int)cameraLocation.Z };
	FMatrix matrix = ((FRotationMatrix)cameraRotation);
	float forward[] = { matrix.GetColumn(0).X,matrix.GetColumn(1).X,matrix.GetColumn(2).X };
	float right[] = { matrix.GetColumn(0).Y,matrix.GetColumn(1).Y,matrix.GetColumn(2).Y };
	float up[] = { matrix.GetColumn(0).Z,matrix.GetColumn(1).Z,matrix.GetColumn(2).Z };


	pTmgRoom->UpdateSelfPosition(position, forward, right, up);
	SetPositionInfo(msg);
}

```

ExperientialDemoViewController.cpp에서 3D 효과를 활성화합니다.

```
void UExperientialDemoViewController::onCheckSpatializer(bool isChecked) {
    char buffer[256]={0};
//    snprintf(buffer, sizeof(buffer), "%s3d_model", getFilePath().c_str());
    snprintf(buffer, sizeof(buffer), "%sgme_2.8_3d_model.dat", getFilePath().c_str());
	int ret1 = ITMGContextGetInstance()->GetAudioCtrl()->InitSpatializer(buffer);
	int ret2 = ITMGContextGetInstance()->GetAudioCtrl()->EnableSpatializer(isChecked, false);
	FString msg = FString::Printf(TEXT("InitSpatializer=%d, EnableSpatializer ret=%d"), ret1, ret2);
	GEngine->AddOnScreenDebugMessage(INDEX_NONE, 10.0f, FColor::Yellow, msg);
}

```
