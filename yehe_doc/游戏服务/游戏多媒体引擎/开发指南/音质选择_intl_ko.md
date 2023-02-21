본문은 Tencent Cloud Game Multimedia Engine(GME)에서 음질을 선택하는 방법을 설명합니다.

## 음질 유형 소개

|음질 유형     |설명|매개변수|비트 레이트|샘플링 레이트|볼륨 유형|적용 가능한 시나리오|
| ------------- |------------ | ---- |---- |---- |---- |---- |
| ITMG_ROOM_TYPE_FLUENCY|Smooth|1|30kbps |16k |<li>스피커: 통화 볼륨</li><li>헤드셋: 미디어 볼륨</li><li>블루투스 헤드셋: HFP 프로토콜, 헤드셋 수집</li>|초저지연 실시간 원활 음질로 FPS 및 MOBA와 같은 게임의 팀 음성 채팅에 적합 |
| ITMG_ROOM_TYPE_STANDARD|Standard|2|64kbps|48k |<li>스피커: 통화 볼륨</li><li>헤드셋: 미디어 볼륨</li><li>Bluetooth 헤드셋: HFP 프로토콜을 통한 헤드셋 오디오 캡처</li>|적정 대기 시간의 비교적 우수한 음질로 Werewolves 및 보드 게임과 같은 캐주얼 게임의 음성 채팅에 적합|
| ITMG_ROOM_TYPE_HIGHQUALITY|HD|3|64kbps|48k|<li>스피커: 미디어 볼륨</li><li>헤드셋: 미디어 볼륨</li><li>Bluetooth 헤드셋: a2dp 프로토콜을 통한 휴대폰 오디오 캡처</li>|상대적으로 대기 시간이 긴 HD 음질로 음악 재생 및 온라인 노래방과 같이 높은 음질을 요구하는 음악 및 댄스 게임 및 음성 채팅 App에 적합|

<dx-alert infotype="notice" title="주의">
버전 2.9.0 이상, Unity, UnrealEngine, Cocos SDK 표준 음질 및 고화질 음질을 사용하려면 [업그레이드 가이드](https://intl.cloud.tencent.com/document/product/607/32363)를 참고하여 연결하십시오.
</dx-alert>


## 관련 개념 소개
### 미디어 볼륨 및 통화 볼륨
휴대폰에는 미디어 볼륨과 통화 볼륨의 두 가지 볼륨 모드가 구성되어 있습니다. 미디어 볼륨은 일반적으로 미디어 파일을 재생하는 데 사용되며 통화 볼륨은 전화 통화 및 통신에 사용됩니다.

Android 휴대폰의 경우 볼륨 키를 누르면 현재 볼륨 유형이 화면에 표시됩니다. 아래 그림과 같이 통화 볼륨은 왼쪽에 있고 미디어 볼륨은 오른쪽에 있습니다.


<img src="https://qcloudimg.tencent-cloud.cn/raw/e3418f5852fbe68affa6481b05ed96df.png"  width="10%" /></img>


<dx-fold-block title="미디어 볼륨 및 통화 볼륨">
[방에 들어간 후에는 휴대폰 볼륨이 매우 낮아졌다가 마이크를 켜면 매우 높아집니다. 어떻게 해결합니까?](https://intl.cloud.tencent.com/document/product/607/39524)
</dx-fold-block>

### 블루투스 헤드셋 프로토콜

오디오 성능이 다른 두 가지 Bluetooth 헤드셋 프로토콜이 있습니다.


| 프로토콜 | 재생 성능 | 성능 캡처 |
|---------|---------|---------|
| HFP |  헤드셋 오디오는 모노 전용입니다| 헤드셋 오디오를 캡처할 수 있습니다 |
| a2dp |  헤드셋 오디오는 스테레오이며 오디오 품질이 더 좋습니다| 헤드셋 오디오는 이 채널을 통해 직접 캡처할 수 없으며 전화 또는 PC 마이크를 사용하여 오디오를 캡처해야 합니다 |


### 트래픽 소모량

트래픽 소모량은 방에서 통화하는 사용자의 수 및 비트 레이트와 관련이 있습니다. 계산 공식: 비트 레이트 × 사용자 수 / 8 = 바이트 수.

### 오디오 처리 효과
오디오 신호는 모바일 장치의 캡처 모듈에 의해 수집되며 믹싱 제거, 노이즈 감소 및 자동 게인 제어와 같은 오디오 전처리 프로세스를 거쳐 오디오 인코더에 의해 인코딩됩니다. 전처리 과정에서 사용되는 Acoustic Echo Cancelling(AEC), Automatic Gain Control(AGC), Automatic Noise Suppression(ANS, noise cancellation, noise suppression라고도 함) 방법은 일반적으로 3A로 알려져 있습니다.
- 원활 음질과 다른 두 가지 음질의 차이는 ANS(노이즈 감소)입니다. ANS는 원활 음질에 활성화되고 표준 및 HD 음질에는 비활성화됩니다.
