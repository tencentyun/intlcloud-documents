This document describes how to quickly run GME Unreal Engine sample project and integrate the sample code to a project.

## Running the Unreal Engine Sample Project

### Environment requirements

- Unreal Engine 4.22 or later
- Microsoft Visual Studio
- A configuration environment that can run Unreal Engine projects

### Prerequisites

You need to activate the voice chat and voice messaging services of GME and get the `AppId` and `Key` in advance. For more information on how to apply for GME services, see [Activating Services](https://cloud.tencent.com/document/product/607/10782). `appId` is the `AppID` and `authKey` is the permission key in the console. 

### Directions

#### Step 1. Download the project

Download the Unreal Engine sample project as instructed in [SDK Download Guide](https://www.tencentcloud.com/document/product/607/18521). As the demo configurations for UE5 and UE4 are different, you need to download the sample project for the corresponding engine version.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/jeet801_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16753202244651.png)


#### Step 2. Configure the project

After downloading, open the project directory, find `UserConfig.cpp` in the `Source\UEDemo1` path, and change the `appID` and `appKey` in the red box as shown below to the `AppID` and permission key applied for in [Service Management > Application Settings](https://console.cloud.tencent.com/gamegme) in the GME console.

![](https://qcloudimg.tencent-cloud.cn/raw/e82b3bf515b0cc8ff2055dff7ac0b1e8.png)

#### Step 3. Compile and run the demo

**1. Run the program**

Click <img src="https://qcloudimg.tencent-cloud.cn/raw/302e95d032818ed9e463a0b3b3417ce4.png" width="30">![]() in the Editor to run the program.

![](https://qcloudimg.tencent-cloud.cn/raw/fe22948ae13046f4f8db953a6ee34e57.png)

**2. Initialize**

- UserID: It is equivalent to `openID`, which is the unique identifier of a user in the application. The `openID` value must be unique on each terminal.
- Voice Chat: voice chat feature UI.
- Voice Messaging: voice messaging feature UI.

Click **Login** to initialize, and then click **Voice Chat** to enter the voice chat room configuration page.

![](https://qcloudimg.tencent-cloud.cn/raw/b872b21122c244b443f7ff651048ca5b.jpg)

**3. Enter a voice chat room**

- RoomId: Room ID. Users in the same room can communicate with each other by voice.
- RoomType: Use Fluency to enter the room.
- JoinRoom: Enter the voice room.
- Back: Go back to the previous page.

After configuring the voice chat room ID, click **JoinRoom** to enter the room.

![](https://qcloudimg.tencent-cloud.cn/raw/4df80f35962207dcc5435eb78dd95138.jpg)

**4. Use voice chat**
The page will display the `RoomID` for room entry and the local `openID`.

- Mic: Select to turn on the mic.
- Speaker: Select to turn on the speaker.
- 3D Voice Effect: Select to enable 3D sound effects.
- Voice Chang: Select to enable voice changing effects.

After the mic and speaker are selected locally, repeat the above steps on another device to enter the same room and turn on the mic and speaker, so that communication can be implemented.
If `3D Voice Effect` is selected on both terminals, use the A, S, D, and W keys to move around and experience the directional 3D stereo effect.

![](https://qcloudimg.tencent-cloud.cn/raw/3c34c7be421a1569cb47807990ae4d07.jpg)

**5. Use voice messaging**

- Language: Select the target language for text conversion. For example, if you speak Chinese, choose Mandarin.
- Audio: Click to listen after recording.
- Audio-to-Text: Text content of the voice message.
- Push To Talk: Press and hold to record.
- Back: Go back to the previous page.

Press and hold **Push to Talk** and speak into the mic. After you release the button, your voice message will be converted into text and displayed in the UI.

![](https://qcloudimg.tencent-cloud.cn/raw/a6634573204ad4df2820357a247e8677.jpg)

## Sample Project Code Overview

The main process to use GME voice chat is `Init > EnterRoom > EnableMic > EnableSpeaker`. The main code of the sample project is in `BaseViewController.cpp` and `ExperientialDemoViewController.cpp`.


### Initialization

The initialization code is in the `InitGME` function in the `BaseViewController.cpp` file. It includes initialization, authentication initialization for voice message, and `TMGDelegate` callback settings.

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

Using GME requires periodic calls to the `Poll` function in `Tick` in the `UEDemoLevelScriptActor.cpp` script.

```
void AUEDemoLevelScriptActor::Tick(float DeltaSeconds) {
	Super::Tick(DeltaSeconds);	

	m_pTestDemoViewController->UpdateTips();
	m_pCurrentViewController->UpdatePosition();
	ITMGContextGetInstance()->Poll();
}
```

### Room entry
The room entry code is in the `EnterRoom` function in the `BaseViewController.cpp` file.

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

The room entry callback is in the `OnEvent` function in the same script.

```
if (eventType == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM) {
		int32 result = JsonObject->GetIntegerField(TEXT("result"));
		FString error_info = JsonObject->GetStringField(TEXT("error_info"));
		if (result == 0) {
			GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, TEXT("Enter room success."));
		}
		else {
			FString msg = FString::Printf(TEXT("Enter room failed. result=%d, info = %ls"), result, *error_info);
			GEngine->AddOnScreenDebugMessage(INDEX_NONE, 20.0f, FColor::Yellow, *msg);
		}
		onEnterRoomCompleted(result, error_info);
```

### Device enablement
Device enablement code after successful room entry is in `ExperientialDemoViewController.cpp`.

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

### 3D sound effect

For the connection of 3D sound effect, see [3D Sound Effect](https://www.tencentcloud.com/document/product/607/18218). In the project, initialize the 3D sound effect feature first with the code in `ExperientialDemoViewController.cpp`.

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

Call the `UpdatePosition` function in `Tick` in the `UEDemoLevelScriptActor.cpp` script .

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

Enable 3D effects in `ExperientialDemoViewController.cpp`.

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
