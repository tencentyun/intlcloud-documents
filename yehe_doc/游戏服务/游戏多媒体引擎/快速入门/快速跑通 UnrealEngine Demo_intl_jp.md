このドキュメントでは、GME UnrealEngine Sample Projectをすばやく実行し、プロジェクトにサンプルコードを導入する方法について説明します。

## UnrealEngine Sample Projectのクイック実行 

### 環境要件

- UnrealEngine 4.22以降のバージョンを推奨します。
- Microsoft Visual Studio。
- UnrealEngineプロジェクトを実行できる構成環境。

### 前提条件

[Tencent Cloudアカウントを登録](https://intl.cloud.tencent.com/document/product/378/17985)し、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了させたことです。

### 1. GMEサービス[](id:step1)の申請

[音声サービス利用開始ガイドライン](https://www.tencentcloud.com/document/product/607/10782)を参照して、GMEリアルタイム音声サービスに申し込み、リアルタイム音声AppidとKeyを入手できます。

### 2. プロジェクトをダウンロードする

[ダウンロードガイド]（https://cloud.tencent.com/document/product/607/18521）でUnrealEngine Demoをダウンロードしてください。UE5とUE4ではDemoの設定が異なるため、対応するエンジンバージョンのSample Projectをダウンロードする必要があります。

![](https://qcloudimg.tencent-cloud.cn/raw/d31444d037de015a99b4bf3884aec906.png)


### 3. プロジェクトの設定

ダウンロード後、プロジェクトディレクトリを開き、パスSource\UEDemo1でUserConfig.cppを見つけ、図の青いボックスにあるappIDとappKeyを、[手順1](#step1)で申請したGMEリアルタイムボイスサービスのAppidとkeyに変更してください。

![](https://qcloudimg.tencent-cloud.cn/raw/e82b3bf515b0cc8ff2055dff7ac0b1e8.png)

### 4. コンパイルと実行。

#### 1. プログラムの実行

「エディタを実行」ボタン<img src="https://qcloudimg.tencent-cloud.cn/raw/302e95d032818ed9e463a0b3b3417ce4.png" width="30">![]()をクリックして、Demo実行プログラムに移行します。

![](https://qcloudimg.tencent-cloud.cn/raw/fe22948ae13046f4f8db953a6ee34e57.png)

#### 2. 初期化

- UserId：openidに相当し、各エンドのopenidは一意である必要があります。
- Voice Chat：リアルタイム音声機能インターフェース。
- Voice Message：音声メッセージ機能のインターフェース。

**Login**をクリックして初期化を行い、**Voice Chat**をクリックしてリアルタイムボイスルームの設定画面を開きます。

![](https://qcloudimg.tencent-cloud.cn/raw/b872b21122c244b443f7ff651048ca5b.jpg)

#### 3. リアルタイムボイスルームに参加する

- RoomId：部屋番号です。同じルームのメンバーが音声で話すことができます。
- RoomType：Fluencyを使用してルームに参加してください。
- JoinRoom：音声ルームに参加します。
- Back：前の画面に戻ります。

リアルタイムボイスルーム番号を設定したら、**JoinRoom**をクリックして リアルタイムボイスルームに入ります。

![](https://qcloudimg.tencent-cloud.cn/raw/4df80f35962207dcc5435eb78dd95138.jpg)

#### 4. リアルタイム音声機能
画面には、ルームのRoomidとローカル端末のopenidが表示されます。

- Mic：マイクをオンにします。
- Speaker：スピーカーをオンにします。
- 3D Voice Effect：3Dサウンドをオンにします。
- Voice Change：ボイスエフェクト。

ローカル端末でMicおよびSpeakerにチェックを入れ、もう一方の端末の機器も以上の手順を繰り返し、同じルームに参加し、MicおよびSpeakerにチェックを入れ、互いにコミュニケーションを行うことができます。
両端末とも3D Voice Effectにチェックを入れ、キーボード【A】【S】【D】【W】で方位を変え、3D音声方位感を体験できます。

![](https://qcloudimg.tencent-cloud.cn/raw/3c34c7be421a1569cb47807990ae4d07.jpg)

#### 5. 音声メッセージ機能

- Language：テキスト変換対象音声を選択し、例えば中国語を話す場合は北京語を選択します。
- Audio：録音後にクリックすると聴くことができます。
- Audio-to-Text：音声から変換されるテキスト内容。
- Push To Talk：長押しすると録音できます。
- Back：前の画面に戻ります。

**Push to Talk**ボタンを長押ししたままマイクに向かって話しかけ、ボタンを離すと音声がテキストに変換されて画面に表示されます。

![](https://qcloudimg.tencent-cloud.cn/raw/a6634573204ad4df2820357a247e8677.jpg)

## プロジェクトサンプルコードの紹介

GMEリアルタイムボイスを利用する主な手順は、Init＞EnterRoom＞EnableMic＞EnableSpeakerです。Demoの主なコードは、BaseViewController.cppおよびExperientialDemoViewController.cppにあります。


### 初期化関連

初期化に関連するコードは、BaseViewController.cppファイルのInitGME関数にあります。これには、初期化、音声メッセージの認証初期化、およびコールバックTMGDelegateの設定が含まれます。

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

GMEを使用するにはPoll関数を定期的に呼び出してください。UEDemoLevelScriptActor.cppスクリプトのTickで呼び出されます。

```
void AUEDemoLevelScriptActor::Tick(float DeltaSeconds) {
	Super::Tick(DeltaSeconds);	

	m_pTestDemoViewController->UpdateTips();
	m_pCurrentViewController->UpdatePosition();
	ITMGContextGetInstance()->Poll();
}
```

### 入室関連
入室関連のコードは、BaseViewController.cppファイルのEnterRoom関数にあります。

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

入室のコールバックは同じスクリプト内のOnEvent関数にあります。

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

### デバイスをオンにする
正常に入室すると、デバイスをオンにします。関連コードはExperientialDemoViewController.cppにあります。

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

### 3Dサウンド関連

3Dサウンドの導入について、[3Dサウンドドキュメント](https://www.tencentcloud.com/document/product/607/18218)をご参照ください。Demoでは、まず3Dサウンド機能が初期化され、関連コードはExperientialDemoViewController.cppにあります。

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

UEDemoLevelScriptActor.cppスクリプトのTickでUpdatePosition関数が呼び出されます。

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

ExperientialDemoViewController.cppで3Dサウンドをオンにします。

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
