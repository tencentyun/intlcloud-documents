텐센트 클라우드 게임 멀티 미디어 엔진 제품 API를 쉽게 디버깅 및 액세스하기 위해 개발된 인터페이스 업그레이드 기술 문서(GME 2.2 업그레이드 GME 2.3.5)를 소개합니다.

## SDK 변경
### 새로운 기능
- 실시간 음성 채팅 중 오프라인 음성을 사용할 수 있습니다.
- 실시간 음성 채팅 중 공포, 포르노 및 정치 등 정보를 필터링합니다.
- 전체 플랫폼에서 실시간 음성 채팅을 위한 H5 실시간 음성 채팅을 지원합니다.
- 안드로이드 v8a 아키텍처 지원이 추가되었습니다.
- Android의 저 지연 재생을 지원합니다.

### 최적화 기능
- SDK의 범위에서 음성 기능의 인터페이스를 최적화하여 진입 장벽을 낮춥니다.
- 음성 소음 감소 효과를 최적화합니다.
- SDK 메모리 사용량을 대폭 줄입니다.

## 주요 인터페이스 변경
### EnterRoom 
체크 인 작업이 동기화에서 비동기화로 변경되었을 때 리턴값이 0이면 비동기 전달이 성공하였음을 의미하고 콜백 함수가 처리되기를 기다립니다. 리턴값이 0이 아닌 경우 비동기 전달이 실패함을 의미합니다.

```
public abstract int EnterRoom();
```

### ExitRoom 
체크 아웃 작업이 동기화에서 비동기화로 변경되었을 때 RoomExitComplete 콜백 함수를 참고하며 처리됩니다. 리턴값이 AV_OK이면 비동기 전달이 성공하였음을 의미합니다.

>!애플리케이션에서 체크 아웃 직후 체크 인이 실행되는 작업 환경이 있는 경우 개발자는 인터페이스 호출 프로세스에서 ExitRoom의 콜백 RoomExitComplete 알림을 기다릴 필요가 없습니다. 인터페이스를 직접 호출하면 됩니다.

```
public abstract int ExitRoom();
```

## 에러코드 변경
모든 에러코드를 동일하게 처리할 경우, AV_OK를 사용하십시오; 

각 유형의 에러코드를 개별적으로 처리해야하는 경우, 인터페이스에서 리턴된 에러코드 유형의 인터페이스에 주의하십시오. 오류 코드 "1"은 명확한 내용이 없으며 2.3.5 이후 버전은 더 이상 리턴되지 않으므로 삭제하십시오.


## 기타 인터페이스 변경
### PauseAudio/ResumeAudio 

```
public int PauseAudio()
public int ResumeAudio()
```

2.3 이전 버전의 SDK 인터페이스가 호출된 경우 ITMGAudioCtrl:: PauseAudio / ResumeAudio라는 두 개의 인터페이스가 있다면 다음 표를 참조하시고 버전을 비교하십시오.


|2.3 이전 버전|업그레이드 2.3 버전|
|---|---|
|사용 목적은 기타 모듈과 상호 배타적이므로|PauseAudio를 Pause로 변경하고 ResumeAudio를 Resume으로 변경합니다.|
|사용 목적은 실시간 음성 채팅의 오프라인 음성에 사용하여| PauseAudio 및 ResumeAudio 제거합니다.|


### SetLogLevel 인터페이스 파라미터 변경

#### 기존 인터페이스
```
ITMGContext virtual void SetLogLevel(int logLevel, bool enableWrite, bool enablePrint)
```

#### 새로운 인터페이스
```
ITMGContext virtual void SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### 파라미터 내용

|파라미터|유형|내용|
|---|---|---|
|levelWrite|ITMG_LOG_LEVEL|입력 로그 레벨을 설정하십시오. TMG_LOG_LEVEL_NONE은 사용하지 않음을 의미합니다. |
|levelPrint|ITMG_LOG_LEVEL|인쇄 로그 레벨을 설정하십시오. TMG_LOG_LEVEL_NONE은 인쇄하지 않음을 의미합니다.|

#### ITMG_LOG_LEVEL 유형

|ITMG_LOG_LEVEL|내용|
|-------------------------------|-------------|
|TMG_LOG_LEVEL_NONE=0|로그를 인쇄하지 않습니다.|
|TMG_LOG_LEVEL_ERROR=1|로그 인쇄 에러코드(기본값)|
|TMG_LOG_LEVEL_INFO=2|로그 표시 인쇄|
|TMG_LOG_LEVEL_DEBUG=3|개발 디버깅 로그 인쇄|
|TMG_LOG_LEVEL_VERBOSE=4|고빈도 로그 인쇄|
