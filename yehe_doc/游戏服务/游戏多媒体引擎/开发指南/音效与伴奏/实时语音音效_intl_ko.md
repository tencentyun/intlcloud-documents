본문은 개발자가 쉽게 디버깅하고 통합할 수 있도록 음성 채팅 음향 효과용 Game Multimedia Engine(GME) API에 대해 설명합니다.


## 전제 조건

- **음성 채팅 서비스 활성화**: [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오.
- **GME SDK 통합**: 핵심 API 및 음성 채팅 API를 포함합니다. 자세한 내용은 [Quick Integration of Native SDK](https://intl.cloud.tencent.com/document/product/607/40858), [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544), [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545)을 참고하십시오.
- GME의 음성 채팅 기능을 이용하여 성공적으로 음성 룸에 입장하고 마이크(EnableMic)와 스피커(EnableSpeaker)를 켰습니다.


## 음성 채팅 음향 효과용 API
|API     | 설명   |
| ------------- |:-------------:|
|PlayEffect    |음향 효과 재생|
|PauseEffect    |음향 효과 일시 중지|
|PauseAllEffects|모든 음향 효과 일시 중지|
|ResumeEffect    |음향 효과 다시 시작|
|ResumeAllEffects|모든 음향 효과 다시 시작|
|StopEffect |음향 효과 중지|
|StopAllEffects|모든 음향 효과 중지|
|SetVoiceType |음성 변조 효과 설정|
|SetKaraokeType |노래방 음향 효과 설정|
|GetEffectsVolume|음향 효과의 볼륨 가져오기|
|SetEffectsVolume |음향 효과의 볼륨 설정|


### 음향 효과 재생
API PlayEffect는 음향 효과를 재생하는 데 사용됩니다. 독립적인 재생 이벤트를 나타내는 음향 효과 ID는 App에서 관리해야 합니다. 이 ID로 재생을 제어할 수 있습니다. 이 파일은 m4a, wav 및 mp3 형식을 지원합니다.

#### 함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int PlayEffect(int soundId,  const char* filePath, bool loop, double pitch, double pan, double gain)
```

|매개변수     | 유형         |설명|
| ------------- |:-------------:|-------------|
| soundId    |int    |음향 효과 ID|
| filePath    |char\*     |음향 효과 경로|
| loop    |bool  |재생 반복 여부|
| pitch    |double|회수 빈도, 기본값은 1.0이며, 값이 작을수록 재생 속도가 느려지고 재생 시간이 길어집니다 |
| pan    |double|사운드 채널, 값범위는 -1.0에서 1.0사이이며, -1.0은 왼쪽 채널만 활성화됨을 의미합니다|
| gain    |double|볼륨을 얻고, 값범위는 0.0에서 1.0사이이며, 기본값은 1.0입니다|

####  예시 코드  
```
double pitch = 1.0;
double pan = 0.0;
double gain = 0.0;
//Windows
ITMGContextGetInstance()->GetAudioEffectCtrl()->PlayEffect(soundId,filepath,true,pitch,pan,gain);
//Android
ITMGContext.GetInstance(this).GetAudioEffectCtrl().PlayEffect(soundId,filePath,loop);
//iOS
[[[ITMGContext GetInstance] GetAudioEffectCtrl] PlayEffect:soundId filePath:path loop:isLoop];
```


### 음향 효과 일시중지
API PauseEffect는 사운드 효과를 일시 중지하는 데 사용됩니다.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int PauseEffect(int soundId)
```

|매개변수     | 유형         |설명|
| ------------- |:-------------:|-------------|
| soundId    |int                    |음향 효과 ID|

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseEffect(soundId);
```

### 모든 음향 효과 일시 중지
API PauseAllEffects는 모든 음향 효과를 일시 중지하는 데 사용됩니다.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int PauseAllEffects()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->PauseAllEffects();
```

### 음향 효과 다시 시작
API ResumeEffect는 음향 효과를 다시 시작하는 데 사용됩니다.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int ResumeEffect(int soundId)
```

|매개변수     | 유형         |설명|
| ------------- |:-------------:|-------------|
| soundId    |int                    |음향 효과 ID|

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeEffect(soundId);
```



### 모든 음향 효과 다시 시작
API ResumeAllEffects는 모든 사운드 효과를 재개하는 데 사용됩니다.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int ResumeAllEffects()
```
####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->ResumeAllEffects();
```


### 음향 효과 중지
API StopEffect는 음향 효과를 중지하는 데 사용됩니다.
####  함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int StopEffect(int soundId)
```

|매개변수     | 유형         |설명|
| ------------- |:-------------:|-------------|
| soundId    |int                    |음향 효과 ID|

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopEffect(soundId);
```

### 모든 음향 효과 중지
API StopAllEffects는 모든 사운드 효과를 중지하는 데 사용됩니다.
#### 함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int StopAllEffects()
```


#### 예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->StopAllEffects();
```



### 음성 변조 효과 설정
API SetVoiceType은 음성 변조 효과를 설정하는 데 사용됩니다.
#### 함수 프로토타입  
```
TMGAudioEffectCtrl int setVoiceType(int type)
```

|매개변수     | 유형         |설명|
| ------------- |:-------------:|-------------|
| type    |int                    |로컬 음성 변조 효과의 유형을 나타냅니다.|



|유형 매개변수     |값|설명|
| ------------- |-------------|------------- |
| ITMG_VOICE_TYPE_ORIGINAL_SOUND  |0|오리지널|
| ITMG_VOICE_TYPE_LOLITA    |1|로리타|
| ITMG_VOICE_TYPE_UNCLE  |2|삼촌|
| ITMG_VOICE_TYPE_INTANGIBLE    |3|오묘한|
| ITMG_VOICE_TYPE_DEAD_FATBOY  |4|통통이|
| ITMG_VOICE_TYPE_HEAVY_MENTA|5|헤비메탈|
| ITMG_VOICE_TYPE_DIALECT |6|외국|
| ITMG_VOICE_TYPE_INFLUENZA |7|감기|
| ITMG_VOICE_TYPE_CAGED_ANIMAL |8|동물|
| ITMG_VOICE_TYPE_HEAVY_MACHINE|9|기계|
| ITMG_VOICE_TYPE_STRONG_CURRENT|10|강한 전류|
| ITMG_VOICE_TYPE_KINDER_GARTEN|11|유치원|
| ITMG_VOICE_TYPE_HUANG |12|미니언|

#### 예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->setVoiceType(0);
```

### 노래방 음향 효과 설정
API SetKaraokeType은 노래방 음향 효과를 설정하는 데 사용됩니다.
####  함수 프로토타입  
```
TMGAudioEffectCtrl int SetKaraokeType(int type)
```

|매개변수     | 유형         |설명|
| ------------- |:-------------:|-------------|
| type    |int                    ||로컬 음성 변조 효과의 유형을 나타냅니다.|


|유형 매개변수     |값|설명|
| ------------- |-------------|------------- |
|ITMG_KARAOKE_TYPE_ORIGINAL |0|오리지널|
|ITMG_KARAOKE_TYPE_POP |1|팝|
|ITMG_KARAOKE_TYPE_ROCK |2|록|
|ITMG_KARAOKE_TYPE_RB |3|힙합|
|ITMG_KARAOKE_TYPE_DANCE |4|댄스|
|ITMG_KARAOKE_TYPE_HEAVEN |5|오묘한 |
|ITMG_KARAOKE_TYPE_TTS |6|음성 합성 |

####  예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetKaraokeType(0);
```

### 음향 효과의 볼륨 가져오기
API GetEffectsVolume은 음향 효과의 볼륨을 얻는 데 사용됩니다. 기본값은 100입니다. 100보다 큰 값은 볼륨 업을 의미하고 100 미만의 값은 볼륨 다운을 의미합니다.
#### 함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int GetEffectsVolume()
```
#### 예시 코드  
```
ITMGContextGetInstance()->GetAudioEffectCtrl()->GetEffectsVolume();
```

### 음향 효과 볼륨 설정
API SetEffectsVolume은 음향 효과의 볼륨을 설정하는 데 사용됩니다.
#### 함수 프로토타입  
```
ITMGAudioEffectCtrl virtual int SetEffectsVolume(int volume)
```

|매개변수     | 유형         |설명|
| ------------- |:-------------:|-------------|
| volume    |int                    |볼륨 값|

#### 예시 코드  
```
int volume=1;
ITMGContextGetInstance()->GetAudioEffectCtrl()->SetEffectsVolume(volume);
```
