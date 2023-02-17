Tencent Cloud GME(Game Multimedia Engine) 고품질 원스톱 음성 솔루션으로 게임 산업의 응용 시나리오를 포괄적으로 커버합니다. 멀티 플레이어 음성 채팅, 3D 음향 효과, 음성 메시지, 음성-텍스트 변환, 음성 콘텐츠 조정 등 다양한 기능을 지원합니다.
이 Demo는 간단한 게임 시나리오를 시뮬레이션하고 음성 채팅, 3D 음성, 범위 음성 및 음성 변조를 포함한 GME의 기능을 보여줍니다.


## 작업 단계
### 1단계: Demo 다운로드
<table>
 <tr>
    <th style="text-align:center;" width="150px"><b>Android, iOS<br></b>카메라로 QR코드 스캔</th>
    <th style="text-align:center;" width="150px"><b>Windows<br></b></th>
 </tr>
 <tr>
    <td style="text-align: center;">
		<img style="width:150px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/5b7f6119b87b2f2aadd3f123c94b6284.png" class="zoom-img-hover">
	 </td>
   <td style="text-align: center;">
	 <a href="https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/GmeDemo_x86_64_1.0.0.zip">다운로드</a>    
	 </td>
  </tr>
</table>


### 2단계: Demo 설치

다운로드한 패키지의 압축을 풀고 **GMEDemo**라는 소프트웨어를 엽니다.


### 3단계: 음성 채팅방 입장
Demo를 연 후, 음성 채팅방 선택 화면으로 들어갑니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/50d395ffc49b18aaece3537240c6b12e.png"  width="60%">

- UserID : Demo에서 자동으로 생성되며 필요에 따라 설정할 수 있습니다. 고유해야 하며 중복될 수 없습니다.
- RoomType: 방의 음질을 선택합니다. 동일한 RoomType 옵션을 선택한 플레이어는 동일한 방에 입장합니다.
	- Smooth sound quality: 부드러운 음질.
	- Standard sound quality: 표준 음질
	- High sound quality: 높은 음질
- Background music: 음성 채팅방에서 배경음악을 틀고 싶을 때 선택합니다.
- **JoinRoom**을 클릭하여 음성 채팅방으로 들어갑니다.



### 4단계: 게임의 메인 UI
음성 채팅방에 입장하면 게임의 메인 UI를 볼 수 있습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/28deb2e315826fa13660698bf2b20a83.png"  width="60%"/></img>

아래 인터페이스 세부 정보를 참고하십시오.
- 뒤로가기 버튼: 왼쪽 상단의 화살표를 클릭하면 음성 채팅방 선택 화면으로 돌아갑니다.
- 마이크 버튼: 기본적으로 방에 입장하면 마이크가 꺼져 있습니다. 방에서 말하려면 마이크를 켜야 합니다.
- 스피커 버튼 : 방에 입장하면 기본적으로 스피커는 꺼집니다. 방에 있는 다른 구성원의 소리를 들으려면 스피커를 켜야 합니다.
- 설정 버튼: 버튼을 클릭하여 언어를 설정하고, 3D 음성, 범위 음성, 음성 변경 기능을 활성화 또는 비활성화합니다.
- 도움말 버튼: 버튼을 클릭하면 게임 가이드를 읽을 수 있습니다.
- 인터페이스 좌측 하단: 캐릭터의 움직임을 제어하는데 사용되는 가상 조이스틱입니다.
- 인터페이스 우측 하단 : 음성 채팅방에 입장하고 퇴장한 사용자를 보여주는 방 로그 정보입니다.

<dx-alert infotype="explain" title="다음의 경우 게임 연결에 성공한 것입니다:">
  1. 게임 UI에서 상대방의 게임 캐릭터를 볼 수 있습니다.
  2. UI 우측 하단의 로그는 상대방 게임 캐릭터의 방 입장 기록을 userID로 표시합니다.
</dx-alert>


### 5단계: 게임 설정 페이지
설정 버튼을 클릭하여 게임 설정 페이지로 이동합니다.


- **언어**: 중국어 또는 영어를 선택합니다.
- **3D 음향**: 3D 음향 효과를 활성화하면 말하는 캐릭터의 움직임에 따라 스테레오 사운드 효과와 볼륨 변화를 경험할 수 있습니다. 자세한 내용은 [3D 음향 효과](https://intl.cloud.tencent.com/document/product/607/18218)를 참고하십시오.
- **범위 음성**: 이 기능을 활성화하면 캐릭터 주위에 서클이 표시됩니다. 캐릭터가 이 서클 안에 있는 플레이어와만 통신할 수 있습니다. 이 기능을 비활성화하면 통신이 범위에 영향을 받지 않습니다. 자세한 내용은 [Range Voice](https://intl.cloud.tencent.com/document/product/607/17972)를 참고하십시오.
- **음성 변조**: 이 기능을 활성화하면 선택한 음색으로 음성을 변조할 수 있습니다. 자세한 내용은 [음성 변조](https://intl.cloud.tencent.com/document/product/607/44995)를 참고하십시오.
- **템플릿**: 드롭다운 목록에서 원하는 음성 변조 템플릿을 선택할 수 있습니다.


### 6단계: 작업 방식

1. 방에 있는 다른 플레이어와 대화하려면 해당 버튼을 클릭하여 마이크와 스피커를 켤 수 있습니다.
2. 설정 페이지로 이동하여 다음 기능을 활성화 또는 비활성화할 수 있습니다: 3D 음성, 범위 음성, 음성 변조.
3. 모바일 장치에서는 가상 조이스틱을 사용하여 캐릭터의 움직임을 제어하고 화면에서 손가락을 움직여 보기를 조정할 수 있습니다. Windows PC에서는 "W", "S", "A", "D" 키를 눌러 각각 ‘앞’, ‘뒤’, ‘왼쪽’, ‘오른쪽’으로 이동할 수 있으며 마우스를 움직여 보기를 조정할 수 있습니다.
4. 게임에 플레이어 A와 플레이어 B라는 두 명의 플레이어가 있다고 가정합니다. 플레이어 A는 이 과정에서 플레이어 B가 플레이어 A 주위를 움직이며 말을 계속할 때 3D 음성 효과를 경험할 수 있습니다. 플레이어 B가 3D 음성 효과에 설정된 범위를 벗어난 위치로 이동하면 플레이어 A는 플레이어 B의 소리를 거의 들을 수 없습니다.
