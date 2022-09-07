
<table>
  <tbody><tr>
    <th style="text-align:center;" width="150px"><b>Android<br></b>아래 QR코드 스캔</th>
    <th style="text-align:center;" width="150px"><b>iOS<br></b>아래 QR코드 스캔</th>
  </tr>
  <tr>
    <td style="
    text-align: center;
"><img style="width:150px; max-width: inherit;" src="https://main.qcloudimg.com/raw/17b2a65547432f5d81391fce1fa17a90.png" class="zoom-img-hover"></td>
    <td style="
    text-align: center;
"><img style="width:150px; max-width: inherit;" src="https://main.qcloudimg.com/raw/17b2a65547432f5d81391fce1fa17a90.png" class="zoom-img-hover"></td>
  </tr>
</tbody></table>

## Android/iOS Unity Demo

<span id="test"></span>

### 로그인

UserId를 입력하고 **Login**을 클릭합니다. 로그인하면 화면에 **Voice Chat** 및 **Voice Message**라는 두 개의 새로운 버튼이 표시됩니다.
<img src="https://main.qcloudimg.com/raw/dbacd4455622253ddb07d53e1bc785b8.png"  width="80%" /></img><br>
- **Voice Chat**을 클릭하면 [음성 채팅](#test1)이 시작됩니다.
- **Voice Message**를 클릭하면 [음성 메시지](#test2)를 보낼 수 있습니다.

<span id="test1"></span>

### 음성 채팅


1. [로그인](#test) 후 음성 채팅을 클릭하여 **Voice Chat** 페이지로 이동합니다:
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_KuI8ov.gif"    width="80%"/></img><br>
 - RoomId: 방의 ID입니다. 같은 방 ID를 가진 사용자가 같은 방에 입장합니다.
 - RoomType: 음질을 제어합니다.
    - Fluency: 부드러운 음질. 초저지연 실시간 음성 채팅 기능으로 FPS 및 MOBA와 같은 게임 내 파티플레이에 적합합니다.
    - Standard: 표준 음질. 음질도 좋고 딜레이도 적당하여 마피아 게임 및 보드 게임과 같은 캐주얼 게임의 음성 채팅에 적합합니다.
    - High Quality: HD 음질. 초고음질과 상대적으로 높은 지연 시간으로 음악 및 댄스 게임 및 음성 채팅 App에 적합하며 음악 재생 및 온라인 노래방과 같은 고음질이 요구되는 시나리오에 적합합니다.


2. **JoinRoom**을 클릭하여 방에 입장합니다:
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_8zP4w2.gif"  width="80%"/><br>
 - Talking Members: 방에서 말하고 있는 구성원을 지정합니다. 해당 구성원의 ID는 방 화면에 표시됩니다.
 - Mic: 이 체크박스를 선택하면 마이크가 활성화됩니다. 
 - Speaker: 이 체크박스를 선택하면 스피커가 활성화됩니다.
 - 3D Voice Effect: 이 체크박스를 선택하면 3D 음성 효과가 활성화됩니다. 이 경우 다음을 구성해야 합니다.
    - Range: 게임 엔진의 거리 단위를 사용하여 오디오를 수신 범위를 지정합니다.
    - X: 자체 X축.
    - Y: 자체 Y축.
    - Z: 자체 Z축.
    - XR: X축을 중심으로 회전하는 각도.
    - YR: Y축을 중심으로 회전하는 각도.
    - ZR: Z축을 중심으로 회전하는 각도.
 - Voice Change: 다양한 실시간 음성 효과를 제공합니다. 자세한 내용은 [Real-time Sound Effect](https://intl.cloud.tencent.com/document/product/607/31503#k-.E6.AD.8C.E9.9F.B3.E6.95.88.E7.89.B9.E6.95.88)를 참고하십시오.


<span id="test2"></span>

### 음성 메시지 텍스트 변환

[로그인](#test) 후 **Voice Message**를 클릭하여 음성 메시지 페이지로 이동합니다.
<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_DsvaLv.gif"  width="80%"/></img><br>
- Language: 음성 메시지에 사용되는 언어를 지정합니다.
- Audio: 음성 메시지의 녹음 및 지속 시간입니다. <img src="https://main.qcloudimg.com/raw/7d268c4b1bb7e1998792b19a23e7bb63.png" width="3%"></img>을(를) 클릭하여 녹음을 재생하고, 중지하려면 다시 클릭합니다.
- Audio-to-Text: 오디오에서 변환된 텍스트. **Push To Talk**를 클릭한 상태로 녹음을 시작하고 **Push To Talk** 버튼에서 손을 떼면 녹음이 중지됩니다.


## Windows 3D 음성 Demo


### 전제 조건
- 본 데모는 Windows 플랫폼에서 실행해야 합니다.
- 데모를 사용하려면 동일한 장치에서 두 개의 프로그램 세션을 실행하거나 동일한 LAN의 두 장치에서 프로그램을 실행해야 합니다.
- 컴퓨터 헤드셋과 마이크를 사용할 수 있습니다.
- GME 음성 채팅 서비스를 미리 신청하십시오.

### 1. 다운로드

클릭하여 [3D 음성 데모](https://picture-1256313114.cos.ap-beijing.myqcloud.com/GMEDemo.zip)를 다운로드하고 압축을 해제합니다.

### 2. Demo 열기

더블 클릭하여 **GMEDemo.exe** 파일을 엽니다. 동일한 장치에서 두 개의 Demo를 동시에 열 수 있습니다.

### 3. 초기화

데모를 초기화하려면 [Game Multimedia Engine 콘솔](https://console.cloud.tencent.com/gamegme/detail/1400391524)의 서비스 관리에서 찾을 수 있는 AppID와 키를 입력해야 합니다. GME 서비스 신청은 [Voice Service Activation Guide](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오. **appId는 콘솔의 AppID에 해당하고 authKey는 콘솔의 키에 해당합니다.**


<dx-alert infotype="explain" title="">
- AppID와 키가 유출되지 않도록 잘 보관하시기 바랍니다.
- 다른 데모 애플리케이션의 userId가 현재 userId와 다른지 확인하십시오.
</dx-alert>



<img src="https://main.qcloudimg.com/raw/f27ce333719f70f03447dcd97c5c9f3a.png"  width="80%"><br>
**초기화**>**음성 채팅**을 클릭하여 음성 채팅방 작성 페이지로 이동합니다.

### 4. 음성 채팅방 입장

이제 방 번호를 입력할 수 있습니다. 다른 데모를 열면 같은 방 번호를 입력하고 **JoinRoom**을 클릭하여 **같은 채팅방**으로 이동합니다.

<img src="https://main.qcloudimg.com/raw/8774bd52027febc15582e3d9f700eff8.jpg"  width="80%">

### 5. 게임 인터페이스

아래 인터페이스 세부 정보를 참고하십시오.
- 나가기: 음성 채팅방 선택 페이지로 돌아갑니다.
- 마이크 켜기/끄기: 마이크는 기본적으로 꺼져 있습니다. 통화를 하려면 켜십시오.
- 도움말: 도움말 인터페이스가 시작됩니다.
- 반주 켜기: 반주가 재생됩니다.
- 오른쪽 하단 모서리: 방에 입장 및 퇴장하는 사용자 로그입니다.
- 왼쪽 상단 모서리: 게임을 시작하기 위한 지역 정보를 구성합니다.
<img src="https://main.qcloudimg.com/raw/ae3f7726b2669c57466194a6e3e1e567.png"  width="80%"/></img>

### 6. 로컬 연결

**이 데모에는 로컬 LAN 연결 기반이 필요합니다**.
<img src="https://main.qcloudimg.com/raw/7779b1359844c1465d613586aab2c06d.png" width="80%" /></img>

- 첫 번째 방 구성원
먼저 방에 들어간 사람이 네트워크 연결의 Host로 채택됩니다. 따라서 첫 번째 구성원은 <b>LAN Host(H)</b>를 클릭해야 코인 옆에 구성원 아바타가 나타납니다.


- 다른 방 구성원
나중에 방에 들어온 사람들은 Host와 연결해야 합니다. 따라서 <b>LAN Client(C)</b>를 클릭하면 코인 옆에 아바타가 나타나며 첫 번째 구성원을 볼 수 있습니다.


### 7. 마이크 켜기

<img src="https://main.qcloudimg.com/raw/1fd9f4e3f35cfc166e04bd26fb520abf.png" width="3%"></img>을(를) 클릭하여 마이크를 켜면 방 구성원들과 대화할 수 있습니다.

### 8. 작업 방식

성공적으로 연결되면 다른 아바타를 볼 수 있습니다. "W", "S", "A", "D" 키를 눌러 아바타를 ‘전’, ‘후’, ‘좌’, ‘우’로 조작하고, 마우스를 움직여 시야각을 변경합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/23cd82f978016559de9c40a413dc23b9.png"  width="80%"/></img>

### 9. 경험

하나의 장치에서 데모의 두 세션을 여는 경우, 하나의 데모에서 아바타의 시각을 코인으로 이동합니다. 그런 다음 마이크를 켭니다. 다른 데모의 아바타를 조작하여 최대한 멀리 달려가면서 계속 말하여 3D 음성 효과를 테스트하십시오. 맵 가장자리로 달려가면 소리가 거의 들리지 않습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/01cfbded69436d29042ba1a14cc0e737.png"  width="80%"/></img>


## 고급 음성 변조 효과

GME 고급 음성 변조를 사용하면 게임 내 음성 채팅 중에 음성을 자유롭게 변형하고 다양한 음향 효과를 전달할 수 있습니다.

### 전제 조건
- 데모는 Windows 플랫폼에서 실행됩니다.
- 컴퓨터 헤드폰과 마이크를 사용할 수 있는지 확인하십시오.
- GME 음성 채팅 서비스를 미리 신청하십시오.

### 데모 열기

[고급 음성 변조 데모](https://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GMEDemoWithVoicemod_1.0.zip)를 다운로드하고 압축을 풀려면 클릭하십시오. 더블 클릭하여 **TMGSDK_For_Audio_ApiExample.exe** 파일을 열고 데모를 실행합니다.

### 실행 중인 인터페이스



### 1. AppID 및 Key 입력

데모를 초기화하려면 [Game Multimedia Engine 콘솔](https://console.intl.cloud.tencent.com/gamegme )의 서비스 관리에서 찾을 수 있는 AppID와 키를 입력해야 합니다. GME 서비스 신청은 [Voice Service Activation Guide](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오. **AppID는 콘솔의 AppID에 해당하고 Key는 콘솔의 키에 해당합니다.**


<dx-alert infotype="explain" title="">
- AppID와 키가 유출되지 않도록 잘 보관하시기 바랍니다.
- 다른 데모 애플리케이션의 userId가 현재 userId와 다른지 확인하십시오.
</dx-alert>

### 2. 초기화
**Init**를 클릭하여 초기화합니다.

### 3. 방 입장
**EnterRoom**을 클릭하여 방에 입장합니다.

### 4. 장치 활성화

**EnableMic**, **EnableSpeaker**, **EnableLoopback**을 클릭하여 장치 및 인이어 모니터링을 활성화합니다.

### 5. 경험

마이크에 대고 말하면서 음성 변화 효과를 경험하십시오.

구성 설명:
<img src="https://qcloudimg.tencent-cloud.cn/raw/97aa3d6feabc0d4e79fe4ac689271c6b.png"  width="80%"/></img>

### 6. 방 퇴장
테스트가 끝나면 **ExitRoom**을 클릭하여 방을 종료합니다. 그렇지 않으면 추가 요금이 발생할 수 있습니다.
