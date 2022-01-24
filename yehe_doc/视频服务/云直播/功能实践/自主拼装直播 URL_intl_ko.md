### 전제 조건
- Tencent Cloud 계정에 가입되어 있어야 하며 [CSS 서비스](https://intl.cloud.tencent.com/product/css)가 활성화된 상태여야 합니다.
- 외부 도메인이 있어야 합니다.
- [CSS 콘솔]>[도메인 관리](https://console.cloud.tencent.com/live/domainmanage)에서 푸시 스트림/재생 도메인을 추가하고 CNAME 작업을 완료한 상태여야 하며, 자세한 방법은 [외부 도메인 추가](https://intl.cloud.tencent.com/document/product/267/35970)를 참조하십시오.

<span id="push"></span>
### 푸시 스트림 URL 연동
실제 제품에 라이브 룸이 비교적 많을 경우 모든 호스트에게 수동으로 푸시 스트림 및 재생 URL을 생성해줄 수 없습니다. 서버를 통해 푸시 스트림 및 재생 주소를 **자동 연동**할 수 있으며, Tencent Cloud 표준 규범에 부합하는 URL이라면 푸시 스트림에 사용할 수 있습니다. 표준 푸시 스트림 URL은 다음과 같으며, 네 부분으로 구성되어 있습니다.
![](https://main.qcloudimg.com/raw/679602c838e8dfd3b61acefebb221d13.jpg)

- **Domain**
푸시 스트림 도메인으로, Tencent CSS를 이용해 제공하는 기본 푸시 스트림 도메인입니다. 외부 도메인에 CNAME을 설정한 푸시 스트림 도메인을 사용할 수도 있습니다.
- **AppName**
라이브 방송 애플리케이션 이름으로, 기본값은 live이며 사용자 정의할 수 있습니다.
- **StreamName(스트림 ID)**
사용자 정의된 스트림 이름으로, 모든 라이브 방송 스트림의 유일한 식별자입니다. 랜덤 숫자 또는 숫자와 영문 알파벳을 조합하여 사용하시기 바랍니다.
- **인증 Key(필수 아님)**
txSecret와 txTime 두 부분 포함: `txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
푸시 스트림 인증 활성화 후에는 인증 Key를 포함한 URL을 사용해 푸시 스트림을 진행해야 합니다. 푸시 스트림 인증을 활성화하지 않은 경우 푸시 스트림 주소에 "?" 와 같은 문자는 필요하지 않습니다.
 - **txTime(주소 유효 시간)** 
해당 URL의 만료 시간을 표시하며, 16진법 UNIX 타임스탬프 포맷을 지원합니다.
	
	>?예를 들어 `5867D600`는 2017년 1월 1일 0시 0분 0초 만료를 의미합니다. 일반적으로 txTime는 24시간 이후 만료로 설정하며, 만료 시간을 너무 짧거나 길게 설정하지 마십시오. 호스트가 라이브 방송 중 네트워크가 몇 초간 끊기는 상황이 발생하는 경우 다시 푸시 스트림이 복구되는데, 이때 만료 시간이 너무 짧으면 푸시 스트림 URL 만료로 인해 호스트가 다시 푸시 스트림을 복구할 수 없게 됩니다.
 - **txSecret(링크 도용 방지 서명)**
해커가 사용자의 백그라운드를 위조하여 푸시 스트림 URL을 생성하는 것을 방지하며, 계산 방법은 [모범 사례-링크 도용 방지 계산](https://intl.cloud.tencent.com/document/product/267/31560)을 참조하십시오.

<span id="play"></span>
### 재생 URL 연동
재생 주소는 주요하게 재생 접두사, 재생 도메인(domain), 애플리케이션 이름(AppName), 스트림 이름(StreamName), 재생 프로토콜 확장자명, 인증 매개변수, 기타 사용자 정의 매개변수로 구성됩니다. 예시는 다음과 같습니다.	

```	
webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```

- **재생 접두사**	
<table>
    <tr><th>재생 프로토콜</th><th>재생 접두사</th><th>비고</th></tr>
    <tr>
        <td>RTMP</td>
        <td><code>rtmp://</code> </td>
        <td>권장하지 않습니다. 바로 재생 효과가 떨어지며 다수의 동시 접속을 지원하지 않습니다.</td>
    </tr><tr>
        <td>HTTP-FLV </td>
				<td><code>http://</code> 또는 <code>https://</code> </td>
        <td>권장합니다. 바로 재생 효과가 적용되며 다수의 동시 접속을 지원합니다.</td>
    </tr><tr>
        <td>HLS(m3u8)</td>
        <td><code>http://</code> 또는 <code>https://</code> </td>
        <td>모바일 및 Mac safari 브라우저에서 권장되는 재생 프로토콜입니다.</td>
    </tr>
</table>
- **Domain**	
	재생 도메인으로, 외부 도메인에 CNAME을 설정한 재생 도메인입니다.
- **AppName**	
  라이브 방송 애플리케이션 이름으로, 라이브 방송 스트림 미디어 파일의 저장 경로를 구분하는 데 사용합니다. 기본값은 live이고, 사용자 정의 가능합니다.
- **StreamName(스트림 이름)<span id="streamname"></span>**	
  사용자 정의된 스트림 이름으로, 모든 라이브 방송 스트림의 유일한 식별자입니다. 랜덤 숫자 또는 숫자와 영문 알파벳을 조합하여 사용하시기 바랍니다.
- **인증 매개변수(필수 아님)**	
	txSecret와 txTime 두 부분 포함: `txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
재생 인증 활성화 후에는 인증 Key를 포함한 URL을 사용해 재생해야 합니다. 재생 인증을 활성화하지 않은 경우 재생 주소에 "?" 및 이후 문자는 필요하지 않습니다.
 - **txTime(주소 유효 시간):** 해당 URL의 만료 시간을 표시하며, 16진법 UNIX 타임스탬프 포맷을 지원합니다.
 - **txSecret(링크 도용 방지 서명):** 해커가 사용자의 백그라운드를 위조하여 재생 URL을 생성하는 것을 방지하며, 계산 방법은 [모범 사례-링크 도용 방지 계산](https://intl.cloud.tencent.com/document/product/267/31560)을 참조하십시오.


<span id="push_code"></span>
### 푸시 스트림 예시 코드 확인
[CSS 콘솔]>[도메인 관리](https://console.cloud.tencent.com/live/domainmanage)에서 이벤트 설정의 푸시 스트림 도메인을 선택한 후, [관리]>[푸시 스트림 설정] 페이지 아래쪽에 [푸시 스트림 주소 예시 코드](PHP 및 Java 두 버전)가 있습니다. 링크 도용 방지 주소를 생성하는 방법을 보여줍니다. 자세한 작업 방법은 [푸시 스트림 설정](https://intl.cloud.tencent.com/document/product/267/31059)을 참조하십시오.

