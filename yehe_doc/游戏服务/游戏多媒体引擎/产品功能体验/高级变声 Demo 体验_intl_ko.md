## 작업 시나리오
Tencent Cloud GME(Game Multimedia Engine)는 고품질을 특징으로 하는 원스톱 음성 솔루션으로 게임 산업의 응용 시나리오를 포괄적으로 다루고 있습니다. 멀티플레이어 음성 채팅, 3D 음향 효과, 음성 메시지, 음성-텍스트 변환, 음성 콘텐츠 조정 등 다양한 기능을 지원합니다. 플레이어는 GME의 고급 음성 변조 효과를 사용하여 게임 내 음성 채팅에서 자유롭게 음성을 변경할 수 있습니다.
>!Demo는 Windows PC에서만 실행할 수 있습니다.

## 전제 조건

- 데모는 Windows 플랫폼에서 실행됩니다.
- 데모를 사용하려면 동일한 시스템에 이중으로 열린 프로그램이 필요하거나 동일한 LAN에 있는 두 시스템에 별도의 프로그램이 필요합니다.
- 컴퓨터 헤드폰과 마이크를 사용할 수 있는지 확인하십시오.
- GME의 실시간 음성 서비스를 활성화하고 사전에 AppId와 Key를 받아야 합니다. GME 서비스 신청 방법에 대한 자세한 내용은 [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오. **appId는 AppID이고 authKey는 콘솔의 권한 키입니다.** 요금 관련 자세한 내용은 [구매 가이드](https://intl.cloud.tencent.com/document/product/607/50009)를 참고하십시오.

## 작업 단계
### 1. 데모 열기

[고급 음성 변조 효과 체험 데모](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GMEDemoWithVoicemod_1.0.zip)를 클릭하여 다운로드하고 압축을 풉니다. 더블 클릭하여 **TMGSDK_For_Audio_ApiExample.exe** 파일을 열고 데모를 실행합니다.

UI는 다음과 같습니다.

<img src="https://qcloudimg.tencent-cloud.cn/raw/ced85aa2b117bad61fe538c2e3a1252e.png" width=80%/><img>

### 2. AppID 및 Key 입력

데모를 초기화하려면 [GME 콘솔](https://console.cloud.tencent.com/gamegme)의 서비스 관리에서 찾을 수 있는 AppID와 권한 키를 입력해야 합니다. [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)의 안내에 따라 GME 서비스를 신청할 수 있습니다. **AppID 및 Key는 각각 콘솔의 AppID 및 권한 키입니다.**

<dx-alert infotype="explain" title="">

- AppID와 키가 유출되지 않도록 잘 보관하시기 바랍니다.
- 다른 데모 애플리케이션의 userId가 현재 userId와 다른지 확인하십시오.
  </dx-alert>

### 3. 데모 초기화

**Init**를 클릭하여 초기화합니다.

### 4. 방 입장

**EnterRoom**을 클릭하여 방에 입장합니다.

### 5. 장치 활성화

**EnableMic**, **EnableSpeaker**, **EnableLoopback**을 클릭하여 장치 및 인이어 모니터링을 활성화합니다.

### 6. 효과 경험

마이크에 대고 말하면서 음성 변화 효과를 경험하십시오.

구성 설명:

<img src="https://qcloudimg.tencent-cloud.cn/raw/791e556855f15dfb3005040a8c4d1d27.png" width=80%/><img>

### 7. 방 퇴장

테스트가 끝나면 **ExitRoom**을 클릭하여 방을 종료합니다. 그렇지 않으면 추가 요금이 발생할 수 있습니다.



