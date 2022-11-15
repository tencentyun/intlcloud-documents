Tencent Cloud GME(Game Multimedia Engine)는 고품질을 특징으로 하는 원스톱 음성 솔루션으로 게임 산업의 응용 시나리오를 포괄적으로 다루고 있습니다. 멀티 플레이어 음성 채팅, 3D 음향 효과, 음성 메시지, 음성-텍스트 변환, 음성 콘텐츠 조정 등 다양한 기능을 지원합니다.
>!이 문서의 Demo는 Android 또는 iOS의 휴대폰에서만 실행할 수 있습니다.

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


## Demo 기능
Demo는 다음과 같은 기본 GME 기능을 보여줍니다.

<table>
   <tr>
      <th>기본 기능</th>
      <th>서브 기능</th>
   </tr>
   <tr>
      <td  rowspan="4">음성 채팅</td>
      <td>음질 옵션: 원활, 표준 및 HD 음질</td>
   </tr>
   <tr>
      <td>음성 채팅방</td>
   </tr>
	    <tr>
      <td>3D 음향 효과</td>
   </tr>
      <td>음성 채팅 시 음성 변경 효과(기본 음성 변조)</td>
   </tr>
      <td>음성 메시지</td>
			<td>버튼을 길게 눌러 음성 메시지 녹음 및 업로드, 탭하여 음성 메시지 재생</td>
   </tr>
      <td>음성-텍스트 변환 기능</td>
			<td>Demo에서 업로드된 음성 메시지는 자동으로 다양한 언어의 텍스트로 변환 가능</td>
   </tr>
</table>

<span id="test"></span>

## 로그인 페이지

### 1. 시스템에 로그인

UserId를 입력하고 **Login**을 누릅니다. 로그인하면 화면에 **Voice Chat** 및 **Voice Message**라는 두 개의 새로운 버튼이 표시됩니다.

<img src="https://main.qcloudimg.com/raw/dbacd4455622253ddb07d53e1bc785b8.png"  width="50%" /></img><br>

### 2. 기능 선택

- **Voice Chat**을 누르면 [실시간 음성 채팅](#test1)이 시작됩니다.
- **Voice Message**를 누르면 [음성 메시지](#test2)를 보낼 수 있습니다.

<span id="test1"></span>


## 음성 채팅 기능 체험

### 1. 음성 채팅방 입장 

 [로그인](#test) 후 **Voice Chat**을 눌러 음성 채팅 페이지로 이동합니다:

 <img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_KuI8ov.gif"    width="50%"/></img><br>

- **RoomId**: 방의 ID입니다. 같은 방 ID를 가진 사용자가 같은 방에 입장합니다.
- **RoomType**: 음질을 제어합니다.
  - Fluency: 부드러운 음질. 초저지연 실시간 음성 채팅 기능으로 FPS 및 MOBA와 같은 게임 내 파티플레이에 적합합니다.
  - Standard: 표준 음질. 음질도 좋고 딜레이도 적당하여 마피아 게임 및 보드 게임과 같은 캐주얼 게임의 음성 채팅에 적합합니다.
  - Hign Quality: 상대적으로 딜레이가 높은 HD 음질을 제공하며, 음악 재생과 같이 고음질을 요구하는 게임 시나리오에 적합합니다.

### 2. 음성 채팅 작업 수행

**JoinRoom**을 눌러 방에 입장합니다:

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_8zP4w2.gif"  width="50%"/><br>

- **Talking Members**: 방에서 말하고 있는 구성원을 지정합니다. 해당 구성원의 ID는 방 화면에 표시됩니다.
- **Mic**: 이 체크박스를 선택하면 마이크가 활성화됩니다. 
- **Speaker**: 이 체크박스를 선택하면 스피커가 활성화됩니다.
- **3D Voice Effect**: 이 체크박스를 선택하면 3D 음성 효과가 활성화됩니다. 이 경우 다음을 구성해야 합니다.
  - Range: 게임 엔진의 거리 단위를 사용하여 오디오를 수신 범위를 지정합니다.
  - X: 자체 X축.
  - Y: 자체 Y축.
  - Z: 자체 Z축.
  - XR: X축을 중심으로 회전하는 각도.
  - YR: Y축을 중심으로 회전하는 각도.
  - ZR: Z축을 중심으로 회전하는 각도.
- **Voice Change**: 다양한 실시간 음성 효과를 제공합니다. 자세한 내용은 [Real-time Sound Effect](https://intl.cloud.tencent.com/document/product/607/31503)를 참고하십시오.
- **QuitRoom**: 음성 대화방을 종료하고 이전 페이지로 돌아갑니다.

<span id="test2"></span>

## 음성 메시지 및 음성-텍스트 변환 기능 체험

### 1. 음성 메시지 페이지로 이동

[로그인](#test) 후 **Voice Message**를 눌러 음성 메시지 페이지로 이동합니다.

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_DsvaLv.gif"  width="50%"/></img><br>

### 2. 페이지에서 작업 수행

- **Language**: 녹음된 음성의 언어를 선택합니다. 녹음 후 음성은 지정된 언어의 텍스트로 변환되고 **Audio-to-Text** 에 표시됩니다.
- **Push To Talk**: **Push To Talk**를 길게 눌러 녹음을 시작하고 손을 떼면 녹음이 중지됩니다.
- **Audio**: 음성 메시지의 녹음 및 지속 시간입니다. <img src="https://main.qcloudimg.com/raw/7d268c4b1bb7e1998792b19a23e7bb63.png" width="3%"></img> 버튼을 눌러 녹음을 재생하고, 중지하려면 다시 클릭합니다.
- **Audio-to-Text**: 텍스트가 출력됩니다.

