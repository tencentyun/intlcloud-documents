## 작업 시나리오
이 파일은 미니 응용프로그램 SDK API를 사용하여 개발자가 Tencent Cloud GME 제품 API를 디버깅하고 액세스하는것을 지원드립니다. 


## 전제조건
Tencent Cloud 백그라운드에서 GME 관련 서비스를 신청하였을 경우, 관련 상세내역은 [SDK 액세스 매뉴얼](https://intl.intl.cloud.tencent.com/document/product/607/10782)을 참조하십시오.


## 작업 프로세스
### LVB(Live Video Broadcasting) 서비스 신청
>LVB를 신청하기 전에 실명정보를 인증해야 합니다. [계정 메시지]에서 실명 인증을 신청하십시오.

1. Tencent Cloud 콘솔에 로그인하여 [LVB] 서비스를 선택하며, [LVB서비스 신청 인터페이스](https://console.cloud.tencent.com/live)에 접속합니다.
2. [<Tencent Cloud 서비스 약관>]을 체크하고, [오픈 신청]을 클릭하여 LVB서비스를 오픈합니다
3. [확인]을 클릭하면 LVB를 신청 완료합니다. 참고 이미지: 
4. 서비스를 신청 후, 좌측 메뉴바의 [도메인 네임 관리]를 클릭하여 도메인 네임 관리 인터페이스에 접속합니다.
5. LVB는 자동으로 푸시 도메인 네임을 생성합니다. [도메인 네임 추가]를 클릭하여 도메인 네임 플레이를 신청할 수 있습니다.
 >기존에 도메인 네임을 등록하여 라이브 방송을 푸시, 플레이합니다. 도메인 네임 관리, 사용방법은 [도메인 네임 관리](https://intl.cloud.tencent.com/document/product/267/31056)와 [CNAME설정](https://cloud.tencent.com/document/product/267/30010)을 참조하십시오. 

플레이 주소를 신청하면 인터페이스에 도메인 네임이 2개 나타납니다. 각 푸시 도메인 네임과 재생 도메인 네임입니다.


### rtmp 스트리밍 주소 생성
방 내 스피킹하는 전체 멤버의 rtmp 스트리밍을 읽어옵니다.

rtmp 스트리밍 주소를 생성하려면 다음 메시지가 필요합니다:

|파라미터|의미|획득방식|
|-----|-----|-----|
|AppID|GME 콘솔에서 신청한 AppID. |Tencent Cloud 콘솔, [SDK 액세스 매뉴얼](https://intl.intl.cloud.tencent.com/document/product/607/10782)을 참조하십시오.|
|RoomID|이 유저가 청취해야 할 방 ID.|이 파라미터는 개발자가 앱에서 생성합니다.|
|BizID|LVB 콘솔에서 생성한 표기 코드 |이 파라미터를 획득하는 방식은 하기[스텝1](#step1)을 참조하십시오.|
|StreamKey|LVB 콘솔에서 생성한 보안키|이 파라미터를 획득하는 방식은 하기 [스텝1](#step1)을 참조하십시오.|
|StreamID|rtmp 스트리밍의 유일한 표기|이 파라미터를 획득하는 방법은 하기 [스텝2](#step2)를 참조하십시오.|
|StreamIDMD5|StreamID Md5 처리|이 파라미터를 획득하는 방법은 하기 [스텝3](#step3)을 참조하십시오.|
|Timestamp|타임스탬프, 단위는 초 |이 파라미터는 개발자가 애플리케이션에서 생성하고 입력합니다.|


rtmp 스트리밍 주소 생성 프로세스: 
<span id="step1"></span>
#### BizID와 StreamKey 획득
1. 도메인 네임 관리 인터페이스에 접속하여 플레이 도메인 네임 칼럼의 [관리]를 클릭하여 플레이 도메인 네임 관리 인터페이스에 접속합니다.
2. CNAME 칼럼에서 “.liveplay.myqcloud.com”접미사 앞의 재생 도메인 네임은 BizID 파라미터입니다. 예를 들면 다음 이미지에서 BizID는 38251입니다. API Key는 StreamKey의 파라미터입니다.

<span id="step2"></span>
#### StreamID 생성

```
mixer_{AppID}_{RoomID}
```

<span id="step3"></span>
#### StreamIDMD5 생성 
```
{BizID}_{AppID}_{RoomID}_MD5({StreamID};
```

#### 최종 주소 생성
```
rtmp://{BizID}.liveplay.myqcloud.com/live/{StreamIDMD5}?txSecret= MD5({StreamKey}{StreamIDMD5}{timestamp})&txTime={timestamp}
```

>그중 MD5(); 는 MD5의 함수입니다.



예시에 필요한 정보: 

```
Bizid:38251
streamKey:4531cddc5bd6dc28a812bb87121a5853
AppID:1400089356
RoomID:20190301
timestamp:5c7913f8
```

rtmp 주소는 다음과 같습니다: 

```
rtmp://38251.liveplay.myqcloud.com/live/38251_1400089356_20190301_fed2b77fb622dcbf978ed6041d9f52d9?txSecret=95c396245d68aed1fa25b8dd79e81aa9&txTime=5c7913f8
```










