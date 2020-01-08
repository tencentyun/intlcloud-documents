개발자가 Tencent Cloud Game Multimedia Engine(GME) 제품 API를 원활히 테스트하고 액세스하는것을 지원드리고자, 게임 멀티미디어 엔진 실시간 음성 반주 관련 액세스 기술 파일을 안내드립니다.

## 실시간 음성 반주 관련 API
|API     | API 의미   |
| ------------- |:-------------:|
|StartAccompany           |반주 플레이 시작.|
|StopAccompany       |반주 플레이 정지.|
|IsAccompanyPlayEnd|반주  플레이 완료 여부.|
|PauseAccompany    |반주 플레이 일시정지.|
|ResumeAccompany|반주 리플레이.|
|SetAccompanyVolume |반주 사운드 설정.|
|GetAccompanyVolume|반주 플레이 사운드 획득.|
|SetAccompanyFileCurrentPlayedTimeByMs |플레이 진행 상황 설정.|


>실시간 음성 반주를 원하시면 GME SDK를 액세스해야 하며, 실시간 음성 통화 시에만 실시간 음성 반주를 사용할 수 있습니다.

### 프로세스 이미지
소셜타입의 앱 호출 프로세스는 하기 이미지를 참조해주세요.
![](https://main.qcloudimg.com/raw/cdcd069530545ed560f99985b15edcc9.png)


### 반주 플레이 시작
StartAccompany API를 호출하여 반주 플레이를 시작합니다. m4a, wav, mp3 등 3종 포멧을 지원합니다. 이 API를 호출하면 사운드는 리셋됩니다.

####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int StartAccompany(const char* filePath, bool loopBack, int loopCount, int msTime) 
```

|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| filePath    |char\* |반주를 플레이하는 경로.|
| loopBack  |bool|오디오 믹싱 발송 여부, 일반적으로  true로 설정하면 타인도 반주를 들을 수 있습니다.|
| loopCount|int    |리사이클 횟수, 수치가 -1일 경우 무제한 리사이클을 의미합니다|
| msTime|int   |지연시간.|

####  예시 코드  
```
//Windows 코드
ITMGContextGetInstance()->GetAudioEffectCtrl()->StartAccompany(filePath,true,-1,0);
//Android 코드
ITMGContext.GetInstance(this).GetAudioEffectCtrl().StartAccompany(filePath,true,loopCount,0);
//iOS 코드
[[[ITMGContext GetInstance] GetAudioEffectCtrl] StartAccompany:path loopBack:isLoopBack loopCount:loopCount msTime:0];
```

### 반주 플레이 콜백
반주 플레이를 완료하면 콜백 함수는 OnEvent를 호출합니다. 이벤트 메시지는 ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH이며, OnEvent함수에서 이벤트 메시지를 판단합니다.
전송된 파라미터 data에 result와 file_path 등 2종 메시지를 포함합니다. 
#### 예시 코드  
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
		case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
		//프로세싱
		break;
	   	}
		...
        case ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH:
		{
		//프로세싱
		break;
		}
	}
}
```

### 반주 플레이 정지
StopAccompany API를 호출하여 반주 플레이를 정지합니다.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int StopAccompany(int duckerTime)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| duckerTime|int             |페이드아웃 시간.|

#### 예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopAccompany(0);
```

### 반주 플레이 완료 여부
플레이를 완료하면 리턴값은 true이며, 플레이를 완료하지 않았다면 리턴값은 false입니다. 
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual bool IsAccompanyPlayEnd()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->IsAccompanyPlayEnd();
```


### 반주 플레이 일시정지
PauseAccompany API를 호출하여 반주 플레이를 일시정지합니다.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int PauseAccompany()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseAccompany();
```


### 반주 플레이 복구 
ResumeAccompany API를 사용하여 반주 플레이를 복구합니다.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int ResumeAccompany()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeAccompany();
```

### 스스로 반주를 들을 수 있는지 설정합니다.
이 API는 자기 스스로 반주를 들을 수 있는 여부를 설정합니다.
#### 함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int EnableAccompanyPlay(bool enable)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|--------------|
| enable    |bool             |들을 수 있는지 여부.|

#### 예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->EnableAccompanyPlay(false);
```

### 타인이 반주를 들을 수 있는지 설정합니다.
타인도 반주를 들을 수 있는지 여부를 설정합니다.
#### 함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int EnableAccompanyLoopBack(bool enable)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|--------------|
| enable    |bool             |들을 수 있는지 여부.|

#### 예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->EnableAccompanyLoopBack(false);
```

### 반주 사운드 설정
SetAccompanyVolume API를 호출하여 반주 사운드를 설정합니다. 기본값은 100이며, 수치가 100보다 클 경우 사운드 증가, 수치가 100보다 작을 경우 사운드 감소, 값범위는 0-200입니다.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int SetAccompanyVolume(int vol)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| vol    |int             |사운드 수치.|

####  예시 코드  
```
int vol=100;
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetAccompanyVolume(vol);
```

### 반주 플레이 사운드 획득
GetAccompanyVolume API는 반주 사운드를 읽어옵니다.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int GetAccompanyVolume()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetAccompanyVolume();
```

### 반주 플레이 진행 상황 획득
다음 2종 API는 반주 플레이 진행 상황을 읽어옵니다.  주의 사항: Current / Total = 기존 리사이클 횟수,  Current % Total = 기존 리사이클 플레이 위치.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int GetAccompanyFileTotalTimeByMs()
ITMGAudioEffectCtrl virtual int GetAccompanyFileCurrentPlayedTimeByMs()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetAccompanyFileTotalTimeByMs();
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetAccompanyFileCurrentPlayedTimeByMs();
```


### 플레이 진행 상황 설정
SetAccompanyFileCurrentPlayedTimeByMs API는 플레이 진행 상황을 설정할 수 있습니다
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int SetAccompanyFileCurrentPlayedTimeByMs(unsigned int time)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| time    |int                |플레이 진행 상황, 단위는 밀리초임.|

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetAccompanyFileCurrentPlayedTimeByMs(time);
```


## 에러코드 리스트

|에러코드 명칭|에러코드값|에러코드 의미|솔루션|
|------|------|------|-----|
|QAV_ERR_ACC_OPENFILE_FAILED        |4001|파일 오픈 실패|파일 경로와 파일 존재 여부를 체크합니다. 파일 액세스 권한이 있는지 체크합니다.|
|QAV_ERR_ACC_FILE_FORAMT_NOTSUPPORT |4002|지원하지 않는 파일 포멧입니다|파일 포멧이 정확한지 체크합니다.|
|QAV_ERR_ACC_DECODER_FAILED         |4003|디코딩 실패|파일포멧이 정확한지 체크합니다.|
|QAV_ERR_ACC_BAD_PARAM              |4004|파라미터 에러|코드에 입력한 파라미터가 정확한지 체크합니다.|
|QAV_ERR_ACC_MEMORY_ALLOC_FAILED    |4005|메모리 할당 실패|시스템 리소스를 소진하였습니다. 혹 이 에러코드가 계속 존재하면 개발자에게 문의해주세요.|
|QAV_ERR_ACC_CREATE_THREAD_FAILED   |4006|스레드 구축 실패|시스템 리소스를 소진하였습니다. 혹 이 에러코드가 계속 존재하면 개발자에게 문의해주세요.|
|QAV_ERR_ACC_STATE_ILLIGAL          |4007|불법 상태입니다|어떤 상태가 아니며, 이 상태에 있을 시에만 허용되는 API를 호출해야 합니다. 그러지 않을 경우 이 에러가 생성합니다.|

