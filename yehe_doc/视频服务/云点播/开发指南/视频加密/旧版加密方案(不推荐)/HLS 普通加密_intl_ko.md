
VOD는 비디오 업계의 저작권 보호 요구 사항에 따라 HLS의 공통 AES 암호화 기술을 사용하여 저작권 보호를 위해 비디오 콘텐츠를 암호화하는 기본 DRM(디지털 저작권 관리) 솔루션을 제안합니다. [VOD 파일 암호화 DEMO](http://demo.vod.qcloud.com/encryption/index.html)에서 DRM 솔루션에 대해 자세히 알아볼 수 있습니다(사용자 이름: test, 비밀번호: 111111).

##  HLS의 일반 암호화 방식

#### 암호화 알고리즘
VOD 시스템은 현재 AES-128을 사용하여 비디오 콘텐츠를 암호화하는 [HLS](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23)에 정의된 암호화 방식(HLS의 일반적인 AES 암호화 기술)을 지원합니다.

#### 플레이어 적응성
VOD의 영상 암호화 솔루션은 모든 HLS 플레이어를 지원합니다.

#### 제한성

- 2017 버전의 API만 지원됩니다. [ProcessFile](https://intl.cloud.tencent.com/document/product/266/34125)을 사용하여 암호화 작업을 시작하고 [GetTaskInfo](https://intl.cloud.tencent.com/document/product/266/34129)를 사용하여 암호화 결과를 쿼리할 수 있습니다.
- 새 버전의 [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) 및 [DescribeTaskDetail](https://intl.cloud.tencent.com/document/product/266/34129) API는 HLS 일반 암호화를 지원하지 않습니다.

### 용어

#### Key Management Service(KMS)
Tencent Cloud KMS는 데이터 키 생성, 암호화 및 복호화를 위한 보안 관리 서비스입니다. 자세한 내용은 [KMS](https://intl.cloud.tencent.com/product/kms)를 참고하십시오.

#### Data Key(DK)
DK는 대칭 암호화 및 암호 복호화을 위해 KMS에서 생성한 키입니다.

#### Encrypted Data Key(EDK)
EDK는 KMS로 암호화된 DK로, 공개적으로 배포할 수 있습니다. DK를 EDK로 교환하려면 KMS의 복호화 API를 호출해야 합니다.

### 전체 아키텍처
![](https://main.qcloudimg.com/raw/53a2bbfe7d920e636c57574d266dc4ec.png)
비디오 암호화 프로세스는 새로운 fileId를 생성하지 않는 트랜스코딩을 통해 구현됩니다. 일반 트랜스코딩 시나리오와 비교할 때 비디오 암호화 트랜스코딩에는 다음과 같은 차이점이 있습니다.
- 암호화는 트랜스코딩 중에 수행됩니다. 즉, 출력 비디오가 암호화됩니다.
- 암호화된 트랜스코딩이 완료된 후 VOD 플레이어를 통해 비디오를 재생하면 소스 파일의 재생 URL을 얻을 수 없습니다.

### 준비 과정

#### KMS 구축
KMS는 주로 비디오 키를 관리하는 데 사용됩니다. 비디오 암호화 프로세스의 다음 단계는 KMS 시스템과 상호 작용해야 합니다.

1. 상기 아키텍처 다이어그램과 같이 비디오 암호화를 위한 DK를 생성하는 II단계. 이 단계에서 DK 및 EDK가 반환됩니다. 후속 단계에서 VOD 트랜스코딩 서비스, 애플리케이션 백엔드 및 인증된 최종 사용자가 DK에 액세스할 수 있으며 EDK는 모든 최종 사용자에게 배포될 수 있습니다. 그러나 EDK를 통해 DK를 얻으려면 App 백엔드에서 인증을 수행해야 합니다.
2. 상기 아키텍처 다이어그램과 같이 비디오 재생을 위해 EDK를 통해 DK를 가져오는 4단계. App에서 최종 사용자를 인증한 후 5단계에 설명된 대로 EDK를 통해 DK를 가져오려면 KMS의 API를 호출해야 합니다.

통합 비용을 최소화하기 위해 KMS는 VOD에 내부에 통합되었으며, 가장 간단한 호출 API를 제공합니다. 전체 비디오 암호화 솔루션에서 App 백엔드가 KMS 서비스와 상호 작용해야 하는 유일한 위치는 복호화 키 가져오기입니다(아키텍처 다이어그램의 5단계).

#### 인증 및 키 배포 서비스 구축

암호화된 비디오의 경우 App 백엔드에서 인증한 클라이언트만 DK를 가져올 수 있습니다. 따라서 최종 사용자가 키를 얻으려고 할 때 App 백엔드에서 인증을 수행해야 합니다. 이 서비스의 비즈니스 로직은 다음과 같습니다.
1. 클라이언트가 EDK를 사용하여 DK를 가져오도록 요청하는 경우(아키텍처 다이어그램의 4단계) 요청자에게 실명 인증을 진행합니다.
2. 인증이 통과되면 KMS 시스템에서 DK(아키텍처 다이어그램의 5단계)를 가져와 클라이언트로 반환합니다.

#### 제안
- DK는 항상 특정 EDK에 해당하므로 KMS 호출 횟수(즉, 아키텍처 다이어그램의 5단계)를 줄이기 위해 App 백엔드에서 이들 간의 통신을 캐시(또는 영구적으로 저장)할 수 있습니다.
- HTTP 캐시 제어 매개변수(예: Cache-Control)를 App 백엔드에서 클라이언트에 반환된 응답에 추가하여 클라이언트가 App 백엔드에서 DK를 가져오는 작업 건수(즉, 아키텍처 다이어그램의 4단계)를 줄일 수 있습니다. 
- 브라우저에서 재생을 지원해야 하는 경우 도메인 간 문제를 방지하기 위해 ‘인증 및 키 배포 서비스’에 사용된 도메인 이름이 ‘비디오 재생 페이지’에 사용된 도메인 이름과 동일해야 합니다(예를 들어 비디오 재생 페이지의 도메인 이름이 `v.myvideo.com`인 경우 키 배포 서비스의 도메인 이름도 `v.myvideo.com`이어야 합니다).

#### 비디오 암호화 템플릿 구성
VOD 백엔드가 암호화 작업을 올바르게 수행할 수 있도록 비디오 암호화 템플릿을 구성해야 합니다. 자세한 내용은 [HLS 일반 암호화 템플릿](https://intl.cloud.tencent.com/document/product/266/33969)을 참고하십시오.

### 비즈니스 프로세스

#### 비디오 업로드
기존 영상 파일을 서버, 클라이언트, 콘솔, 레코딩, URL 등의 방식으로 VOD 플랫폼에 업로드할 수 있습니다.

#### 비디오 암호화

비디오 암호화의 주요 단계는 다음과 같습니다.

#### 1. App 백엔드가 비디오 암호화를 시작합니다.

현재 [ProcessFile](https://intl.cloud.tencent.com/document/product/266/34125) API를 사용하여 비디오 암호화를 시작할 수 있습니다. HLS 파일만 암호화할 수 있습니다.

예시의 의미는 다음과 같습니다.

- 비디오 파일을 트랜스코딩합니다. 트랜스코딩의 대상 출력 템플릿은 210, 220, 230, 240이며 낮은 비트레이트에서 높은 비트레이트로의 트랜스코딩은 금지됩니다.
- 트랜스코딩 프로세스는 암호화 템플릿 10을 사용하여 암호화됩니다.
- 이벤트 알림 모드: 전체 이벤트가 완료된 후 이벤트 알림이 전송됩니다.

<pre>
https://vod.api.qcloud.com/v2/index.php?Action=ProcessFile
&transcode.definition.0=210
&transcode.definition.1=220
&transcode.definition.3=230
&transcode.definition.4=240
&transcode.drm.definition=10
&amp;notifyMode=Finish
&COMMON_PARAMS
</pre>

#### 2. VOD 플랫폼이 암호화 키를 가져옵니다.
VOD 플랫폼은 호출자가 지정한 암호화 매개변수 템플릿을 기반으로 키 획득 방법을 읽습니다. 최종 사용자는 복호화 키의 URL(예: `https://getkey.example.com`)을 얻은 다음 KMS 시스템에서 비디오 암호화 키 (DK 및 EDK)를 가져옵니다.

#### 3. VOD 플랫폼이 암호화된 비디오 트랜스코딩을 시작합니다.

VOD의 트랜스코딩 플랫폼은 비디오 암호화를 수행할 때 지정된 암호화 알고리즘과 키를 사용하여 대상 출력 파일을 암호화할 뿐만 아니라 복호화 키를 얻기 위한 URL을 비디오 파일에 기록합니다. 예를 들어 HLS의 경우 URL은 M3U8 파일의 `EXT-X-KEY` 태그에 기록됩니다. 그러나 작성하기 전에 트랜스코딩 플랫폼은 이 URL의 QueryString에 다음 세 가지 매개변수를 추가합니다.

- fileId: 암호화된 파일의 ID.
2. keySource: 이 매개변수의 값은 항상 VodBuildInKMS이며, 이는 Tencent Cloud VOD 내장 KMS를 의미합니다.
3. edk: DK에 해당하는 EDK.

상기 매개변수를 추가한 후 대상 출력 비디오 파일에 기록할 URL은 다음과 같을 수 있습니다.

<pre>
https://getkey.example.com?fileId=123456&keySource=VodBuildInKMS&edk=abcdef
</pre>


이 URL은 클라이언트가 비디오 재생 중에 복호화 키를 얻으려고 할 때 액세스해야 하는 URL이기도 합니다.

#### 4. VOD 플랫폼이 암호화를 시작하고 콜백을 완료합니다.
암호화 작업이 포함된 태스크 플로우의 상태가 변경되거나 태스크 플로우가 완료되면 VOD 플랫폼은 [태스크 플로우 상태 변경 알림](https://intl.cloud.tencent.com/document/product/266/33953)을 트리거합니다.

### 미디어 자원 관리
비디오 암호화된 후 GetVideoInfo API를 사용하여 암호화 정보를 얻을 수 있습니다.
- GetVideoInfo API는 소스 파일의 재생 주소를 포함하여 모든 트랜스코딩 사양에 따라 비디오 ID에 대한 비디오 재생 주소를 반환합니다. 소스 파일이 암호화되지 않기 때문에 App 서버는 소스 파일의 재생 주소를 필터링하고 암호화된 비디오의 재생 주소만 클라이언트에 제공하도록 선택할 수 있습니다.
- GetVideoInfo에서 얻은 소스 파일의 definition 매개변수는 0이며, 이를 기반으로 소스 파일의 재생 주소를 필터링할 수 있습니다.

## 비디오 재생 개요

인증된 최종 사용자만 비디오 암호 복호화 키를 얻을 수 있습니다. 따라서 최종 사용자를 인증하는 방법은 재생 중에 가장 중요합니다.

재생 과정에서 플레이어는 M3U8 파일의 `EXT-X-KEY` 태그로 식별된 URL에 액세스하여 키를 얻을 수 있습니다. 이 단계에서 최종 사용자의 인증 정보를 전달해야 하며, 이 정보는 두 가지 방식으로 App의 인증 서비스에 전달될 수 있습니다.

1. 최종 사용자의 ID 정보를 URL에 매개변수로 추가하고 URL을 App의 인증 서비스에 전달합니다. 이 체계는 모든 HLS 플레이어에게 적합합니다. 자세한 내용은 [비디오 재생 방식1](#p1): QueryString을 통한 실명 인증 정보 전달을 참고하십시오.
2. Cookie를 통해 최종 사용자의 ID 정보를 App의 인증 서비스로 가져옵니다. 이 방법은 더 안전하지만 `EXT-X-KEY` 태그로 식별되는 URL에 액세스할 때 Cookie를 운반하는 플레이어에게만 적합합니다. 자세한 내용은 [비디오 재생 방식2](#p2): Cookie를 통한 인증 정보 전달을 참고하십시오.

<span id="p1"></span>
### 비디오 재생 방식 1

비디오 재생 방식 1: QueryString을 통해 실명 인증 정보를 전달합니다. 이 방식은 모든 HLS 지원 플레이어에게 적합합니다.

#### 1. 로그인 후 실명 인증에 사용되는 Token 배포
인증된 최종 사용자만 비디오 암호 복호화 키를 얻을 수 있습니다. 따라서 비디오를 재생하기 전에 클라이언트에 로그인해야 하며, App 서버는 Token이라고 하는 실명 인증 정보가 포함된 서명을 클라이언트에 배포합니다.

#### 2. Key 링크 도용 방지가 포함된 멀티 비트 레이트 재생 주소 가져오기
ProcessFile API 또는 GetVideoInfo API의 콜백 알림에서 암호화된 비디오의 멀티 비트 레이트 재생 주소를 가져올 수 있습니다.
멀티 비트 레이트 재생 주소를 얻은 후 클라이언트는 최종 사용자의 ID 정보를 주소에 추가해야 합니다. 이를 위해 재생 URL의 **파일 이름** 앞에 `voddrm.token.<Token>`을 추가합니다.

예를 들어 최종 사용자의 ID가 ABC123일 때, 임의의 비트 레이트에 대한 재생 URL은 다음과 같습니다.
<pre>
http://example.vod2.myqcloud.com/path/to/a/video.m3u8
</pre>

최종 URL은 다음과 같습니다.
<pre>
http://example.vod2.myqcloud.com/path/to/a/voddrm.token.ABC123.video.m3u8
</pre>


#### 3. 비디오 콘텐츠 가져오기(암호화됨)

플레이어가 이전 단계에서 설명한 대로 최종 사용자의 ID 정보를 전달하는 URL에 액세스하면 VOD 백엔드는 소스 M3U8 파일의 `EXT-X-KEY` 태그로 식별된 URL에 Token 정보를 QueryString으로 자동 추가합니다.

예를 들어 특정 비트 레이트에 대한 암호화된 비디오 URL이 다음과 같은 경우:
<pre>
http://example.vod2.myqcloud.com/path/to/a/video.m3u8
</pre>

이 파일에서 `EXT-X-KEY`로 식별되는 비디오 복호화 키를 얻기 위한 URL은 다음과 같습니다.
<pre>
https://getkey.example.com?fileId=123456&keySource=VodBuildInKMS&edk=abcdef
</pre>

플레이어가 Token 정보를 전달하는 재생 URL에 다음과 같이 액세스합니다.
<pre>
http://example.vod2.myqcloud.com/path/to/a/voddrm.token.ABC123.video.m3u8
</pre>

`EXT-X-KEY` 태그로 식별되는 비디오 복호화 키를 얻기 위한 URL은 다음으로 대체됩니다.
<pre>
https://getkey.example.com?fileId=123456&keySource=VodBuildInKMS&edk=abcdef&token=ABC123
</pre>

이 때 플레이어가 복호화 DK를 얻으려고 하면 1단계에서 배포된 Token을 가져옵니다.

#### 4. 비디오 복호화 키 가져오기(실명 인증 Cookie 포함)

플레이어가 비디오 인덱스 파일(M3U8 파일)을 가져온 후 비디오 파일을 재생하기 전에 자동으로 4단계를 시작합니다. App 백엔드는 클라이언트의 요청을 수신한 후 먼저 QueryString에서 Token을 확인합니다. 최종 사용자의 ID가 유효하지 않은 경우 요청을  거부합니다. 최종 사용자의 ID가 유효한 경우 URL의 fileId, keySource 및 edk와 같은 매개변수를 기반으로 KMS 시스템에서 DK를 가져와 클라이언트에 반환합니다.
상기 단계가 완료되면 클라이언트는 비디오 복호화 키를 얻고 비디오 복호화 및 재생을 수행할 수 있습니다.

<span id="p2"></span>

### 비디오 재생 방식 2
비디오 재생 방식 2: Cookie를 통해 실명 인증 정보를 전달합니다. 이 방식은 iOS 장치 또는 PC의 HTML5/Flash 플레이어에만 적합합니다. 이 경우 플레이어는 `EXT-X-KEY` 태그로 식별되는 URL에 액세스할 때 Cookie를 가져옵니다.

>! 테스트에 결과 Android의 HTML5 플레이어는 `EXT-X-KEY` 태그로 식별된 URL에 액세스할 때 Cookie를 전달하지 않습니다. 그러므로 Android 플랫폼의 경우 현재 **방식 1**만 사용할 수 있습니다.

#### 1. 로그인 후 인증에 사용되는 Cookie 배포
실명 인증된 최종 사용자만 비디오 복호화 키를 얻을 수 있습니다. 따라서 비디오를 재생하기 전에 클라이언트에 로그인해야 하며, 로그인 후 App 서버가 클라이언트에 서명을 배포합니다. 예를 들어, 클라이언트가 `login.example.com`에서 계정과 암호로 로그인하고 실명 인증이 App 백엔드에 전달된 후 최종 사용자를 식별하기 위해 `example.com` 도메인의 Cookie가 클라이언트에 배포됩니다.

#### 2. 지정된 비디오의 멀티 비트 레이트 재생 주소 가져오기
VOD의 Web 플레이어는 멀티 비트 레이트 재생을 지원하며, fileId를 기반으로 비디오의 멀티 비트 레이트 재생 주소를 얻을 수 있습니다. 다른 플레이어를 사용하는 경우 멀티 비트 레이트 재생 주소를 직접 가져와야 합니다.

#### 3. 비디오 콘텐츠 가져오기(암호화됨)
플레이어는 비디오 재생을 시작할 때 이 단계를 자동으로 수행합니다.
플레이어가 비디오 재생을 시작하면 VOD의 CDN 에지 서버에서 비디오 데이터 파일을 요청합니다. HLS 형식의 비디오의 경우 플레이어는 M3U8 파일의 `EXT-X-KEY` 태그를 기반으로 비디오 복호화 키를 가져옵니다. 예를 들어 `EXT-X-KEY` 태그에서 비디오 복호화 키를 가져오는 URL은 다음과 같습니다.
<pre>
https://getkey.example.com?fileId=123456&keySource=VodBuildInKMS&edk=abcdef
</pre>

플레이어가 복호화 DK를 가져오면 1단계에서 App 백엔드에서 배포한 `example.com` 도메인의 Cookie를 가져옵니다.

#### 4. 비디오 복호화 키 가져오기(실명 인증 Cookie 포함)

플레이어가 비디오 인덱스 파일(M3U8 파일)을 가져온 후 비디오 파일을 재생하기 전에 자동으로 4단계를 시작합니다.

App 백엔드는 클라이언트의 요청을 수신한 후 먼저 Cookie의 식별자를 확인합니다. 최종 사용자의 ID가 유효하지 않은 경우 요청을 직접 거부합니다. 최종 사용자의 ID가 유효한 경우 URL의 fileId, keySource 및 edk와 같은 매개변수를 기반으로 KMS 시스템에서 DK를 가져와 클라이언트에 반환합니다.
상기 단계가 완료되면 클라이언트는 비디오 복호화 키를 얻고 비디오 복호화 및 재생을 수행할 수 있습니다.

## FAQ

####  1. 암호화된 HLS와 일반 HLS의 차이점은 무엇입니까?
HLS 사양에 따르면 HLS 암호화는 미디어 파일(TS 파일)을 암호화하는 것이며 M3U8 파일은 플레이어가 이를 해독하는 방법을 설명합니다. 암호화된 HLS의 M3U8 파일에는 `METHOD` 및 `URI` 속성이 있는 `EXT-X-KEY` 태그가 포함되어 있습니다. `METHOD`는 `AES-128`과 같은 암호화 알고리즘을 설명하고 `URI`는 복호화에 사용되는 키 데이터를 얻기 위해 플레이어가 액세스할 수 있는 복호화 키를 얻기 위한 주소를 설명합니다. URI가 다음과 같은 경우:
<pre>
http://www.test.com/getdk?fileId=123&edk=14cf
</pre>

플레이어가 M3U8 파일을 구문 분석할 때 이 URI에 HTTP 요청을 보내고 반환 패킷에서 키 데이터를 가져옵니다.

####  2. VOD 암호화를 사용하려면 어떤 정보가 필요합니까?
VOD 암호화를 활성화하려면 getkeyurl, 즉 `EXT-X-KEY` 태그의 `URI` 속성을 제공해야 합니다.
App 서버는 클라이언트가 암호화된 비디오를 재생할 때 키 데이터를 가져오는 HTTP 서비스를 배포해야 합니다. VOD 서비스가 비디오를 암호화할 때 암호화된 비디오의 M3U8 파일에 있는 `EXT-X-KEY` 태그의 `URI` 속성이 getkeyurl로 설정됩니다. 키를 가져와서 편리하게 관리하기 위해 getkeyurl에 3개의 매개변수 fileId, edk, keySource를 추가합니다.

>? fileId는 비디오 ID, edk는 암호화된 키, keySource는 키 소스입니다. VOD에 구축된 KMS 시스템으로 암호화된 파일의 경우 keySource는 VodBuildInKMS입니다. 플레이어가 복호화 키 가져오기 요청을 시작하면 App 서버가 수신한 HTTP 요청의 QueryString에 fileId 및 edk와 같은 매개변수가 포함되며, 이를 기반으로 App 서버는 해당 DK를 플레이어에 반환할 수 있습니다.

####  3. 암호화된 비디오를 재생할 때 플레이어는 어디에서 복호화 키를 얻습니까?
플레이어는 암호화된 비디오를 재생할 때 App이 VOD에 제공한 getkeyurl 주소인 M3U8 파일의 `EXT-X-KEY` 태그 URI를 기반으로 키를 얻기 위한 요청을 시작합니다.
플레이어는 키를 얻기 위해 VOD 서버에 요청하지 않습니다. App 서버가 암호화를 위해 VOD의 ProcessFile API를 호출하면 암호화가 완료된 후 비디오 복호화 키 API를 호출하여 키를 가져옵니다. 그 후 키를 저장해야 하며 플레이어가 해당 키를 요청하면 플레이어의 요청 매개변수에 따라 키를 반환합니다.

####  4. App 서버는 어떻게 키를 플레이어에 반환합니까?
플레이어가 App 서버에 키를 요청하면 App 서버는 16바이트의 바이너리 키 데이터를 플레이어에 반환해야 합니다. 그러나 비디오 복호화 키 API를 통해 얻은 키는 Base64로 인코딩된 문자열입니다. 따라서 플레이어에 반환되기 전에 문자열을 바이너리 데이터로 변환해야 합니다.
예를 들어, dkData는 Base64로 인코딩된 키 데이터입니다.

Java
```java
  import java.util.Base64;
  byte[] dkBin = Base64.getDecoder().decode(dkData);
```

PHP
```php
$dkBin = base64_decode($dkData);
```
