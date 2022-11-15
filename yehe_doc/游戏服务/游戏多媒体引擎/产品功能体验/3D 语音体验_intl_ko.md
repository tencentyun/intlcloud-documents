## 작업 시나리오
Tencent Cloud GME(Game Multimedia Engine)는 고품질을 특징으로 하는 원스톱 음성 솔루션으로 게임 산업의 응용 시나리오를 포괄적으로 다루고 있습니다. 멀티 플레이어 음성 채팅, 3D 음향 효과, 음성 메시지, 음성-텍스트 변환, 음성 콘텐츠 조정 등 다양한 기능을 지원합니다. 본 문서는 음성 채팅의 [3D Sound Effect](https://intl.cloud.tencent.com/document/product/607/18218)를 설명합니다. 플레이어는 캐릭터가 움직일 때 캐릭터의 방향 감각과 함께 스테레오 음성을 들을 수 있습니다. 또한 음원과의 거리가 멀어질수록 목소리가 약해집니다.
>!Demo는 Windows PC에서만 실행할 수 있습니다.

## 전제 조건

- 데모는 Windows 플랫폼에서 실행됩니다.
- 데모를 사용하려면 동일한 시스템에 이중으로 열린 프로그램이 필요하거나 동일한 LAN에 있는 두 시스템에 별도의 프로그램이 필요합니다.
- 컴퓨터 헤드폰과 마이크를 사용할 수 있는지 확인하십시오.
- GME의 실시간 음성 서비스를 활성화하고 사전에 AppId와 Key를 받아야 합니다. GME 서비스 신청 방법에 대한 자세한 내용은 [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오. **appId는 AppID이고 authKey는 콘솔의 권한 키입니다.** 요금 관련 자세한 내용은 [구매 가이드](https://intl.cloud.tencent.com/document/product/607/50009)를 참고하십시오.


## 작업 단계
### 1. Demo 다운로드

클릭하여 [3D 음성 데모](https://picture-1256313114.cos.ap-beijing.myqcloud.com/GMEDemo.zip)를 다운로드하고 압축을 해제합니다.

### 2. Demo 열기

더블 클릭하여 **GMEDemo.exe** 파일을 엽니다. 동일한 장치에서 두 개의 Demo를 동시에 열 수 있습니다.

### 3. 데모 초기화

<img src="https://main.qcloudimg.com/raw/33540519cd5c2bdde6139f8a4af537a6.png"  width="50%"><br>
데모를 초기화하려면 [GME 콘솔](https://console.cloud.tencent.com/gamegme/detail/1400391524)의 서비스 관리에서 찾을 수 있는 AppID와 권한 키를 입력해야 합니다.

- appId: 콘솔에서 Appid를 입력합니다.
- userId: Demo에서 자동으로 생성되며 필요에 따라 설정할 수 있습니다. 고유해야 하며 중복될 수 없습니다.
- authKey: 콘솔에서 권한 키를 입력합니다.
- **초기화** -> **실시간 음성 채팅**을 클릭하여 음성 채팅방 설정 페이지로 이동합니다.

>! 
>- AppID와 키가 유출되지 않도록 잘 보관하시기 바랍니다.
>- 다른 데모 애플리케이션의 userId가 현재 userId와 다른지 확인하십시오.

### 4. 음성 채팅방 입장

<img src="https://main.qcloudimg.com/raw/7393dbb31007299894586205cb8b6f9c.jpg"  width="50%">

음성 채팅방 선택 페이지에서 방 ID를 입력할 수 있습니다. 다른 데모를 열면 동일한 방 ID를 입력하십시오.

- 문자열 또는 숫자로 된 방 ID를 입력합니다.
- **JoinRoom**을 클릭하여 음성 채팅방으로 들어갑니다.

### 5. 게임 UI 개요

<img src="https://main.qcloudimg.com/raw/0e451b80402caeb31cf6bd932acee127.png"  width="50%"/></img>

아래 인터페이스 세부 정보를 참고하십시오.

- 나가기: 클릭하면 음성 채팅방 선택 페이지로 돌아갑니다.
- 마이크 활성화/비활성화: 방의 마이크는 기본적으로 꺼져 있습니다. 전화를 걸려면 마이크를 활성화해야 합니다.
- 사용: 클릭하면 사용 페이지가 열립니다.
- 반주 켜기: 클릭하면 반주 재생이 시작됩니다.
- 인터페이스 우측 하단 : 음성 채팅방에 입장하고 퇴장한 사용자를 보여주는 방 로그 정보입니다.
- 인터페이스 왼쪽: 로컬 연결 버튼. 게임이 공식적으로 시작되기 전에 구성해야 합니다.



### 6. 로컬 연결 구성

<img src="https://main.qcloudimg.com/raw/670b24a1133dc07bdc9892ffa12b159f.png" width="50%" /></img>

>!이 데모에는 로컬 LAN 연결 기반이 필요합니다.

- **방에 처음 입장하는 사람**
  방에 들어가는 첫 번째 사람은 네트워크 연결 Host입니다. **LAN Host(H)**를 클릭하면 코인 옆에 캐릭터가 생성됩니다.
  <img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/master.gif"  width="50%"/></img>
- **다음 사람**
  **LAN Client(C)**를 클릭하여 다음과 같은 사람이 Host에 연결되어야 하며 해당 캐릭터는 코인 옆에 표시됩니다. 이제 그들은 방에 들어오는 첫 번째 사람들을 볼 수 있습니다.
  <img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/client.gif"  width="50%"/></img>
- **연결 성공 여부 판단을 위한 정보**
  1. 게임 UI에서 상대방의 게임 캐릭터를 볼 수 있습니다. 
  2. UI 우측 하단의 로그에 상대방의 게임 캐릭터 userID의 방 입장 기록이 표시됩니다.

### 7. 마이크 활성화

<img src="https://main.qcloudimg.com/raw/1fd9f4e3f35cfc166e04bd26fb520abf.png" width="3%"></img> 버튼을 클릭하여 마이크를 켜면 방 구성원들과 대화할 수 있습니다.

### 8. 작업 방식

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/linaji.gif"  width="50%"/></img>

키보드의 "W", "S", "A", "D"는 각각 ‘전’, ‘후’, ‘좌’, ‘우’에 해당합니다. 마우스를 사용하여 원근을 조절할 수 있습니다. 연결된 클라이언트는 다른 클라이언트가 운영하는 캐릭터를 참고하십시오.

### 9. 체험 방법

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/yuan.gif"  width="50%"/></img>

로컬에서 2개의 인스턴스에서 데모를 열면 한 데모의 시점을 코인으로 이동하고 마이크를 활성화하고 다른 데모의 캐릭터가 가능한 한 멀리 도망가서 계속 말하게 할 수 있습니다. 이런 식으로 3D 음향 효과를 시험해 볼 수 있습니다. 캐릭터가 맵 경계에 있을 때 음성은 거의 들리지 않습니다.



