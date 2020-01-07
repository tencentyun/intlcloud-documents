개발자가 Tencent Cloud Game Multimedia Engine(GME) 제품 API를 테스트하고 액세스하는 편의성을 위해 GME 실시간 음성 채팅 효과음을 액세스하는 기술 파일을 소개드립니다.


## 실시간 음성 채팅 효과음 관련 API
|API     | API 의미   |
| ------------- |:-------------:|
|PlayEffect    |효과음 플레이.|
|PauseEffect    |효과음 플레이 일시정지.|
|PauseAllEffects|전체 효과음 일시정지.|
|ResumeEffect    |효과음 리플레이.|
|ResumeAllEffects|전체 효과음 리플레이.|
|StopEffect |효과음 플레이 스톱.|
|StopAllEffects|전체 효과음 플레이 스톱.|
|SetVoiceType |변성 이펙트.|
|SetKaraokeType |노래방 효과음 이펙트.|
|GetEffectsVolume|플레이하는 효과음의 사운드를 획득.|
|SetEffectsVolume |플레이하는 효과음 사운드를 설정.|


### 효과음 플레이
PlayEffect API는 효과음을 플레이합니다. 파라미터터중 효과음 ID는 앱에서 관리해야 하며, ID는 낱개 플레이 이벤트를 의미합니다. 향후 이 ID로 대응하는 플레이를 제어할 수 있습니다. 파일은 m4a, wav, mp3 등 3종 포멧을 지원합니다.
#### 함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int PlayEffect(int soundId,  const char* filePath, bool loop, double pitch, double pan, double gain)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| soundId    |int    |효과음 ID.|
| filePath    |char\*     |효과음 경로.|
| loop    |bool  |반복 플레이 여부.|
| pitch    |double|플레이 빈도, 디폴트는 1.0, 해당 값이 작을 수록 플레이 속도가 느리고, 시간이 길어집니다.|
| pan    |double|사운드트랙, 값범위는 -1.0부터1.0사이이며, -1.0은 왼쪽 채널(FL)만 오픈함을 의미합니다.|
| gain    |double|사운드 추가, 값버위는 0.0-1.0이며, 기본값은 1.0입니다.|

####  예시 코드  
```
double pitch = 1.0;
double pan = 0.0;
double gain = 0.0;
//Windows 시스템
ITMGContextGetInstance()->GetAudioEffectCtrl()->PlayEffect(soundId,filepath,true,pitch,pan,gain);
//Android 시스템
ITMGContext.GetInstance(this).GetAudioEffectCtrl().PlayEffect(soundId,filePath,loop);
//iOS 시스템
[[[ITMGContext GetInstance] GetAudioEffectCtrl] PlayEffect:soundId filePath:path loop:isLoop];
```


### 효과음 플레이 일시정지
PauseEffect API는 효과음 플레이를 일시정지합니다.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int PauseEffect(int soundId)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| soundId    |int                    |효과음 ID.|

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseEffect(soundId);
```

### 전체 효과음 일시정지
PauseAllEffects API를 호출하여 전체 효과음을 일시정지합니다.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int PauseAllEffects()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseAllEffects();
```

### 효과음 리플레이
ResumeEffect API는 효과음을 리플레이합니다.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int ResumeEffect(int soundId)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| soundId    |int                    |효과음 ID.|

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeEffect(soundId);
```



### 전체 효과음 리플레이
ResumeAllEffects API를 호출하여 전체 효과음을 리플레이합니다.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int ResumeAllEffects()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeAllEffects();
```

### 효과음 플레이 스톱
StopEffect API는 효과음 플레이를 스톱합니다.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int StopEffect(int soundId)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| soundId    |int                    |효과음 ID.|

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopEffect(soundId);
```

### 전체 효과음 플레이 스톱
StopAllEffects API를 호출하여 전체 효과음 플레이를 스톱합니다.
#### 함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int StopAllEffects()
```


#### 예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopAllEffects();
```



### 변성 이펙트
SetVoiceType API를 호출하여 변성 이펙트를 설정합니다.
#### 함수 프로토타입  
```
TMGAudioEffectCtrl int setVoiceType(int type)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| type    |int                    |이 터널의 가청 주파수 변성 타입을 의미합니다.|



|타입파라미터     |파라미터 대표|의미|
| ------------- |-------------|------------- |
| ITMG_VOICE_TYPE_ORIGINAL_SOUND  |0|오리지널 사운드.|
| ITMG_VOICE_TYPE_LOLITA    |1|로리.|
| ITMG_VOICE_TYPE_UNCLE  |2|아저씨.|
| ITMG_VOICE_TYPE_INTANGIBLE    |3|헤븐.|
| ITMG_VOICE_TYPE_DEAD_FATBOY  |4|집돌이.|
| ITMG_VOICE_TYPE_HEAVY_MENTA|5|헤비메탈.|
| ITMG_VOICE_TYPE_DIALECT |6|외국인.|
| ITMG_VOICE_TYPE_INFLUENZA |7|감기.|
| ITMG_VOICE_TYPE_CAGED_ANIMAL |8|코너에 몰린 몬스터.|
| ITMG_VOICE_TYPE_HEAVY_MACHINE|9|헤비 머신.|
| ITMG_VOICE_TYPE_STRONG_CURRENT|10|고전류.|
| ITMG_VOICE_TYPE_KINDER_GARTEN|11|유치원.|
| ITMG_VOICE_TYPE_HUANG |12|미니언즈.|

#### 예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->setVoiceType(0);
```

### 노래방 효과음 이펙트
SetKaraokeType API를 호출하여 노래방 효과음 이펙트를 설정합니다.
####  함수 프로토타입  
```
TMGAudioEffectCtrl int SetKaraokeType(int type)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| type    |int                    |이 터널의 가청 주파수 변셩 타입을 의미합니다.|


|타입파라미터     |파라미터代表|의미|
| ------------- |-------------|------------- |
|ITMG_KARAOKE_TYPE_ORIGINAL |0|오리지널 사운드.|
|ITMG_KARAOKE_TYPE_POP |1|팝.|
|ITMG_KARAOKE_TYPE_ROCK |2|록.|
|ITMG_KARAOKE_TYPE_RB |3|힙합.|
|ITMG_KARAOKE_TYPE_DANCE |4|댄스곡.|
|ITMG_KARAOKE_TYPE_HEAVEN |5|헤븐.|
|ITMG_KARAOKE_TYPE_TTS |6|음성 TTS.|

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetKaraokeType(0);
```

### 플레이 효과음 볼륨 획득
GetEffectsVolume API를 호출하여 플레이하는 효과음 볼륨을 읽어옵니다. 스레드 볼륨으로, 기본값은 100이며, 값이 100을 초과하면 효과가 증가되며, 값이 100보다 작을 경우 효과가 줄어듭니다.
#### 함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int GetEffectsVolume()
```
#### 예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetEffectsVolume();
```

### 플레이하는 효과음 볼륨을 설정합니다.
SetEffectsVolume API를 호출하여 플레이하는 효과음 볼륨을 설정합니다.
#### 함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int SetEffectsVolume(int volume)
```
|파라미터     | 타입         |의미|
| ------------- |:-------------:|-------------|
| volume    |int                    |볼륨 수치.|

#### 예시 코드  
```
int volume=1;
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetEffectsVolume(volume);
```

