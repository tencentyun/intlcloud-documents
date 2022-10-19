도메인 푸시 스트리밍 완료 후, CSS 콘솔로 이동해 재생 주소 생성기를 이용하여 푸시 스트리밍 주소 StreamName과 동일한 StreamName을 입력하고 해당 스트림의 재생 주소를 생성하면, 해당 재생 주소를 통해 라이브 방송 화면을 확인할 수 있습니다.

## 전제 조건
 - [CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인되어 있어야 합니다.
 - **재생 도메인**이 추가되어 있어야 합니다. 자세한 내용은 [외부 도메인 추가](https://intl.cloud.tencent.com/document/product/267/35970)를 참고하십시오.

## 작업 단계
1. **[도메인 관리](https://console.cloud.tencent.com/live/domainmanage)**를 선택하여 설정할 재생 도메인 또는 **관리**를 클릭해 도메인 관리로 이동합니다.
2. **재생 설정** > **재생 주소 생성기**를 선택하여 다음과 같이 설정합니다.
	1. **원본 스트림 재생**, **트랜스코딩된 스트림 재생** 또는 **어댑티브 비트 레이트 스트림 재생**을 선택합니다. **트랜스코딩된 스트림 재생**을 선택한 경우 트랜스코딩 템플릿을 지정해야 합니다. **어댑티브 비트 레이트 스트림**을 선택하는 경우 어댑티브 비트 레이트 템플릿을 지정해야 합니다.
	2. 사용자 정의 스트림 이름 StreamName을 작성합니다(예시: liveteststream). 재생 주소 StreamName과 푸시 스트리밍 주소 StreamName이 일치해야 해당 스트림을 재생할 수 있습니다.
	3. 어댑티브 비트 레이트 템플릿을 선택하면 템플릿의 스트림 이름이 비트 레이트를 기준으로 내림차순으로 나열됩니다.
	4. 주소 유효 시간을 선택합니다. 예시: `2021-06-30 19:00:44`.
5. **주소 생성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ae67aa5386d9f47d7bd20d7cce7c7603.png)
3. 재생 도메인의 재생 인증이 비활성화 상태인 경우, **재생 설정** > **재생 주소 리졸브** 탭에서 해당 재생 도메인의 RTMP, FLV, HLS, UDP의 네 가지 재생 주소를 확인할 수 있습니다. 재생 주소 상의 StreamName(스트림 이름)을 변경하여 푸시 스트리밍 주소와 연결하면 재생 주소로 라이브 방송 화면을 확인할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/16a192a0090e8f4f470ace2b78cac52e.png)
>? CSS 재생에 관한 자세한 내용은 [라이브 방송 재생](https://intl.cloud.tencent.com/document/product/267/31559)을 참고하십시오.




## 재생 주소
### 재생 주소 생성 규칙
```
RTMP 형식: rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
FLV 형식: http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
M3U8 형식: http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
UDP 형식: webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
- domain: ICP비안을 완료한 외부 재생 도메인.
- AppName: 기본적으로 live이며 사용자 정의할 수 있는 라이브 스트리밍 애플리케이션 이름.
- StreamName: 스트림 이름으로, 사용자 정의가 가능하며 라이브 방송 스트림을 식별하는 데 사용됩니다.
- txSecret: 재생 인증을 활성화하면 생성되는 인증 문자열입니다.
- txTime: 재생 주소에 설정된 타임스탬프로, 콘솔 재생 주소의 유효 시간입니다.

>!
>- 도메인 인증을 활성화한 경우 실제 만료 시간은 txTime + 인증 유효시간입니다.
>- 콘솔에서는 사용 편의를 위해 설정 시간이 곧 실제 만료시간입니다. 도메인 인증을 활성화한 경우 재생 주소 연산 시 공식에 따라 txTime을 역산출합니다.
>- 만료 시간 전에 푸시 또는 재생을 시작하고 스트림이 중단되지 않는 한 URL이 만료된 후에도 푸시 또는 재생을 계속할 수 있습니다.

### 트랜스 코딩 후의 라이브 방송 주소
라이브 방송 도메인에 트랜스 코딩 템플릿을 설정하고 트랜스 코딩 후의 라이브 방송 스트림을 재생해야 하는 경우, 트랜스 코딩 재생 주소는 원본 재생 주소 상의 StreamName 뒤에 `_트랜스 코딩 템플릿 이름`을 추가하는 방식으로 조합됩니다.

예를 들어 원본 재생 주소가 `http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`이고 연결된 트랜스 코딩 템플릿 이름이 `hd`인 경우, 트랜스 코딩 재생 주소는 `http://domain/AppName/StreamName_hd.flv?txSecret=Md5(key+StreamName_hd+hex(time))&txTime=hex(time)`이 됩니다.

### 어댑티브 비트 레이트 재생 URL

어댑티브 비트 레이트 재생에는 HLS 및 WebRTC만 지원됩니다. 두 프로토콜의 URL 형식은 다릅니다.
HLS 어댑티브 비트 레이트 URL을 가져오려면 템플릿 이름(`_어댑티브 비트 레이트 템플릿 이름`)을 원본 재생 URL의 StreamName에 추가합니다.
예를 들어 원래 재생 URL이 `http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`이고 연결한 어댑티브 비트 레이트 템플릿 이름이 'autobitrate'인 경우 HLS 어댑티브 비트 레이트 URL은 `http://domain/AppName/StreamName_autobitrate.m3u8?txSecret=Md5(key+StreamName_hd+hex(time))&txTime=hex(time)`입니다.

WebRTC 어댑티브 비트 레이트 URL의 형식은 재생 도메인(domain)+AppName(기본적으로 live)+StreamName(스트림 ID)+인증 정보+어댑티브 비트 레이트 스트림 이름+처음 재생된 스트림의 이름 + 비트 레이트 제어 모드입니다. 어댑티브 스트림 이름은 비트 레이트에 따라 내림차순으로 나열됩니다.
어댑티브 비트 레이트 템플릿에 세 개의 스트림이 있다고 가정합니다. 이름은 test1, test2 및 test3이며 비트 레이트는 각각 200Kbps, 300Kbps 및 400Kbps입니다.
WebRTC 어댑티브 비트 레이트 URL은 `webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)&tabr_bitrates=test3,test2,test1&tabr_start_bitrate=test1&tabr_control=auto`입니다.




### H.265 재생 주소
CSS는 H.265 인코딩을 통한 푸시 스트리밍 및 재생을 지원합니다. 라이브 방송 원본 스트림이 H.264를 통해 인코딩된 경우, 라이브 방송 트랜스 코딩 템플릿을 통해 H.265 라이브 방송 스트림으로 전환하여 재생할 수 있습니다. 콘솔 트랜스 코딩 사용에 관한 내용은 [라이브 방송 콘솔 트랜스 코딩](https://intl.cloud.tencent.com/document/product/267/31561)을, API 트랜스 코딩에 관한 내용은 [라이브 방송 트랜스 코딩 API](https://intl.cloud.tencent.com/document/product/267/31561)를 참고하십시오.