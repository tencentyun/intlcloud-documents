미니 응용프로그램 개발자가 Tencent Cloud GME API를 디버깅하고 연결하는 데 도움이 되도록 미니 응용프로그램 개발에 적합한 액세스 문서를 소개합니다.


## GME 서비스 신청

Tencent Cloud 콘솔에서 GME 관련 서비스를 신청하려면 [액세스 가이드](https://cloud.tencent.com/document/product/607/10782)를 참조하십시오.

## 미니 응용프로그램 라이브 방송 서비스 신청
### 1. Live 서비스 액세스
Tencent Cloud 콘솔에 로그인한 후, [Live]를 검색하여 [Live 신청 인터페이스](https://console.cloud.tencent.com/live)에 들어갑니다.

### 2. Live 서비스 신청
[동의] 버튼을 클릭하고 [개통 신청] 버튼을 클릭하여 Live를 활성화합니다.

![](https://main.qcloudimg.com/raw/3cc2238c29b077c8c9b50a5f62ce0df6.png)

> Live 서비스를 신청하기 전에 실명 인증을 진행해야 합니다. [계정 정보]에서 실명 인증하십시오.

### 3. 서비스 신청 성공
아래 그림이 나타날 경우 Live 서비스 신청에 성공했음을 의미합니다.

![](https://main.qcloudimg.com/raw/53d626f2dea1eaecf459636db1481e4b.png)

### 4. 재생 도메인 이름 신청
서비스를 신청 완료 후, 페이지 왼쪽 탐색 모음 중의 [도메인 이름 관리]를 클릭하여 도메인 이름 관리 인터페이스에 들어갑니다.
Live 서비스는 자동으로 한 개 푸시 도메인 이름을 생성합니다. [도메인 이름 추가] 버튼을 클릭하여 재생 도메인 이름을 신청하십시오.

![](https://main.qcloudimg.com/raw/d24740621f990a6101ee031de1a78cc4.png)
> 보유하고 ICP 라이센스가 있는 도메인 이름을 추가하여 라이브 방송 푸시 및 재생을 진행하십시오. 도메인 이름 관리 방법은 [도메인 이름 관리](https://cloud.tencent.com/document/product/267/30559)와 [CNAME 구성](https://cloud.tencent.com/document/product/267/30010)을 참조하십시오.


### 5. 재생 도메인 이름 신청 성공
재생 주소 신청이 성공한 후, 인터페이스에는 두 개의 도메인 이름이 존재하며, 하나는 푸시 도메인 이름이고 다른 하나는 재생 도메인 이름입니다.

![](https://main.qcloudimg.com/raw/df0850145ad53d12285e8e1b8f29cec5.png)


## rtmp 스트림 주소 생성
rtmp 스트림은 두가지 모드를 지원하며, 하나는 방 내의 말을 하는 어떤 멤버의 rtmp 스트림을 풀링하고 다른 하나는 방 내의 말을 하는 모든 멤버의 합성된 rtmp 스트림을 풀링합니다. 모드 1은 지정된 멤버의 음성만 들을 수 있고 모드 2는 모든 멤버의 음성을 들을 수 있습니다.

rtmp 스트림 주소 생성은 아래 몇가지 정보가 필요합니다.

|매개변수|의미|획득 방법|
|-----|-----|-----|
|AppID|GME 콘솔에서 신청한 AppID |Tencent Cloud 콘솔|
|RoomID|해당 사용자가 수신하려는 방 번호 ID |개발자가 응용프로그램에서 생성|
|UserID|해당 사용자가 수신하려는 다른 사용자의 ID |개발자가 응용프로그램에서 생성|
|BizID|Live 콘솔에서 생성한 식별 코드 |획득 방법은 아래 절차1 참조|
|StreamKey|Live 콘솔에서 생성한 키|획득 방법은 아래 절차1 참조|
|StreamID|rtmp 스트림의 유일한 ID|획득 방법은 아래 절차2 참조|
|Timestamp|타임스탬프(단위: 초) |개발자 생성 및 추가|


rtmp 스트림 주소의 생성은 아래 몇가지 절차를 포함합니다.
### 1. BizID 및 StreamKey 획득

- 도메인 이름 관리 인터페이스에 들어가고 재생 도메인 이름 메뉴에서 [관리] 버튼을 클릭하여 재생 도메인 이름 관리 인터페이스에 액세스합니다.

  ![](https://main.qcloudimg.com/raw/df0850145ad53d12285e8e1b8f29cec5.png)

- 인터페이스는 그림과 같습니다. CNAME 메뉴에서 "liveplay.myqcloud.com" 접미사 앞부분의 재생 도메인 이름은 BizID 매개변수입니다. 아래 그림 중의 BizID는 38521입니다.

- 인터페이스 중의 API Key는 StreamKey 매개변수입니다.

  ![](https://main.qcloudimg.com/raw/6a0a8c119acd2d49b575a40aa7ededcc.png)


### 2. StreamID 생성

모드 1:
```
{AppID}_{UserID}_{RoomID}_main
```
모드 2:
```
mixer_{AppID}_{RoomID}
```

### 3. 최종 주소 생성
```
rtmp://{BizID}.liveplay.myqcloud.com/live/MD5({StreamID})?txSecret= MD5({StreamKey}{streamidMd5}{timestamp})&txTime={timestamp}
```

> 그 중 MD5(): MD5를 계산하기 위한 함수

## 샘플 코드

예시 필요 정보:

```
Bizid:38251
streamKey:4531cddc5bd6dc28a812bb87121a5853
AppID:1400089356
RoomID:20180301
Userid:123456
timestamp:1551438840
```

rtmp 주소는 아래와 같습니다.

```
모드 1：
rtmp://38251.liveplay.myqcloud.com/live/38251_5a1d7c2f7e8fcb56942691035b49d960?txSecret=09fcc68fc320336c2b85071b11056bd6&txTime=5c7913f8

모드 2：
rtmp://38251.liveplay.myqcloud.com/live/38251_fed2b77fb622dcbf978ed6041d9f52d9?txSecret=2d69cfbd346da4531d82624a0bed9368&txTime=5c7913f8
```
