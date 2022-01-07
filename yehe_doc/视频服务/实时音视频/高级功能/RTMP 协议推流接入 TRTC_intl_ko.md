
## 솔루션 배경
고객의 진입 장벽을 낮추기 위해, TRTC는 RTMP 표준 프로토콜 스트리밍을 지원하며, 실제 상황에 따라 [OBS](https://obsproject.com/download) 또는 FFmpeg를 선택하여 스트리밍할 수 있습니다. OBS는 사용자 사용이 용이한 무료 서드 파티 오픈 소스 프로그램 라이브 스트림 미디어 콘텐츠 제작 소프트웨어입니다. OS X, Windows, Linux 운영 체제를 지원하며, 다양한 라이브 방송 시나리오에 적합하고, 대부분의 라이브 방송 운영 요구 사항을 충족합니다. [OBS 공식 웹사이트](https://obsproject.com/download?spm=a2c4g.11186623.2.15.6aac1445JPlKR8)에서 최신 버전의 소프트웨어를 다운로드할 수 있으며, OBS를 사용하면 플러그 인을 설치할 필요가 없습니다.

이 기능은 현재 무료 베타 기간(과금 시 사전 공지 예정)이나, 연결된 RTMP 스트림은 회의실에서 버츄얼 사용자로 사용되어 일반 통화 요금이 발생합니다. 자세한 내용은 [과금 개요](https://intl.cloud.tencent.com/document/product/647/34610)를 참고하시기 바라며, 문의사항은 프리세일즈 팀(xunchenliu@tencent.com)에 연락하시기 바랍니다. 사용을 위해 얼로우리스트에 추가할 신청서를 제출하십시오(SdkAppId 필요).

>! TRTC에서 풀 스트림을 가져오는 RTMP를 지원하지 않습니다. CDN 라이브 방송 시청을 릴레이해야 하는 경우 [CDN 라이브 방송 시청 실행](https://intl.cloud.tencent.com/document/product/647/35242)을 참고하십시오.

## 응용 시나리오
<table>
<thead><tr><th width=22%>시나리오 유형</th><th>설명</th></tr></thead>
<tbody><tr>
<td>온라인 교육 시나리오</td>
<td>교사가 교육 자료 비디오를 보여줄 때, PC의 OBS 또는 FFmpeg를 통해 대다수의 미디어 형식을 RTMP로 TRTC 룸으로 푸시할 수 있습니다. 교실에 있는 학생들은 TRTC SDK로 풀 스트림하여 동시에 교육 비디오를 시청할 수 있으며, 교사가 비디오 자료 재생 중 건너뛰기, 속도 조정 및 다음 챕터 전환 등 제어를 진행할 수 있습니다. 높은 동시성으로 수업 질서와 품질의 안정성을 보장합니다.</td>
</tr><tr>
<td>스포츠 경기 관람 시나리오</td>
<td>스포츠 경기 스트림 미디어는 이벤트 공급자가 항상 RTMP 형식의 스트림으로 스포츠 경기 화면을 제공하고, RTMP 프로토콜을 통해 TRTC 룸으로 푸시하여, TRTC 룸에서 초저지연 경기 라이브 방송을 동시에 시청할 수 있도록 합니다. TRTC의 실시간 인터랙티브 기능으로 친구들과 음성/영상으로 대화하고, 함께 응원할 수 있어 모든 하이라이트 순간들을 공유할 수 있습니다.</td>
</tr><tr>
<td>더 많은 시나리오</td>
<td>모든 미디어 스트림 기반 실시간 인터랙션 시나리오는 RTMP 프로토콜 푸시 스트리밍을 통해 구현될 수 있습니다.</td>
</tr></tbody></table>


## OBS 푸시 스트림 설정
### 준비 작업[](id:ready)
[OBS](https://obsproject.com/download?spm=a2c4g.11186623.2.15.6aac1445JPlKR8) 툴을 설치하고 열어 다음 작업을 수행합니다.

### 입력 소스 선택[](id:step1)
하단 툴 바의 **소스** 태그를 확인하고, **+** 버튼을 클릭한 다음, 비즈니스 요구 사항에 따라 입력 소스를 선택합니다. 일반적으로 다음과 같습니다.

| 입력 소스         | 설명                                                         |
| :------------- | :----------------------------------------------------------- |
| 이미지           | 단일 영상 라이브 방송에 활용                                         |
| 이미지 슬라이드 쇼 | 복합 이미지를 순환 혹은 순차적으로 재생                                 |
| 시나리오           | 각종 라이브 방송 효과 구현. 또 다른 시나리오는 소스 형태로 현재 시나리오에 추가하여 전체 시나리오 삽입 구현 가능 |
| 미디어 소스         | 로컬 비디오 업로드 및 로컬 VOD 비디오 파일 스트리밍화 처리           |
| 텍스트           | 라이브 방송 창에 실시간 텍스트 추가                                   |
| 창 캡처       | 선택한 창 실시간 캡처. 라이브 방송 중에 다른 창은 캡처하지 않으며 현재 창만 표시 |
| 비디오 캡처 디바이스   | 촬영 디바이스를 실시간 동적 캡처하여 촬영 후 화면을 라이브로 방송             |
| 오디오 입력 캡처   | 음성 라이브 방송 이벤트에 사용(음성 입력 디바이스)                           |
| 오디오 출력 캡처   | 음성 라이브 방송 이벤트에 사용(음성 출력 디바이스)                           |


![](https://qcloudimg.tencent-cloud.cn/raw/cd227431216391302e50a3ed4e794de2.png)


### 푸시 스트림 매개변수 설정[](id:step2)
1. 하단 툴 바의 **컨트롤러>설정** 버튼을 눌러 설정 인터페이스로 이동합니다.
![img](https://qcloudimg.tencent-cloud.cn/raw/26404eda70b80a654f3119683ae3ca46.png)
2. **푸시 스트림**을 클릭하여 푸시 스트림 설정 탭으로 이동하고 서비스 유형을 **사용자 정의**로 선택합니다.
3. 서버 입력: `rtmp://rtmp.rtc.qq.com/push/`.
4. 스트림 키 형식:
```
방 번호?sdkappid=애플리케이션&userid=사용자 이름&usersig=서명
```
방 번호, 애플리케이션, 사용자 이름 및 서명을 비즈니스로 전환하는 예시:
```
22998?sdkappid=140*****66&userid=******rtmp2&usersig=eJw1jdE***************ZLgi5UAgOzoMhrayt*cjbmiCJ699T09juc833IMT94Ld7I0iHZqVDzvVAqkZsG-IKlzLiXOnEhswHu1iUyTc9pv*****D8MQwoA496Ke6U1ip4EAH4UMc5H9pSmv6MeTBWLamhwFnWRBZ8qKGRj8Yp-wVbv*mGMVZqS7w-mMDQL
```
	- 매개변수를 단순화하기 위해 문자열 방 번호만 지원하며 64자 이하의 숫자, 알파벳, 언더바만 사용 가능합니다. TRTC의 기타 다른 엔드로 RTMP 스트림을 시청하려면 **문자열 방 번호를 사용하여 방에 입장합니다**.
	- usersig 생성 규칙은 [UserSig 관련 질문](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오(**유효기간 이내의 서명이어야 함**).
	- 상기 서버 주소 + 스트림 키로 RTMP 스트림 주소를 구성하며 FFmpeg 또는 기타 RTMP 라이브러리 푸시 스트림에도 사용할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c3b309db1312f19abb3ca147c1ecea32.png)

### 출력 설정[](id:step3)
RTMP 백엔드는 B-프레임 전송을 지원하지 않으며, 사용자는 다음 설정을 통해 푸시 스트림 소프트웨어의 비디오 인코딩 매개변수를 조정하여 B-프레임을 제거할 수 있습니다.
1. **설정**에서 **출력** 탭을 클릭하여 설정합니다.
2. **출력 모드**에서 **고급**을 선택하고, **키 프레임 간격을 1 또는 2로 입력하는 것이 좋습니다.** **확인**을 클릭하여 설정을 저장합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/072b2fbaf9a3bf6674a48943223de22c.png)  


### 비디오 옵션 설정[](id:step4)
**설정**의 **비디오** 탭을 클릭하여 해상도와 프레임 레이트를 설정합니다. 해상도는 시청자가 보는 화질을 결정합니다. 해상도가 높을수록 화면이 선명합니다. FPS는 비디오 프레임 레이트를 뜻하며 비디오의 재생 품질과 관련됩니다. 보통 비디오 프레임 레이트는 24 ~ 30프레임이며 16프레임 이하 화면은 딜레이되는 듯한 느낌을 줍니다. 그래서 비교적 높은 프레임 레이트를 요구하는 게임의 경우 30프레임 이하로 내려가면 일반적으로 자연스럽지 못한 느낌을 줍니다.
![](https://qcloudimg.tencent-cloud.cn/raw/81e9e716bf76a8a1a20a1badcf7dfcd9.png)


### 고급 옵션[](id:step5)
- 엔드 투 엔드 딜레이를 줄이기 위해 **스트림 딜레이**를 활성화하지 않는 것이 좋습니다.
- **자동 재연결**을 활성화하고 **재시도 딜레이**를 최대한 짧게 설정하면, 네트워크 지터 발생 시 연결이 끊어지면 최대한 빨리 재연결됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7a25a1cb3e2a6daf07508bcb2fdabeb6.png)


### 푸시 스트림 클릭[](id:step6)
1. OBS 하단 툴 바에서 **컨트롤러**를 조회하고 **푸시 스트림 시작**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8709c618536109bfb02e860b47581e45.png)
2. 푸시 스트림 성공 후, 일반적으로 푸시 스트림 상태가 인터페이스 하단에 표시되고, 사용자의 방 입장 기록은 TRTC 콘솔 대시보드에 기록됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/15c0d1b5df33c4a738050f1f532a990c.png)

### 다른 엔드 보기[](id:step7)
[푸시 스트림 매개변수 설정](#step2)에서 언급한 바와 같이, TRTC의 다른 엔드는 문자열 방 번호를 사용하여 방에 입장해야 합니다. Web에서의 RTMP 스트림 시청 효과는 다음과 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/787178aa5dc550a592f5455d9f2ffb8e.png)

## FFmpeg 설정[](id:FFmpeg)
명령 라인 또는 기타 RTMP 라이브러리를 사용하여 스트림을 푸시하려면 [푸시 스트림 매개변수 설정](#step2)에서 서버 주소 + 스트림 키를 참조하여 표준 RTMP 푸시 스트림 주소를 구성합니다. FFmpeg 또는 기타 RTMP 라이브러리에서 푸시 스트림에 사용할 수 있습니다. 비디오 인코딩은 H.264를, 오디오 인코딩은 AAC를, 컨테이너 형식은 FLV를 사용합니다. GOP를 2초 또는 1초로 설정하는 것이 좋습니다.
FFmpeg 명령 설정 매개변수는 시나리오마다 다르므로 특정 FFmpeg 사용 경험이 필요합니다. 다음은 FFmpeg 일반적으로 사용되는 명령 라인 옵션 입니다. 더 많은 FFmpeg 옵션은 [FFmpeg 공식 웹사이트](https://ffmpeg.org/ffmpeg.html)를 참고하십시오.

### FFmpeg 명령 라인[](id:order)
```
ffmpeg [global_options] {[input_file_options] -i input_url} ... {[output_file_options] output_url} 
```

### 일반적인 FFmpeg 옵션[](id:set)
<table>
<thead><tr><th>옵션</th><th>설명</th></tr></thead>
<tbody><tr>
<td>-re</td><td>native 프레임 레이트로 입력 읽기, 일반적으로 로컬 파일 읽기에만 사용됨</td>
</tr></tr></tbody></table>

**output_file_options** 설정 가능한 옵션은 다음과 같습니다.

<table>
<thead><tr><th>옵션</th><th>설명</th></tr></thead>
<tbody><tr>
<td> -c:v</td><td>비디오 인코딩, <code>libx264</code>사용 권장</td>
</tr><tr>
<td>-b:v</td><td>비디오 비트 레이트. 예: 1500k는 1500kbps를 나타냄</td>
</tr><tr>
<td>-r</td><td>비디오 프레임 레이트</td>
</tr><tr>
<td>-profile:v</td><td>비디오 profile. baseline을 지정하면 B-프레임을 인코딩하지 않음, TRTC 백엔드는 B-프레임 미지원</td>
</tr><tr>
<td>-g</td><td>GOP 프레임 간격</td>
</tr><tr>
<td>-c:a</td><td>오디오 인코딩. <code>libfdk_aac</code>사용 권장</td>
</tr><tr>
<td>-ac</td><td>사운드 채널 수, 2 또는 1 입력</td>
</tr><tr>
<td>-b:a</td><td>오디오 비트 레이트</td>
</tr><tr>
<td>-f</td><td>형식을 지정하고 <code>flv</code>를 입력한 후, TRTC로 전송하여 FLV 컨테이너 캡슐화 사용</td>
</tr></tbody></table>
다음은 파일 읽기를 통해 TRTC에 푸시하는 예시입니다.

```
ffmpeg -loglevel info -re -i sample.flv -c:v libx264 -preset fast -profile:v baseline -g 30 -sc_threshold 0 -b:v 1500k -c:a libfdk_aac -ac 2 -b:a 128k -f flv 'rtmp://rtmp.rtc.qq.com/push/hello-string-room?userid=rtmpForFfmpeg&sdkappid=140xxxxxx&usersig=xxxxxxxxxx'
```

### Web 시청 효과[](id:view)
![](https://qcloudimg.tencent-cloud.cn/raw/3ba672af6154d1998b4e5ede78296d9d.png)


